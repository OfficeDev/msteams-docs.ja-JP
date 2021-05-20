---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: チーム アプリ 会議ユーザー参加者ロール API
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565915"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="42b63-104">Teams 会議用のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="42b63-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="42b63-105">前提条件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="42b63-105">Prerequisites and considerations</span></span>

<span data-ttu-id="42b63-106">Teams会議用のアプリを作成する前に、次の点を理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="42b63-107">Teamsアプリの開発方法に関する知識が必要です。</span><span class="sxs-lookup"><span data-stu-id="42b63-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="42b63-108">詳細については、「[アプリ開発Teams」](../overview.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="42b63-109">アプリが会議で利用できることを示すには、Teams アプリ マニフェストを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="42b63-110">詳細については、「アプリ [マニフェスト」を参照してください](#update-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="42b63-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="42b63-111">アプリが会議のライフサイクルでタブとして機能するには、groupchat スコープで構成可能なタブをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="42b63-112">詳細については、「 [グループチャットのスコープ](../resources/schema/manifest-schema.md#configurabletabs) と [グループ タブの作成](../build-your-first-app/build-channel-tab.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="42b63-113">会議前および会議後のシナリオに関する一般的なTeamsタブ設計ガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="42b63-114">会議中のエクスペリエンスについては、会議内のタブと会議中のダイアログ の設計ガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="42b63-115">詳細については[、「Teams タブ設計ガイドライン](../tabs/design/tabs.md)、[ミーティングタブ設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)、および[ミーティングダイアログの設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="42b63-116">`groupchat`会議前および会議後のチャットでアプリを有効にするには、スコープをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="42b63-117">会議前のアプリエクスペリエンスを使用すると、会議アプリを見つけて追加したり、会議前のタスクを実行したりできます。</span><span class="sxs-lookup"><span data-stu-id="42b63-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="42b63-118">会議後のアプリエクスペリエンスを使用すると、アンケート調査結果やフィードバックなど、会議の結果を表示できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="42b63-119">会議 API の URL パラメータには `meetingId` `userId` 、 、および が必要です `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="42b63-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="42b63-120">これらは、クライアント SDK とボットアクティビティTeamsの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="42b63-121">さらに、 [タブ SSO 認証](../tabs/how-to/authentication/auth-aad-sso.md)を使用して、ユーザー ID とテナント ID の信頼できる情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="42b63-122">`GetParticipant`認証トークンを生成するには、API にボット登録と ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="42b63-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="42b63-123">詳細については、「 [ボットの登録と ID](../build-your-first-app/build-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="42b63-124">アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいて最新の状態にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="42b63-125">これらのイベントは、会議のライフサイクル全体で、会議内のダイアログ ボックスやその他のステージ内に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="42b63-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="42b63-126">[会議中] ダイアログ ボックスについては、 `bot Id` の完了パラメーターを参照してください `Notification Signal API` 。</span><span class="sxs-lookup"><span data-stu-id="42b63-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="42b63-127">ミーティング アプリ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="42b63-127">Meeting apps API reference</span></span>

|<span data-ttu-id="42b63-128">API</span><span class="sxs-lookup"><span data-stu-id="42b63-128">API</span></span>|<span data-ttu-id="42b63-129">説明</span><span class="sxs-lookup"><span data-stu-id="42b63-129">Description</span></span>|<span data-ttu-id="42b63-130">要求</span><span class="sxs-lookup"><span data-stu-id="42b63-130">Request</span></span>|<span data-ttu-id="42b63-131">ソース</span><span class="sxs-lookup"><span data-stu-id="42b63-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="42b63-132">**ユーザーコンテキストを取得します。**</span><span class="sxs-lookup"><span data-stu-id="42b63-132">**GetUserContext**</span></span>| <span data-ttu-id="42b63-133">この API を使用すると、コンテキスト情報を取得して、関連するコンテンツをTeamsタブに表示できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="42b63-134">_**> { /*..*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="42b63-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="42b63-135">クライアント SDK Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="42b63-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="42b63-136">**参加者を取得します。**</span><span class="sxs-lookup"><span data-stu-id="42b63-136">**GetParticipant**</span></span>| <span data-ttu-id="42b63-137">この API により、ボットはミーティング ID と参加者 ID によって参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="42b63-138">**GET** _**/v1/会議/{会議Id}/参加者/{参加者Id}?テナントId={テナントId}**_</span><span class="sxs-lookup"><span data-stu-id="42b63-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="42b63-139">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="42b63-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="42b63-140">**通知シグナル**</span><span class="sxs-lookup"><span data-stu-id="42b63-140">**NotificationSignal**</span></span> | <span data-ttu-id="42b63-141">この API を使用すると、ユーザーボットチャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="42b63-142">会議中のダイアログ ボックスを表示するユーザーアクションに基づいて通知できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="42b63-143">**ポスト** _**/v3/会話/{会話Id}/アクティビティ**_</span><span class="sxs-lookup"><span data-stu-id="42b63-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="42b63-144">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="42b63-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="42b63-145">ユーザーコンテキストを取得します。</span><span class="sxs-lookup"><span data-stu-id="42b63-145">GetUserContext</span></span>

<span data-ttu-id="42b63-146">タブコンテンツのコンテキスト情報を識別して取得するには[、「Teamsタブのコンテキストを取得する](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)」を参照してください。`meetingId`は、会議コンテキストで実行しているときにタブによって使用され、応答ペイロードに追加されます。</span><span class="sxs-lookup"><span data-stu-id="42b63-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="42b63-147">参加者の取得 API</span><span class="sxs-lookup"><span data-stu-id="42b63-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="42b63-148">会議の開催者はいつでもロールを変更できるため、参加者ロールをキャッシュしないでください。</span><span class="sxs-lookup"><span data-stu-id="42b63-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="42b63-149">Teamsは現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズをサポートしていません `GetParticipant` 。</span><span class="sxs-lookup"><span data-stu-id="42b63-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="42b63-150">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="42b63-150">Query parameters</span></span>

|<span data-ttu-id="42b63-151">値</span><span class="sxs-lookup"><span data-stu-id="42b63-151">Value</span></span>|<span data-ttu-id="42b63-152">型</span><span class="sxs-lookup"><span data-stu-id="42b63-152">Type</span></span>|<span data-ttu-id="42b63-153">必須</span><span class="sxs-lookup"><span data-stu-id="42b63-153">Required</span></span>|<span data-ttu-id="42b63-154">説明</span><span class="sxs-lookup"><span data-stu-id="42b63-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="42b63-155">**ミーティングID**</span><span class="sxs-lookup"><span data-stu-id="42b63-155">**meetingId**</span></span>| <span data-ttu-id="42b63-156">文字列</span><span class="sxs-lookup"><span data-stu-id="42b63-156">string</span></span> | <span data-ttu-id="42b63-157">はい</span><span class="sxs-lookup"><span data-stu-id="42b63-157">Yes</span></span> | <span data-ttu-id="42b63-158">会議の識別子は、ボット呼び出しとクライアント SDK Teamsを通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="42b63-159">**参加者 ID**</span><span class="sxs-lookup"><span data-stu-id="42b63-159">**participantId**</span></span>| <span data-ttu-id="42b63-160">文字列</span><span class="sxs-lookup"><span data-stu-id="42b63-160">string</span></span> | <span data-ttu-id="42b63-161">はい</span><span class="sxs-lookup"><span data-stu-id="42b63-161">Yes</span></span> | <span data-ttu-id="42b63-162">参加者 ID はユーザー ID です。</span><span class="sxs-lookup"><span data-stu-id="42b63-162">The participant ID is the user ID.</span></span> <span data-ttu-id="42b63-163">タブ SSO、ボット呼び出し、およびクライアント SDK Teamsで使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="42b63-164">タブ SSO から参加者 ID を取得することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="42b63-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="42b63-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="42b63-165">**tenantId**</span></span>| <span data-ttu-id="42b63-166">文字列</span><span class="sxs-lookup"><span data-stu-id="42b63-166">string</span></span> | <span data-ttu-id="42b63-167">はい</span><span class="sxs-lookup"><span data-stu-id="42b63-167">Yes</span></span> | <span data-ttu-id="42b63-168">テナントのユーザーにはテナント ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="42b63-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="42b63-169">タブ SSO、ボット呼び出し、およびクライアント SDK Teamsで使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="42b63-170">タブ SSO からテナント ID を取得することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="42b63-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="42b63-171">例</span><span class="sxs-lookup"><span data-stu-id="42b63-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="42b63-172">C#</span><span class="sxs-lookup"><span data-stu-id="42b63-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="42b63-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="42b63-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="42b63-174">JSON</span><span class="sxs-lookup"><span data-stu-id="42b63-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="42b63-175">API の JSON 応答の本文 `GetParticipant` は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="42b63-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="42b63-176">応答コード</span><span class="sxs-lookup"><span data-stu-id="42b63-176">Response codes</span></span>

|<span data-ttu-id="42b63-177">応答コード</span><span class="sxs-lookup"><span data-stu-id="42b63-177">Response code</span></span>|<span data-ttu-id="42b63-178">説明</span><span class="sxs-lookup"><span data-stu-id="42b63-178">Description</span></span>|
|---|---|
| <span data-ttu-id="42b63-179">**403**</span><span class="sxs-lookup"><span data-stu-id="42b63-179">**403**</span></span> | <span data-ttu-id="42b63-180">アプリは参加者情報を取得できません。</span><span class="sxs-lookup"><span data-stu-id="42b63-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="42b63-181">これは最も一般的なエラー応答であり、会議でアプリがインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="42b63-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="42b63-182">たとえば、アプリがテナント管理者によって無効にされた場合や、ライブ サイトの移行中にブロックされた場合などです。</span><span class="sxs-lookup"><span data-stu-id="42b63-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="42b63-183">**200**</span><span class="sxs-lookup"><span data-stu-id="42b63-183">**200**</span></span> | <span data-ttu-id="42b63-184">参加者情報が正常に取得されました。</span><span class="sxs-lookup"><span data-stu-id="42b63-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="42b63-185">**401**</span><span class="sxs-lookup"><span data-stu-id="42b63-185">**401**</span></span> | <span data-ttu-id="42b63-186">アプリが無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="42b63-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="42b63-187">**404**</span><span class="sxs-lookup"><span data-stu-id="42b63-187">**404**</span></span> | <span data-ttu-id="42b63-188">会議の期限が切れているか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="42b63-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="42b63-189">**500**</span><span class="sxs-lookup"><span data-stu-id="42b63-189">**500**</span></span> | <span data-ttu-id="42b63-190">会議の終了後 60 日以上経過したか、または参加者のロールに基づくアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="42b63-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="42b63-191">通知シグナル API</span><span class="sxs-lookup"><span data-stu-id="42b63-191">NotificationSignal API</span></span>

<span data-ttu-id="42b63-192">会議のすべてのユーザーは、API を介して送信された通知を受信します `NotificationSignal` 。</span><span class="sxs-lookup"><span data-stu-id="42b63-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="42b63-193">会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="42b63-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="42b63-194">現在、対象通知の送信はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="42b63-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="42b63-195">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="42b63-195">Query parameters</span></span>

|<span data-ttu-id="42b63-196">値</span><span class="sxs-lookup"><span data-stu-id="42b63-196">Value</span></span>|<span data-ttu-id="42b63-197">型</span><span class="sxs-lookup"><span data-stu-id="42b63-197">Type</span></span>|<span data-ttu-id="42b63-198">必須</span><span class="sxs-lookup"><span data-stu-id="42b63-198">Required</span></span>|<span data-ttu-id="42b63-199">説明</span><span class="sxs-lookup"><span data-stu-id="42b63-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="42b63-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="42b63-200">**conversationId**</span></span>| <span data-ttu-id="42b63-201">文字列</span><span class="sxs-lookup"><span data-stu-id="42b63-201">string</span></span> | <span data-ttu-id="42b63-202">はい</span><span class="sxs-lookup"><span data-stu-id="42b63-202">Yes</span></span> | <span data-ttu-id="42b63-203">会話識別子は、ボット呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-203">The conversation identifier is available as part of bot invoke.</span></span> |

#### <a name="example"></a><span data-ttu-id="42b63-204">例</span><span class="sxs-lookup"><span data-stu-id="42b63-204">Example</span></span>

<span data-ttu-id="42b63-205">`Bot ID`がマニフェストで宣言され、ボットが結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="42b63-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="42b63-206">の `completionBotId` パラメーター `externalResourceUrl` は、要求されたペイロードの例では省略可能です。</span><span class="sxs-lookup"><span data-stu-id="42b63-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="42b63-207">`Bot ID` がマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="42b63-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="42b63-208">`externalResourceUrl`幅と高さのパラメータはピクセル単位である必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="42b63-209">寸法が許可された制限内であることを確認するには、 [設計ガイドライン](design/designing-apps-in-meetings.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="42b63-210">URL は、 `<iframe>` 会議中のダイアログ ボックスに として読み込まれたページです。</span><span class="sxs-lookup"><span data-stu-id="42b63-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="42b63-211">ドメインは、アプリ マニフェストのアプリの `validDomains` 配列に含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="42b63-212">C#</span><span class="sxs-lookup"><span data-stu-id="42b63-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="42b63-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="42b63-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="42b63-214">JSON</span><span class="sxs-lookup"><span data-stu-id="42b63-214">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="42b63-215">応答コード</span><span class="sxs-lookup"><span data-stu-id="42b63-215">Response codes</span></span>

|<span data-ttu-id="42b63-216">応答コード</span><span class="sxs-lookup"><span data-stu-id="42b63-216">Response code</span></span>|<span data-ttu-id="42b63-217">説明</span><span class="sxs-lookup"><span data-stu-id="42b63-217">Description</span></span>|
|---|---|
| <span data-ttu-id="42b63-218">**201**</span><span class="sxs-lookup"><span data-stu-id="42b63-218">**201**</span></span> | <span data-ttu-id="42b63-219">シグナルのあるアクティビティは正常に送信されます。</span><span class="sxs-lookup"><span data-stu-id="42b63-219">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="42b63-220">**401**</span><span class="sxs-lookup"><span data-stu-id="42b63-220">**401**</span></span> | <span data-ttu-id="42b63-221">アプリが無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="42b63-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="42b63-222">**403**</span><span class="sxs-lookup"><span data-stu-id="42b63-222">**403**</span></span> | <span data-ttu-id="42b63-223">アプリは信号を送信できません。</span><span class="sxs-lookup"><span data-stu-id="42b63-223">The app is unable to send the signal.</span></span> <span data-ttu-id="42b63-224">これは、テナント管理者がアプリを無効にしたり、ライブ サイトの移行中にアプリがブロックされるなどのさまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="42b63-225">この場合、ペイロードには詳細なエラー メッセージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="42b63-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="42b63-226">**404**</span><span class="sxs-lookup"><span data-stu-id="42b63-226">**404**</span></span> | <span data-ttu-id="42b63-227">会議チャットが存在しません。</span><span class="sxs-lookup"><span data-stu-id="42b63-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="42b63-228">Teams会議でアプリを有効にする</span><span class="sxs-lookup"><span data-stu-id="42b63-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="42b63-229">アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="42b63-229">Update your app manifest</span></span>

<span data-ttu-id="42b63-230">会議アプリの機能は、 、、および 配列を使用してアプリ マニフェストで宣言 `configurableTabs` `scopes` `context` されます。</span><span class="sxs-lookup"><span data-stu-id="42b63-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="42b63-231">スコープは、アプリが使用可能な場所を定義するユーザーとコンテキストを定義します。</span><span class="sxs-lookup"><span data-stu-id="42b63-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="42b63-232">マニフェスト [スキーマ](../resources/schema/manifest-schema-dev-preview.md)を使用してアプリ マニフェストを更新してみてください。</span><span class="sxs-lookup"><span data-stu-id="42b63-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="42b63-233">会議のアプリには *、グループチャット* のスコープが必要です。</span><span class="sxs-lookup"><span data-stu-id="42b63-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="42b63-234">*チーム* スコープは、チャネル内のタブでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="42b63-234">The *team* scope works for tabs in channels only.</span></span>

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
> <span data-ttu-id="42b63-235">`meetingStage` は、現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="42b63-236">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="42b63-236">Context property</span></span>

<span data-ttu-id="42b63-237">タブ `context` と `scopes` プロパティを使用すると、アプリの表示場所を決定できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="42b63-238">または スコープ内のタブ `team` `groupchat` には、複数のコンテキストを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="42b63-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="42b63-239">値のすべて `context` または一部を使用できるプロパティの値を次に示します。</span><span class="sxs-lookup"><span data-stu-id="42b63-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="42b63-240">値</span><span class="sxs-lookup"><span data-stu-id="42b63-240">Value</span></span>|<span data-ttu-id="42b63-241">説明</span><span class="sxs-lookup"><span data-stu-id="42b63-241">Description</span></span>|
|---|---|
| <span data-ttu-id="42b63-242">**チャンネルタブ**</span><span class="sxs-lookup"><span data-stu-id="42b63-242">**channelTab**</span></span> | <span data-ttu-id="42b63-243">チーム チャネルのヘッダーのタブ。</span><span class="sxs-lookup"><span data-stu-id="42b63-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="42b63-244">**プライベートチャットタブ**</span><span class="sxs-lookup"><span data-stu-id="42b63-244">**privateChatTab**</span></span> | <span data-ttu-id="42b63-245">チームまたは会議のコンテキストにないユーザーのセット間のグループ チャットのヘッダーのタブ。</span><span class="sxs-lookup"><span data-stu-id="42b63-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="42b63-246">**ミーティングチャットタブ**</span><span class="sxs-lookup"><span data-stu-id="42b63-246">**meetingChatTab**</span></span> | <span data-ttu-id="42b63-247">スケジュールされた会議のコンテキストで、グループ チャットのヘッダーのタブ。</span><span class="sxs-lookup"><span data-stu-id="42b63-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="42b63-248">**会議の詳細タブ**</span><span class="sxs-lookup"><span data-stu-id="42b63-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="42b63-249">予定表の会議詳細ビューのヘッダーのタブ。</span><span class="sxs-lookup"><span data-stu-id="42b63-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="42b63-250">**ミーティングサイドパネル**</span><span class="sxs-lookup"><span data-stu-id="42b63-250">**meetingSidePanel**</span></span> | <span data-ttu-id="42b63-251">会議中のパネルは、統一されたバー(Uバー)を介して開かれました。</span><span class="sxs-lookup"><span data-stu-id="42b63-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="42b63-252">**ミーティングステージ**</span><span class="sxs-lookup"><span data-stu-id="42b63-252">**meetingStage**</span></span> | <span data-ttu-id="42b63-253">サイドパネルのアプリを会議ステージに共有できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="42b63-254">`Context` プロパティは、現在、モバイル クライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="42b63-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="42b63-255">会議シナリオ用にアプリを構成する</span><span class="sxs-lookup"><span data-stu-id="42b63-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="42b63-256">アプリをタブ ギャラリーに表示するには、構成可能なタブとグループ チャットのスコープをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="42b63-257">モバイル クライアントは、会議の前後のステージでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="42b63-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="42b63-258">会議内のダイアログ ボックスおよびタブは、現在、モバイル クライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="42b63-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="42b63-259">詳細については、 [モバイル用のタブを作成する際のモバイルの](../tabs/design/tabs-mobile.md) タブのガイダンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="42b63-260">会議の前に</span><span class="sxs-lookup"><span data-stu-id="42b63-260">Before a meeting</span></span>

<span data-ttu-id="42b63-261">会議の前に、ユーザーはタブ、ボット、およびメッセージング拡張機能を会議に追加できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="42b63-262">開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="42b63-263">**会議にタブを追加するには**</span><span class="sxs-lookup"><span data-stu-id="42b63-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="42b63-264">カレンダーで、タブを追加する会議を選択します。</span><span class="sxs-lookup"><span data-stu-id="42b63-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="42b63-265">[ **詳細** ] タブを選択し、[+ ]</span><span class="sxs-lookup"><span data-stu-id="42b63-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="42b63-266">.</span><span class="sxs-lookup"><span data-stu-id="42b63-266">.</span></span> <span data-ttu-id="42b63-267">タブ ギャラリーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="42b63-267">The tab gallery appears.</span></span>

    ![事前会議の経験](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="42b63-269">タブ ギャラリーで、追加するアプリを選択し、必要に応じて手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="42b63-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="42b63-270">アプリはタブとしてインストールされます。</span><span class="sxs-lookup"><span data-stu-id="42b63-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="42b63-271">現在、[会議] タブでは、会議の詳細と参加者の情報を取得することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="42b63-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="42b63-272">**会議にメッセージ拡張機能を追加するには**</span><span class="sxs-lookup"><span data-stu-id="42b63-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="42b63-273">チャットのメッセージ作成領域にある省略記号またはオーバーフロー メニュー &#x25CF;&#x25CF;&#x25CF; を選択します。</span><span class="sxs-lookup"><span data-stu-id="42b63-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="42b63-274">追加するアプリを選択し、必要に応じて手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="42b63-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="42b63-275">アプリは、メッセージング拡張機能としてインストールされます。</span><span class="sxs-lookup"><span data-stu-id="42b63-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="42b63-276">**会議にボットを追加するには**</span><span class="sxs-lookup"><span data-stu-id="42b63-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="42b63-277">会議チャットでキーを入力 **@** し、[ **ボットの取得**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="42b63-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="42b63-278">ユーザー ID は [、タブ SSO](../tabs/how-to/authentication/auth-aad-sso.md)を使用して確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="42b63-279">認証後、アプリは API を使用してユーザー ロールを取得できます `GetParticipant` 。</span><span class="sxs-lookup"><span data-stu-id="42b63-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="42b63-280">ユーザー ロールに基づいて、アプリはロール固有のエクスペリエンスを提供する機能を持ちます。</span><span class="sxs-lookup"><span data-stu-id="42b63-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="42b63-281">たとえば、ポーリング アプリでは、主催者と発表者のみが新しいポーリングを作成できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="42b63-282">会議の進行中にロールの割り当てを変更できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="42b63-283">詳細については、「 [Teams会議でのロール](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="42b63-284">会議中</span><span class="sxs-lookup"><span data-stu-id="42b63-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="42b63-285">サイドパネル</span><span class="sxs-lookup"><span data-stu-id="42b63-285">sidePanel</span></span>

<span data-ttu-id="42b63-286">サイドパネルを使用すると、開催者と発表者がさまざまなビューとアクションを持つことができる会議のエクスペリエンスをカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="42b63-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="42b63-287">アプリ マニフェストで、コンテキスト配列に sidePanel を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="42b63-288">会議とすべてのシナリオで、アプリは、幅 320 ピクセルの会議内タブでレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="42b63-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="42b63-289">詳細については、「 [フレーム コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-289">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="42b63-290">API を使用 `userContext` して要求をルーティングするには[、「sdk Teams」](../tabs/how-to/access-teams-context.md#user-context)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="42b63-291">[タブTeams認証フローを](../tabs/how-to/authentication/auth-flow-tab.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="42b63-292">タブの認証フローは、Web サイトの認証フローとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="42b63-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="42b63-293">したがって、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="42b63-294">[Microsoft ID プラットフォームと OAuth 2.0 の認証コード フロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="42b63-295">メッセージング拡張機能は、ユーザーが会議内ビューに表示され、ユーザーがメッセージの拡張カードを作成する投稿を行う場合に、期待どおりに動作します。</span><span class="sxs-lookup"><span data-stu-id="42b63-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="42b63-296">会議内の AppName は、会議中のアプリ名を示すツールヒントです。</span><span class="sxs-lookup"><span data-stu-id="42b63-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="42b63-297">バージョン 1.7.0 以上の[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用する前のバージョンではサイド パネルがサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="42b63-297">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="42b63-298">会議中ダイアログ</span><span class="sxs-lookup"><span data-stu-id="42b63-298">In-meeting dialog</span></span>

<span data-ttu-id="42b63-299">会議中のダイアログ ボックスを使用して、ミーティング中に参加者を参加させ、会議中に情報やフィードバックを収集できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-299">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="42b63-300">API [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) を使用して、バブル通知をトリガーする必要があることを通知します。</span><span class="sxs-lookup"><span data-stu-id="42b63-300">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="42b63-301">通知要求ペイロードの一部として、表示されるコンテンツがホストされている URL を含めます。</span><span class="sxs-lookup"><span data-stu-id="42b63-301">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="42b63-302">会議内ダイアログでは、タスク モジュールを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="42b63-302">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="42b63-303">タスク モジュールは、会議チャットでは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="42b63-303">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="42b63-304">外部リソース URL は、会議でコンテンツ バブルを表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="42b63-304">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="42b63-305">このメソッドを使用 `submitTask` して、会議チャットでデータを送信できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-305">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="42b63-306">ユーザーが Web ビューでアクションを実行した後に自動的に終了するには [、submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-306">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="42b63-307">これはアプリの申請に必要な要件です。</span><span class="sxs-lookup"><span data-stu-id="42b63-307">This is a requirement for app submission.</span></span> <span data-ttu-id="42b63-308">詳細については、「 [SDK タスク モジュールTeams」](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-308">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="42b63-309">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、 `from.id` `from` 要求メタデータではなく、オブジェクト内の要求メタデータに依存する必要があります `from.aadObjectId` 。</span><span class="sxs-lookup"><span data-stu-id="42b63-309">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="42b63-310">`from.id`はユーザー ID であり `from.aadObjectId` 、ユーザーの Azure Active Directory (AAD) ID です。</span><span class="sxs-lookup"><span data-stu-id="42b63-310">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="42b63-311">詳細については、 [タブでのタスクモジュールの使用](../task-modules-and-cards/task-modules/task-modules-tabs.md) および [タスクモジュールの作成と送信を](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)参照してください。</span><span class="sxs-lookup"><span data-stu-id="42b63-311">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="42b63-312">ステージ間で共有</span><span class="sxs-lookup"><span data-stu-id="42b63-312">Share to stage</span></span> 

> [!NOTE]
> * <span data-ttu-id="42b63-313">この機能は、現在、開発者プレビューでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-313">This capability is currently available in developer preview only.</span></span>
> * <span data-ttu-id="42b63-314">この機能を使用するには、アプリがミーティング中のサイドパネルをサポートしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="42b63-314">To use this feature, the app must support an in-meeting sidepanel.</span></span>


<span data-ttu-id="42b63-315">この機能により、開発者は会議の段階でアプリを共有できます。</span><span class="sxs-lookup"><span data-stu-id="42b63-315">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="42b63-316">ミーティングのステージで共有を有効にすると、ミーティング参加者はリアルタイムで共同作業を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="42b63-316">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="42b63-317">必要なコンテキストは `meetingStage` 、アプリ マニフェストにあります。</span><span class="sxs-lookup"><span data-stu-id="42b63-317">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="42b63-318">この場合の前提条件は、コンテキストを持つ `meetingSidePanel` ためです。</span><span class="sxs-lookup"><span data-stu-id="42b63-318">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="42b63-319">これにより、次の図に示すように、サイドパネルの **[共有** ] ボタンが有効になります。</span><span class="sxs-lookup"><span data-stu-id="42b63-319">This enables the **Share** button in the sidepanel as depecited in the following image:</span></span>

  ![share_to_stage_during_meeting経験](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="42b63-321">この機能を有効にするために必要なマニフェストの変更は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="42b63-321">The manifest change that is needed to enable this capability is as follows:</span></span> 

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



### <a name="after-a-meeting"></a><span data-ttu-id="42b63-322">会議の後</span><span class="sxs-lookup"><span data-stu-id="42b63-322">After a meeting</span></span>

<span data-ttu-id="42b63-323">会議後と会議前の構成は同じです。</span><span class="sxs-lookup"><span data-stu-id="42b63-323">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="42b63-324">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="42b63-324">Code sample</span></span>

|<span data-ttu-id="42b63-325">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="42b63-325">Sample name</span></span> | <span data-ttu-id="42b63-326">説明</span><span class="sxs-lookup"><span data-stu-id="42b63-326">Description</span></span> | <span data-ttu-id="42b63-327">.NET</span><span class="sxs-lookup"><span data-stu-id="42b63-327">.NET</span></span> | <span data-ttu-id="42b63-328">Node.js</span><span class="sxs-lookup"><span data-stu-id="42b63-328">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="42b63-329">会議の機能拡張</span><span class="sxs-lookup"><span data-stu-id="42b63-329">Meetings extensibility</span></span> | <span data-ttu-id="42b63-330">トークンを渡すための会議の機能拡張サンプルをMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="42b63-330">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="42b63-331">View</span><span class="sxs-lookup"><span data-stu-id="42b63-331">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="42b63-332">View</span><span class="sxs-lookup"><span data-stu-id="42b63-332">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="42b63-333">ミーティング コンテンツ バブル ボット</span><span class="sxs-lookup"><span data-stu-id="42b63-333">Meeting content bubble bot</span></span> | <span data-ttu-id="42b63-334">Microsoft Teams会議でコンテンツ バブル ボットと対話するための会議機能拡張サンプルです。</span><span class="sxs-lookup"><span data-stu-id="42b63-334">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="42b63-335">View</span><span class="sxs-lookup"><span data-stu-id="42b63-335">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="42b63-336">View</span><span class="sxs-lookup"><span data-stu-id="42b63-336">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="42b63-337">ミーティングサイドパネル</span><span class="sxs-lookup"><span data-stu-id="42b63-337">Meeting SidePanel</span></span> | <span data-ttu-id="42b63-338">Microsoft Teams会議中のサイド パネルで反復処理を行うための会議の機能拡張サンプルです。</span><span class="sxs-lookup"><span data-stu-id="42b63-338">Microsoft Teams meeting extensibility sample for iteracting with the side panel in-meeting.</span></span> | [<span data-ttu-id="42b63-339">View</span><span class="sxs-lookup"><span data-stu-id="42b63-339">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a><span data-ttu-id="42b63-340">関連項目</span><span class="sxs-lookup"><span data-stu-id="42b63-340">See also</span></span>

* [<span data-ttu-id="42b63-341">会議中のダイアログデザインガイドライン</span><span class="sxs-lookup"><span data-stu-id="42b63-341">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="42b63-342">タブのTeams認証フロー</span><span class="sxs-lookup"><span data-stu-id="42b63-342">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
