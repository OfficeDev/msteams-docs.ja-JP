---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 8ccc4f39b62d7aefb8d0ff56e7f0dbd00d15e356
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075655"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="285ec-104">Teams 会議用のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="285ec-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="285ec-105">前提条件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="285ec-105">Prerequisites and considerations</span></span>

<span data-ttu-id="285ec-106">会議のアプリを作成Teams、次の情報を理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="285ec-107">アプリを開発する方法に関する知識Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="285ec-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="285ec-108">詳細については、「アプリ開発の[Teams」を参照してください](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="285ec-109">アプリが会議でTeamsを示すために、アプリ マニフェストを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="285ec-110">詳細については、「アプリ マニフェスト [」を参照してください](#update-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="285ec-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="285ec-111">アプリが会議のライフサイクルでタブとして機能するには、グループチャット スコープで構成可能なタブをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="285ec-112">詳細については[、「groupchat スコープ」を参照し、](../resources/schema/manifest-schema.md#configurabletabs)[グループ タブを作成するを参照してください](../build-your-first-app/build-channel-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="285ec-113">会議前および会議後のシナリオTeams一般的なタブ設計ガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="285ec-114">会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="285ec-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="285ec-115">詳細については、「[タブデザイン](../tabs/design/tabs.md)Teams、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="285ec-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="285ec-116">会議前および会議後のチャットでアプリを有効にするには、この `groupchat` 範囲をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="285ec-117">会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="285ec-118">会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果やフィードバックなど、会議の結果を表示できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="285ec-119">会議 API の URL パラメーターには、、 `meetingId` 、 `userId` および を指定する必要があります `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="285ec-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="285ec-120">これらは、クライアント SDK およびボット アクティビティTeams使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="285ec-121">さらに、ユーザー ID とテナント ID の信頼できる情報は、Tab SSO 認証を使用 [して取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="285ec-122">認証 `GetParticipant` トークンを生成するには、API にボット登録と ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="285ec-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="285ec-123">詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="285ec-124">アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="285ec-125">これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。</span><span class="sxs-lookup"><span data-stu-id="285ec-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="285ec-126">[会議内] ダイアログ ボックスについては、「で完了パラメーター」 `bot Id` を参照してください `Notification Signal API` 。</span><span class="sxs-lookup"><span data-stu-id="285ec-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="285ec-127">会議アプリ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="285ec-127">Meeting apps API reference</span></span>

|<span data-ttu-id="285ec-128">API</span><span class="sxs-lookup"><span data-stu-id="285ec-128">API</span></span>|<span data-ttu-id="285ec-129">説明</span><span class="sxs-lookup"><span data-stu-id="285ec-129">Description</span></span>|<span data-ttu-id="285ec-130">要求</span><span class="sxs-lookup"><span data-stu-id="285ec-130">Request</span></span>|<span data-ttu-id="285ec-131">ソース</span><span class="sxs-lookup"><span data-stu-id="285ec-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="285ec-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="285ec-132">**GetUserContext**</span></span>| <span data-ttu-id="285ec-133">この API を使用すると、コンテキスト情報を取得して、関連するコンテンツを [コンテンツ] タブTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="285ec-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="285ec-134">_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="285ec-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="285ec-135">Microsoft Teams SDK</span><span class="sxs-lookup"><span data-stu-id="285ec-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="285ec-136">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="285ec-136">**GetParticipant**</span></span>| <span data-ttu-id="285ec-137">この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="285ec-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="285ec-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="285ec-139">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="285ec-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="285ec-140">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="285ec-140">**NotificationSignal**</span></span> | <span data-ttu-id="285ec-141">この API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="285ec-142">これにより、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="285ec-143">**POST** _**/v3/conversation/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="285ec-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="285ec-144">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="285ec-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="285ec-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="285ec-145">GetUserContext</span></span>

<span data-ttu-id="285ec-146">タブ コンテンツのコンテキスト情報を特定して取得するには[、「get context for your Teams タブ」を参照してください](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`は、会議コンテキストで実行するときにタブで使用され、応答ペイロードに追加されます。</span><span class="sxs-lookup"><span data-stu-id="285ec-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="285ec-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="285ec-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="285ec-148">会議の開催者がいつでも役割を変更できるので、参加者の役割をキャッシュしない。</span><span class="sxs-lookup"><span data-stu-id="285ec-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="285ec-149">Teams現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズはサポート `GetParticipant` されていません。</span><span class="sxs-lookup"><span data-stu-id="285ec-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="285ec-150">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="285ec-150">Query parameters</span></span>

|<span data-ttu-id="285ec-151">値</span><span class="sxs-lookup"><span data-stu-id="285ec-151">Value</span></span>|<span data-ttu-id="285ec-152">型</span><span class="sxs-lookup"><span data-stu-id="285ec-152">Type</span></span>|<span data-ttu-id="285ec-153">必須</span><span class="sxs-lookup"><span data-stu-id="285ec-153">Required</span></span>|<span data-ttu-id="285ec-154">説明</span><span class="sxs-lookup"><span data-stu-id="285ec-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="285ec-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="285ec-155">**meetingId**</span></span>| <span data-ttu-id="285ec-156">文字列</span><span class="sxs-lookup"><span data-stu-id="285ec-156">string</span></span> | <span data-ttu-id="285ec-157">はい</span><span class="sxs-lookup"><span data-stu-id="285ec-157">Yes</span></span> | <span data-ttu-id="285ec-158">会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="285ec-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="285ec-159">**participantId**</span></span>| <span data-ttu-id="285ec-160">文字列</span><span class="sxs-lookup"><span data-stu-id="285ec-160">string</span></span> | <span data-ttu-id="285ec-161">はい</span><span class="sxs-lookup"><span data-stu-id="285ec-161">Yes</span></span> | <span data-ttu-id="285ec-162">参加者 ID はユーザー ID です。</span><span class="sxs-lookup"><span data-stu-id="285ec-162">The participant ID is the user ID.</span></span> <span data-ttu-id="285ec-163">これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="285ec-164">Tab SSO から参加者 ID を取得する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="285ec-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="285ec-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="285ec-165">**tenantId**</span></span>| <span data-ttu-id="285ec-166">文字列</span><span class="sxs-lookup"><span data-stu-id="285ec-166">string</span></span> | <span data-ttu-id="285ec-167">はい</span><span class="sxs-lookup"><span data-stu-id="285ec-167">Yes</span></span> | <span data-ttu-id="285ec-168">テナントユーザーにはテナント ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="285ec-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="285ec-169">これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="285ec-170">Tab SSO からテナント ID を取得する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="285ec-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="285ec-171">例</span><span class="sxs-lookup"><span data-stu-id="285ec-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="285ec-172">C#</span><span class="sxs-lookup"><span data-stu-id="285ec-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="285ec-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="285ec-173">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="285ec-174">JSON</span><span class="sxs-lookup"><span data-stu-id="285ec-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="285ec-175">API の JSON 応答 `GetParticipant` 本文は次の形式です。</span><span class="sxs-lookup"><span data-stu-id="285ec-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="285ec-176">応答コード</span><span class="sxs-lookup"><span data-stu-id="285ec-176">Response codes</span></span>

|<span data-ttu-id="285ec-177">応答コード</span><span class="sxs-lookup"><span data-stu-id="285ec-177">Response code</span></span>|<span data-ttu-id="285ec-178">説明</span><span class="sxs-lookup"><span data-stu-id="285ec-178">Description</span></span>|
|---|---|
| <span data-ttu-id="285ec-179">**403**</span><span class="sxs-lookup"><span data-stu-id="285ec-179">**403**</span></span> | <span data-ttu-id="285ec-180">アプリは参加者情報の取得を許可されません。</span><span class="sxs-lookup"><span data-stu-id="285ec-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="285ec-181">これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="285ec-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="285ec-182">たとえば、テナント管理者によってアプリが無効になっている場合や、ライブ サイトの移行中にブロックされている場合などです。</span><span class="sxs-lookup"><span data-stu-id="285ec-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="285ec-183">**200**</span><span class="sxs-lookup"><span data-stu-id="285ec-183">**200**</span></span> | <span data-ttu-id="285ec-184">参加者情報が正常に取得されます。</span><span class="sxs-lookup"><span data-stu-id="285ec-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="285ec-185">**401**</span><span class="sxs-lookup"><span data-stu-id="285ec-185">**401**</span></span> | <span data-ttu-id="285ec-186">アプリは無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="285ec-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="285ec-187">**404**</span><span class="sxs-lookup"><span data-stu-id="285ec-187">**404**</span></span> | <span data-ttu-id="285ec-188">会議の有効期限が切れているか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="285ec-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="285ec-189">**500**</span><span class="sxs-lookup"><span data-stu-id="285ec-189">**500**</span></span> | <span data-ttu-id="285ec-190">会議が終了して 60 日以上経過した場合、または参加者が自分の役割に基づくアクセス許可を持っていません。</span><span class="sxs-lookup"><span data-stu-id="285ec-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="285ec-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="285ec-191">NotificationSignal API</span></span>

<span data-ttu-id="285ec-192">会議のすべてのユーザーは、API を介して送信された通知を受け取 `NotificationSignal` る。</span><span class="sxs-lookup"><span data-stu-id="285ec-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="285ec-193">会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="285ec-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="285ec-194">現在、ターゲット通知の送信はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="285ec-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="285ec-195">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="285ec-195">Query parameters</span></span>

|<span data-ttu-id="285ec-196">値</span><span class="sxs-lookup"><span data-stu-id="285ec-196">Value</span></span>|<span data-ttu-id="285ec-197">型</span><span class="sxs-lookup"><span data-stu-id="285ec-197">Type</span></span>|<span data-ttu-id="285ec-198">必須</span><span class="sxs-lookup"><span data-stu-id="285ec-198">Required</span></span>|<span data-ttu-id="285ec-199">説明</span><span class="sxs-lookup"><span data-stu-id="285ec-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="285ec-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="285ec-200">**conversationId**</span></span>| <span data-ttu-id="285ec-201">文字列</span><span class="sxs-lookup"><span data-stu-id="285ec-201">string</span></span> | <span data-ttu-id="285ec-202">はい</span><span class="sxs-lookup"><span data-stu-id="285ec-202">Yes</span></span> | <span data-ttu-id="285ec-203">会話識別子は、ボットの呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-203">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="285ec-204">例</span><span class="sxs-lookup"><span data-stu-id="285ec-204">Example</span></span>

<span data-ttu-id="285ec-205">は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="285ec-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="285ec-206">要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、the のパラメーターは省略可能です。</span><span class="sxs-lookup"><span data-stu-id="285ec-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="285ec-207">`Bot ID` はマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="285ec-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="285ec-208">幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="285ec-209">寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="285ec-210">URL は、会議中のダイアログ ボックスに表示 `<iframe>` されるページです。</span><span class="sxs-lookup"><span data-stu-id="285ec-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="285ec-211">ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="285ec-212">C#</span><span class="sxs-lookup"><span data-stu-id="285ec-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="285ec-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="285ec-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="285ec-214">JSON</span><span class="sxs-lookup"><span data-stu-id="285ec-214">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="285ec-215">応答コード</span><span class="sxs-lookup"><span data-stu-id="285ec-215">Response codes</span></span>

|<span data-ttu-id="285ec-216">応答コード</span><span class="sxs-lookup"><span data-stu-id="285ec-216">Response code</span></span>|<span data-ttu-id="285ec-217">説明</span><span class="sxs-lookup"><span data-stu-id="285ec-217">Description</span></span>|
|---|---|
| <span data-ttu-id="285ec-218">**201**</span><span class="sxs-lookup"><span data-stu-id="285ec-218">**201**</span></span> | <span data-ttu-id="285ec-219">シグナルを含むアクティビティが正常に送信される</span><span class="sxs-lookup"><span data-stu-id="285ec-219">The activity with signal is successfully sent</span></span> |
| <span data-ttu-id="285ec-220">**401**</span><span class="sxs-lookup"><span data-stu-id="285ec-220">**401**</span></span> | <span data-ttu-id="285ec-221">アプリは無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="285ec-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="285ec-222">**403**</span><span class="sxs-lookup"><span data-stu-id="285ec-222">**403**</span></span> | <span data-ttu-id="285ec-223">アプリは信号を送信できません。</span><span class="sxs-lookup"><span data-stu-id="285ec-223">The app is unable to send the signal.</span></span> <span data-ttu-id="285ec-224">これは、テナント管理者がアプリを無効にし、アプリがライブ サイトの移行中にブロックされるなど、さまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="285ec-225">この場合、ペイロードには詳細なエラー メッセージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="285ec-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="285ec-226">**404**</span><span class="sxs-lookup"><span data-stu-id="285ec-226">**404**</span></span> | <span data-ttu-id="285ec-227">会議チャットが存在しません。</span><span class="sxs-lookup"><span data-stu-id="285ec-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="285ec-228">会議でアプリを有効Teamsする</span><span class="sxs-lookup"><span data-stu-id="285ec-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="285ec-229">アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="285ec-229">Update your app manifest</span></span>

<span data-ttu-id="285ec-230">会議アプリの機能は、、 、および配列を使用してアプリ マニフェスト `configurableTabs` `scopes` で宣言 `context` されます。</span><span class="sxs-lookup"><span data-stu-id="285ec-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="285ec-231">スコープは、アプリを使用できる場所を定義するユーザーとコンテキストを定義します。</span><span class="sxs-lookup"><span data-stu-id="285ec-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="285ec-232">マニフェスト スキーマを使用してアプリ マニフェストを [更新してみてください](../resources/schema/manifest-schema-dev-preview.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="285ec-233">会議のアプリには、 *グループチャットスコープが必要* です。</span><span class="sxs-lookup"><span data-stu-id="285ec-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="285ec-234">チーム *スコープは* 、チャネル内のタブでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="285ec-234">The *team* scope works for tabs in channels only.</span></span>

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
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> <span data-ttu-id="285ec-235">`meetingStage` は現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="285ec-236">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="285ec-236">Context property</span></span>

<span data-ttu-id="285ec-237">タブと `context` プロパティ `scopes` を使用すると、アプリを表示する必要がある場所を特定できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="285ec-238">またはスコープ内 `team` のタブ `groupchat` には、複数のコンテキストを指定できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="285ec-239">値のすべてまたは一部を使用できるプロパティの値を `context` 次に示します。</span><span class="sxs-lookup"><span data-stu-id="285ec-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="285ec-240">値</span><span class="sxs-lookup"><span data-stu-id="285ec-240">Value</span></span>|<span data-ttu-id="285ec-241">説明</span><span class="sxs-lookup"><span data-stu-id="285ec-241">Description</span></span>|
|---|---|
| <span data-ttu-id="285ec-242">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="285ec-242">**channelTab**</span></span> | <span data-ttu-id="285ec-243">チーム チャネルのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="285ec-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="285ec-244">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="285ec-244">**privateChatTab**</span></span> | <span data-ttu-id="285ec-245">チームまたは会議のコンテキストではない一連のユーザー間のグループ チャットのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="285ec-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="285ec-246">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="285ec-246">**meetingChatTab**</span></span> | <span data-ttu-id="285ec-247">スケジュールされた会議のコンテキスト内の一連のユーザー間のグループ チャットのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="285ec-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="285ec-248">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="285ec-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="285ec-249">予定表の会議の詳細ビューのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="285ec-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="285ec-250">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="285ec-250">**meetingSidePanel**</span></span> | <span data-ttu-id="285ec-251">統合バー (U バー) を介して開いた会議内パネル。</span><span class="sxs-lookup"><span data-stu-id="285ec-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="285ec-252">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="285ec-252">**meetingStage**</span></span> | <span data-ttu-id="285ec-253">サイドパネルのアプリを会議ステージに共有できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="285ec-254">`Context` プロパティは現在、モバイル クライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="285ec-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="285ec-255">会議シナリオ用にアプリを構成する</span><span class="sxs-lookup"><span data-stu-id="285ec-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="285ec-256">タブ ギャラリーにアプリを表示するには、構成可能なタブとグループ チャットスコープをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="285ec-257">モバイル クライアントは、会議の開催前と開催後のステージでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="285ec-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="285ec-258">現在、モバイル クライアントでは、会議中のダイアログ ボックスとタブである会議内エクスペリエンスはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="285ec-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="285ec-259">詳細については、「モバイル用の [タブを作成する際の](../tabs/design/tabs-mobile.md) モバイルタブのガイダンス」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="285ec-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="285ec-260">会議の前に</span><span class="sxs-lookup"><span data-stu-id="285ec-260">Before a meeting</span></span>

<span data-ttu-id="285ec-261">会議の前に、ユーザーはタブ、ボット、メッセージング拡張機能を会議に追加できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="285ec-262">開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="285ec-263">**タブを会議に追加するには**</span><span class="sxs-lookup"><span data-stu-id="285ec-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="285ec-264">予定表で、タブを追加する会議を選択します。</span><span class="sxs-lookup"><span data-stu-id="285ec-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="285ec-265">[詳細] **タブを選択** し、[プラス] を選択します。</span><span class="sxs-lookup"><span data-stu-id="285ec-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="285ec-266">.</span><span class="sxs-lookup"><span data-stu-id="285ec-266">.</span></span> <span data-ttu-id="285ec-267">タブ ギャラリーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="285ec-267">The tab gallery appears.</span></span>

    ![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="285ec-269">タブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。</span><span class="sxs-lookup"><span data-stu-id="285ec-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="285ec-270">アプリはタブとしてインストールされます。</span><span class="sxs-lookup"><span data-stu-id="285ec-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="285ec-271">現在、会議タブでは、会議の詳細と参加者情報の取得はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="285ec-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="285ec-272">**会議にメッセージング拡張機能を追加するには**</span><span class="sxs-lookup"><span data-stu-id="285ec-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="285ec-273">チャット内のメッセージの作成 &#x25CF;&#x25CF;&#x25CF; にある省略記号またはオーバーフロー メニューを選択します。</span><span class="sxs-lookup"><span data-stu-id="285ec-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="285ec-274">追加するアプリを選択し、必要に応じて手順に従います。</span><span class="sxs-lookup"><span data-stu-id="285ec-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="285ec-275">アプリはメッセージング拡張機能としてインストールされます。</span><span class="sxs-lookup"><span data-stu-id="285ec-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="285ec-276">**ボットを会議に追加するには**</span><span class="sxs-lookup"><span data-stu-id="285ec-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="285ec-277">会議チャットでキーを入力し **@** 、[ボットの取得 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="285ec-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="285ec-278">ユーザー ID は、Tabs SSO を使用して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="285ec-279">認証後、アプリは API を使用してユーザー ロールを取得 `GetParticipant` できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="285ec-280">ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="285ec-281">たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="285ec-282">会議の進行中に役割の割り当てを変更できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="285ec-283">詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="285ec-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="285ec-284">会議中</span><span class="sxs-lookup"><span data-stu-id="285ec-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="285ec-285">sidePanel</span><span class="sxs-lookup"><span data-stu-id="285ec-285">sidePanel</span></span>

<span data-ttu-id="285ec-286">sidePanel を使用すると、会議のエクスペリエンスをカスタマイズして、開催者と発表者が異なるビューとアクションのセットを持つ事が可能です。</span><span class="sxs-lookup"><span data-stu-id="285ec-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="285ec-287">アプリ マニフェストで、コンテキスト配列に sidePanel を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="285ec-288">会議およびすべてのシナリオで、アプリは幅 320 ピクセルの会議内タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="285ec-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="285ec-289">詳細については [、「FrameContext インターフェイス」を参照してください](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)。</span><span class="sxs-lookup"><span data-stu-id="285ec-289">For more information, see [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="285ec-290">API を使用して要求を必要に応じてルーティングするには、「SDK `userContext` Teams[参照してください](../tabs/how-to/access-teams-context.md#user-context)。</span><span class="sxs-lookup"><span data-stu-id="285ec-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="285ec-291">タブについては[Teams認証フローを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="285ec-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="285ec-292">タブの認証フローは、Web サイトの認証フローと非常に似ています。</span><span class="sxs-lookup"><span data-stu-id="285ec-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="285ec-293">したがって、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="285ec-294">参照[、Microsoft ID プラットフォーム OAuth 2.0 承認コード フローを参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="285ec-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="285ec-295">メッセージング拡張機能は、ユーザーが会議内ビューにいて、ユーザーが作成メッセージ拡張カードを投稿できる場合に期待通り動作します。</span><span class="sxs-lookup"><span data-stu-id="285ec-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="285ec-296">AppName in-meeting は、会議中の U バーのアプリ名を示すツールヒントです。</span><span class="sxs-lookup"><span data-stu-id="285ec-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="285ec-297">バージョン 1.7.0 以上の[Teams SDK](https://docs.microsoft.com/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用します。前のバージョンではサイド パネルはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="285ec-297">Use version 1.7.0 or higher of [Teams SDK](https://docs.microsoft.com/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="285ec-298">会議中ダイアログ</span><span class="sxs-lookup"><span data-stu-id="285ec-298">In-meeting dialog</span></span>

<span data-ttu-id="285ec-299">[会議中] ダイアログ ボックスを使用すると、会議中に参加者を引き付け、会議中に情報やフィードバックを収集できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-299">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="285ec-300">API を [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) 使用して、バブル通知をトリガーする必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-300">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="285ec-301">通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含める。</span><span class="sxs-lookup"><span data-stu-id="285ec-301">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="285ec-302">会議中のダイアログでは、タスク モジュールを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="285ec-302">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="285ec-303">タスク モジュールは、会議チャットでは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="285ec-303">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="285ec-304">外部リソース URL を使用して、会議にコンテンツ バブルを表示します。</span><span class="sxs-lookup"><span data-stu-id="285ec-304">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="285ec-305">このメソッドを使用 `submitTask` して、会議チャットでデータを送信できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-305">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="285ec-306">ユーザーが Web ビューでアクションを実行した後に自動的に終了するには [、submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-306">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="285ec-307">これは、アプリの申請に必要な要件です。</span><span class="sxs-lookup"><span data-stu-id="285ec-307">This is a requirement for app submission.</span></span> <span data-ttu-id="285ec-308">詳細については、「SDK タスク モジュール[Teamsを参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="285ec-308">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="285ec-309">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、要求メタデータではなく、オブジェクト内の要求メタデータ `from.id` `from` に `from.aadObjectId` 依存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-309">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="285ec-310">`from.id`はユーザー ID であり `from.aadObjectId` 、ユーザー Azure Active Directory (AAD) ID です。</span><span class="sxs-lookup"><span data-stu-id="285ec-310">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="285ec-311">詳細については、「タブでタスク [モジュールを使用する」を参照し](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、 [タスク モジュールを作成して送信します](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="285ec-311">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="285ec-312">ステージ間の共有</span><span class="sxs-lookup"><span data-stu-id="285ec-312">Share to stage</span></span> 

> [!NOTE]
> * <span data-ttu-id="285ec-313">この機能は現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-313">This capability is currently available in developer preview only.</span></span>
> * <span data-ttu-id="285ec-314">この機能を使用するには、アプリが会議中のサイドパネルをサポートしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-314">To use this feature, the app must support an in-meeting sidepanel.</span></span>


<span data-ttu-id="285ec-315">この機能により、開発者はアプリを会議ステージに共有できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-315">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="285ec-316">会議ステージへの共有を有効にすると、会議の参加者はリアルタイムで共同作業できます。</span><span class="sxs-lookup"><span data-stu-id="285ec-316">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="285ec-317">必要なコンテキストは `meetingStage` 、アプリ マニフェスト内です。</span><span class="sxs-lookup"><span data-stu-id="285ec-317">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="285ec-318">このための前提条件は、コンテキストを持 `meetingSidePanel` つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="285ec-318">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="285ec-319">これにより、 **サイドパネルの** [共有] ボタンが次の図で切り離されます。</span><span class="sxs-lookup"><span data-stu-id="285ec-319">This enables the **Share** button in the sidepanel as depecited in the following image:</span></span>

  ![share_to_stage_during_meetingエクスペリエンス](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="285ec-321">この機能を有効にするために必要なマニフェストの変更は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="285ec-321">The manifest change that is needed to enable this capability is as follows:</span></span> 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a><span data-ttu-id="285ec-322">会議の後</span><span class="sxs-lookup"><span data-stu-id="285ec-322">After a meeting</span></span>

<span data-ttu-id="285ec-323">会議後と会議前の構成は同等です。</span><span class="sxs-lookup"><span data-stu-id="285ec-323">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="285ec-324">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="285ec-324">Code sample</span></span>

|<span data-ttu-id="285ec-325">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="285ec-325">Sample name</span></span> | <span data-ttu-id="285ec-326">説明</span><span class="sxs-lookup"><span data-stu-id="285ec-326">Description</span></span> | <span data-ttu-id="285ec-327">.NET</span><span class="sxs-lookup"><span data-stu-id="285ec-327">.NET</span></span> | <span data-ttu-id="285ec-328">Node.js</span><span class="sxs-lookup"><span data-stu-id="285ec-328">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="285ec-329">会議の機能拡張</span><span class="sxs-lookup"><span data-stu-id="285ec-329">Meetings extensibility</span></span> | <span data-ttu-id="285ec-330">Microsoft Teams渡しに関する会議機能拡張サンプル。</span><span class="sxs-lookup"><span data-stu-id="285ec-330">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="285ec-331">View</span><span class="sxs-lookup"><span data-stu-id="285ec-331">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | |
| <span data-ttu-id="285ec-332">会議コンテンツ バブル ボット</span><span class="sxs-lookup"><span data-stu-id="285ec-332">Meeting content bubble bot</span></span> | <span data-ttu-id="285ec-333">Microsoft Teamsでコンテンツ バブル ボットを操作するための会議機能拡張サンプルを作成します。</span><span class="sxs-lookup"><span data-stu-id="285ec-333">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="285ec-334">View</span><span class="sxs-lookup"><span data-stu-id="285ec-334">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="285ec-335">View</span><span class="sxs-lookup"><span data-stu-id="285ec-335">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="285ec-336">Meeting SidePanel</span><span class="sxs-lookup"><span data-stu-id="285ec-336">Meeting SidePanel</span></span> | <span data-ttu-id="285ec-337">Microsoft Teams会議のサイド パネルで iteracting の会議機能拡張サンプルを作成します。</span><span class="sxs-lookup"><span data-stu-id="285ec-337">Microsoft Teams meeting extensibility sample for iteracting with the side panel in-meeting.</span></span> | [<span data-ttu-id="285ec-338">View</span><span class="sxs-lookup"><span data-stu-id="285ec-338">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a><span data-ttu-id="285ec-339">関連項目</span><span class="sxs-lookup"><span data-stu-id="285ec-339">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="285ec-340">会議中のダイアログの設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="285ec-340">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [<span data-ttu-id="285ec-341">Teamsの認証フロー</span><span class="sxs-lookup"><span data-stu-id="285ec-341">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
