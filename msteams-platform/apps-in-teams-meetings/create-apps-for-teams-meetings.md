---
title: Teams 会議アプリへの前提条件と API リファレンス
author: surbhigupta
description: 会議のアプリをTeamsする
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: e6d1c442f77f4d271c43d866c819d65697262b6b
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068563"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="f3c43-104">Teams 会議アプリへの前提条件と API リファレンス</span><span class="sxs-lookup"><span data-stu-id="f3c43-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="f3c43-105">会議のライフサイクル全体にわたってアプリの機能を拡張するには、Teams会議用のアプリTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="f3c43-106">前提条件を確認し、会議アプリ API 参照を使用して会議のエクスペリエンスを向上させる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3c43-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="f3c43-107">Prerequisites</span></span>

<span data-ttu-id="f3c43-108">会議のアプリをTeams前に、次の情報を理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="f3c43-109">アプリを開発する方法に関する知識Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="f3c43-110">詳細については、「アプリ開発の[Teams」を参照してください](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f3c43-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="f3c43-111">アプリが会議でTeamsを示すために、アプリ マニフェストを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="f3c43-112">詳細については、「アプリ マニフェスト [」を参照してください](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="f3c43-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="f3c43-113">アプリが会議のライフサイクルでタブとして機能するには、アプリが groupchat スコープで構成可能なタブをサポートしている必要があります。詳細については[、「groupchat スコープ」を参照し、](../resources/schema/manifest-schema.md#configurabletabs)[グループ タブを作成するを参照してください](../build-your-first-app/build-channel-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="f3c43-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="f3c43-114">会議前および会議後のシナリオTeams一般的なタブデザインガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="f3c43-115">会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f3c43-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="f3c43-116">詳細については、「[タブデザイン](../tabs/design/tabs.md)Teams、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)および会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="f3c43-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="f3c43-117">会議前および会議後のチャットでアプリを有効にするには、この `groupchat` 範囲をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="f3c43-118">会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="f3c43-119">会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果やフィードバックなど、会議の結果を表示できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="f3c43-120">会議 API の URL パラメーターには、、 `meetingId` 、 `userId` および を指定する必要があります `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="f3c43-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="f3c43-121">これらは、クライアント SDK およびボット アクティビティTeams使用できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="f3c43-122">さらに、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="f3c43-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="f3c43-123">認証 `GetParticipant` トークンを生成するには、API にボット登録と ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="f3c43-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="f3c43-124">詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="f3c43-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="f3c43-125">アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="f3c43-126">これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="f3c43-127">[会議内] ダイアログ ボックスについては、「API の完了 `bot Id` パラメーター」を参照 `NotificationSignal` してください。</span><span class="sxs-lookup"><span data-stu-id="f3c43-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

<span data-ttu-id="f3c43-128">前提条件を満たした後、会議アプリ API 参照を使用して、属性を使用して情報にアクセスし、関連するコンテンツ `GetUserContext` `GetParticipant` `NotificationSignal` を表示できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-128">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, and `NotificationSignal` that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="f3c43-129">会議アプリ API の参照</span><span class="sxs-lookup"><span data-stu-id="f3c43-129">Meeting apps API references</span></span>

<span data-ttu-id="f3c43-130">新しい会議の機能は、会議のエクスペリエンスを変革する API を提供します。</span><span class="sxs-lookup"><span data-stu-id="f3c43-130">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="f3c43-131">この新しい機能を使用すると、会議のライフサイクル内でアプリを構築したり、既存のアプリを統合することができます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-131">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="f3c43-132">API を使用すると、アプリで会議を認識できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-132">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="f3c43-133">会議のエクスペリエンスを強化するために使用する API を選択できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-133">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="f3c43-134">次の表に、これらの API の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="f3c43-134">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="f3c43-135">API</span><span class="sxs-lookup"><span data-stu-id="f3c43-135">API</span></span>|<span data-ttu-id="f3c43-136">説明</span><span class="sxs-lookup"><span data-stu-id="f3c43-136">Description</span></span>|<span data-ttu-id="f3c43-137">要求</span><span class="sxs-lookup"><span data-stu-id="f3c43-137">Request</span></span>|<span data-ttu-id="f3c43-138">ソース</span><span class="sxs-lookup"><span data-stu-id="f3c43-138">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="f3c43-139">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="f3c43-139">**GetUserContext**</span></span>| <span data-ttu-id="f3c43-140">この API を使用すると、コンテキスト情報を取得して、関連するコンテンツを [コンテンツ] タブTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-140">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="f3c43-141">_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="f3c43-141">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="f3c43-142">Microsoft Teamsクライアント SDK</span><span class="sxs-lookup"><span data-stu-id="f3c43-142">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="f3c43-143">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="f3c43-143">**GetParticipant**</span></span>| <span data-ttu-id="f3c43-144">この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-144">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="f3c43-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="f3c43-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="f3c43-146">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="f3c43-146">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="f3c43-147">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="f3c43-147">**NotificationSignal**</span></span> | <span data-ttu-id="f3c43-148">この API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-148">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="f3c43-149">これにより、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-149">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="f3c43-150">**POST** _**/v3/conversation/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="f3c43-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="f3c43-151">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="f3c43-151">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext-api"></a><span data-ttu-id="f3c43-152">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="f3c43-152">GetUserContext API</span></span>

<span data-ttu-id="f3c43-153">タブ コンテンツのコンテキスト情報を特定して取得するには[、「get context for your Teams タブ」を参照してください](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`は、会議コンテキストで実行するときにタブで使用され、応答ペイロードに追加されます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-153">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="f3c43-154">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="f3c43-154">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="f3c43-155">会議の開催者がいつでも役割を変更できるので、参加者の役割をキャッシュしない。</span><span class="sxs-lookup"><span data-stu-id="f3c43-155">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="f3c43-156">Teams現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズはサポート `GetParticipant` されていません。</span><span class="sxs-lookup"><span data-stu-id="f3c43-156">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="f3c43-157">API `GetParticipant` を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-157">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="f3c43-158">API には、クエリ パラメーター、例、および応答コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-158">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="f3c43-159">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="f3c43-159">Query parameters</span></span>

<span data-ttu-id="f3c43-160">`GetParticipant`API には、次のクエリ パラメーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-160">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="f3c43-161">値</span><span class="sxs-lookup"><span data-stu-id="f3c43-161">Value</span></span>|<span data-ttu-id="f3c43-162">型</span><span class="sxs-lookup"><span data-stu-id="f3c43-162">Type</span></span>|<span data-ttu-id="f3c43-163">必須</span><span class="sxs-lookup"><span data-stu-id="f3c43-163">Required</span></span>|<span data-ttu-id="f3c43-164">説明</span><span class="sxs-lookup"><span data-stu-id="f3c43-164">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="f3c43-165">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="f3c43-165">**meetingId**</span></span>| <span data-ttu-id="f3c43-166">String</span><span class="sxs-lookup"><span data-stu-id="f3c43-166">String</span></span> | <span data-ttu-id="f3c43-167">はい</span><span class="sxs-lookup"><span data-stu-id="f3c43-167">Yes</span></span> | <span data-ttu-id="f3c43-168">会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-168">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="f3c43-169">**participantId**</span><span class="sxs-lookup"><span data-stu-id="f3c43-169">**participantId**</span></span>| <span data-ttu-id="f3c43-170">String</span><span class="sxs-lookup"><span data-stu-id="f3c43-170">String</span></span> | <span data-ttu-id="f3c43-171">はい</span><span class="sxs-lookup"><span data-stu-id="f3c43-171">Yes</span></span> | <span data-ttu-id="f3c43-172">参加者 ID はユーザー ID です。</span><span class="sxs-lookup"><span data-stu-id="f3c43-172">The participant ID is the user ID.</span></span> <span data-ttu-id="f3c43-173">これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-173">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="f3c43-174">Tab SSO から参加者 ID を取得する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f3c43-174">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="f3c43-175">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="f3c43-175">**tenantId**</span></span>| <span data-ttu-id="f3c43-176">String</span><span class="sxs-lookup"><span data-stu-id="f3c43-176">String</span></span> | <span data-ttu-id="f3c43-177">はい</span><span class="sxs-lookup"><span data-stu-id="f3c43-177">Yes</span></span> | <span data-ttu-id="f3c43-178">テナントユーザーにはテナント ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="f3c43-178">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="f3c43-179">これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-179">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="f3c43-180">Tab SSO からテナント ID を取得する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f3c43-180">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="f3c43-181">例</span><span class="sxs-lookup"><span data-stu-id="f3c43-181">Example</span></span>

<span data-ttu-id="f3c43-182">`GetParticipant`API には、次の例が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-182">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="f3c43-183">C#</span><span class="sxs-lookup"><span data-stu-id="f3c43-183">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="f3c43-184">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f3c43-184">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f3c43-185">JSON</span><span class="sxs-lookup"><span data-stu-id="f3c43-185">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="f3c43-186">API の JSON 応答 `GetParticipant` 本文は次の形式です。</span><span class="sxs-lookup"><span data-stu-id="f3c43-186">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="f3c43-187">応答コード</span><span class="sxs-lookup"><span data-stu-id="f3c43-187">Response codes</span></span>

<span data-ttu-id="f3c43-188">`GetParticipant`API には、次の応答コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-188">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="f3c43-189">応答コード</span><span class="sxs-lookup"><span data-stu-id="f3c43-189">Response code</span></span>|<span data-ttu-id="f3c43-190">説明</span><span class="sxs-lookup"><span data-stu-id="f3c43-190">Description</span></span>|
|---|---|
| <span data-ttu-id="f3c43-191">**403**</span><span class="sxs-lookup"><span data-stu-id="f3c43-191">**403**</span></span> | <span data-ttu-id="f3c43-192">アプリは参加者情報の取得を許可されません。</span><span class="sxs-lookup"><span data-stu-id="f3c43-192">The app is not allowed to get participant information.</span></span> <span data-ttu-id="f3c43-193">これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-193">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="f3c43-194">たとえば、テナント管理者によってアプリが無効になっている場合や、ライブ サイトの移行中にブロックされている場合などです。</span><span class="sxs-lookup"><span data-stu-id="f3c43-194">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="f3c43-195">**200**</span><span class="sxs-lookup"><span data-stu-id="f3c43-195">**200**</span></span> | <span data-ttu-id="f3c43-196">参加者情報が正常に取得されます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-196">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="f3c43-197">**401**</span><span class="sxs-lookup"><span data-stu-id="f3c43-197">**401**</span></span> | <span data-ttu-id="f3c43-198">アプリは無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="f3c43-198">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="f3c43-199">**404**</span><span class="sxs-lookup"><span data-stu-id="f3c43-199">**404**</span></span> | <span data-ttu-id="f3c43-200">会議の有効期限が切れているか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="f3c43-200">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="f3c43-201">**500**</span><span class="sxs-lookup"><span data-stu-id="f3c43-201">**500**</span></span> | <span data-ttu-id="f3c43-202">会議が終了した後、会議の有効期限が切れている (60 日を超える) か、参加者が自分の役割に基づいてアクセス許可を持っていません。</span><span class="sxs-lookup"><span data-stu-id="f3c43-202">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="f3c43-203">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="f3c43-203">NotificationSignal API</span></span>

<span data-ttu-id="f3c43-204">会議のすべてのユーザーは、API を介して送信された通知を受け取 `NotificationSignal` る。</span><span class="sxs-lookup"><span data-stu-id="f3c43-204">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="f3c43-205">会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-205">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="f3c43-206">現在、ターゲット通知の送信はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f3c43-206">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="f3c43-207">`NotificationSignal` API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-207">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="f3c43-208">この API を使用すると、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-208">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="f3c43-209">API には、クエリ パラメーター、例、および応答コードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-209">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="f3c43-210">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="f3c43-210">Query parameter</span></span>

<span data-ttu-id="f3c43-211">`NotificationSignal`API には、次のクエリ パラメーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-211">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="f3c43-212">値</span><span class="sxs-lookup"><span data-stu-id="f3c43-212">Value</span></span>|<span data-ttu-id="f3c43-213">型</span><span class="sxs-lookup"><span data-stu-id="f3c43-213">Type</span></span>|<span data-ttu-id="f3c43-214">必須</span><span class="sxs-lookup"><span data-stu-id="f3c43-214">Required</span></span>|<span data-ttu-id="f3c43-215">説明</span><span class="sxs-lookup"><span data-stu-id="f3c43-215">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="f3c43-216">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="f3c43-216">**conversationId**</span></span>| <span data-ttu-id="f3c43-217">String</span><span class="sxs-lookup"><span data-stu-id="f3c43-217">String</span></span> | <span data-ttu-id="f3c43-218">はい</span><span class="sxs-lookup"><span data-stu-id="f3c43-218">Yes</span></span> | <span data-ttu-id="f3c43-219">会話識別子は、ボット呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-219">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="f3c43-220">例</span><span class="sxs-lookup"><span data-stu-id="f3c43-220">Examples</span></span>

<span data-ttu-id="f3c43-221">は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-221">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="f3c43-222">要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、the のパラメーターは省略可能です。</span><span class="sxs-lookup"><span data-stu-id="f3c43-222">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="f3c43-223">`Bot ID` はマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-223">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="f3c43-224">幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-224">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="f3c43-225">寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="f3c43-225">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="f3c43-226">URL は、会議中のダイアログ ボックスに表示 `<iframe>` されるページです。</span><span class="sxs-lookup"><span data-stu-id="f3c43-226">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="f3c43-227">ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-227">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="f3c43-228">`NotificationSignal`API には、次の例が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-228">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="f3c43-229">C#</span><span class="sxs-lookup"><span data-stu-id="f3c43-229">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="f3c43-230">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f3c43-230">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f3c43-231">JSON</span><span class="sxs-lookup"><span data-stu-id="f3c43-231">JSON</span></span>](#tab/json)

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

---

#### <a name="response-codes"></a><span data-ttu-id="f3c43-232">応答コード</span><span class="sxs-lookup"><span data-stu-id="f3c43-232">Response codes</span></span>

<span data-ttu-id="f3c43-233">`NotificationSignal`API には、次の応答コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-233">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="f3c43-234">応答コード</span><span class="sxs-lookup"><span data-stu-id="f3c43-234">Response code</span></span>|<span data-ttu-id="f3c43-235">説明</span><span class="sxs-lookup"><span data-stu-id="f3c43-235">Description</span></span>|
|---|---|
| <span data-ttu-id="f3c43-236">**201**</span><span class="sxs-lookup"><span data-stu-id="f3c43-236">**201**</span></span> | <span data-ttu-id="f3c43-237">シグナルを含むアクティビティが正常に送信されます。</span><span class="sxs-lookup"><span data-stu-id="f3c43-237">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="f3c43-238">**401**</span><span class="sxs-lookup"><span data-stu-id="f3c43-238">**401**</span></span> | <span data-ttu-id="f3c43-239">アプリは無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="f3c43-239">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="f3c43-240">**403**</span><span class="sxs-lookup"><span data-stu-id="f3c43-240">**403**</span></span> | <span data-ttu-id="f3c43-241">アプリは信号を送信できません。</span><span class="sxs-lookup"><span data-stu-id="f3c43-241">The app is unable to send the signal.</span></span> <span data-ttu-id="f3c43-242">これは、テナント管理者がアプリを無効にし、アプリがライブ サイトの移行中にブロックされるなど、さまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f3c43-242">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="f3c43-243">この場合、ペイロードには詳細なエラー メッセージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c43-243">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="f3c43-244">**404**</span><span class="sxs-lookup"><span data-stu-id="f3c43-244">**404**</span></span> | <span data-ttu-id="f3c43-245">会議チャットが存在しません。</span><span class="sxs-lookup"><span data-stu-id="f3c43-245">The meeting chat does not exist.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="f3c43-246">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="f3c43-246">Code sample</span></span>

|<span data-ttu-id="f3c43-247">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="f3c43-247">Sample name</span></span> | <span data-ttu-id="f3c43-248">説明</span><span class="sxs-lookup"><span data-stu-id="f3c43-248">Description</span></span> | <span data-ttu-id="f3c43-249">.NET</span><span class="sxs-lookup"><span data-stu-id="f3c43-249">.NET</span></span> | <span data-ttu-id="f3c43-250">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3c43-250">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="f3c43-251">会議の機能拡張</span><span class="sxs-lookup"><span data-stu-id="f3c43-251">Meetings extensibility</span></span> | <span data-ttu-id="f3c43-252">Microsoft Teams渡しに関する会議機能拡張サンプル。</span><span class="sxs-lookup"><span data-stu-id="f3c43-252">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="f3c43-253">View</span><span class="sxs-lookup"><span data-stu-id="f3c43-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="f3c43-254">View</span><span class="sxs-lookup"><span data-stu-id="f3c43-254">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="f3c43-255">会議コンテンツ バブル ボット</span><span class="sxs-lookup"><span data-stu-id="f3c43-255">Meeting content bubble bot</span></span> | <span data-ttu-id="f3c43-256">Microsoft Teamsでコンテンツ バブル ボットを操作するための会議機能拡張サンプルを作成します。</span><span class="sxs-lookup"><span data-stu-id="f3c43-256">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="f3c43-257">View</span><span class="sxs-lookup"><span data-stu-id="f3c43-257">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="f3c43-258">View</span><span class="sxs-lookup"><span data-stu-id="f3c43-258">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="f3c43-259">MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="f3c43-259">Meeting meetingSidePanel</span></span> | <span data-ttu-id="f3c43-260">Microsoft Teamsのサイド パネルを操作するための会議機能拡張サンプルを作成します。</span><span class="sxs-lookup"><span data-stu-id="f3c43-260">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="f3c43-261">View</span><span class="sxs-lookup"><span data-stu-id="f3c43-261">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="f3c43-262">View</span><span class="sxs-lookup"><span data-stu-id="f3c43-262">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|

## <a name="see-also"></a><span data-ttu-id="f3c43-263">関連項目</span><span class="sxs-lookup"><span data-stu-id="f3c43-263">See also</span></span>

* [<span data-ttu-id="f3c43-264">会議中のダイアログの設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="f3c43-264">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="f3c43-265">Teamsの認証フロー</span><span class="sxs-lookup"><span data-stu-id="f3c43-265">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="f3c43-266">会議のTeamsアプリ</span><span class="sxs-lookup"><span data-stu-id="f3c43-266">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="f3c43-267">次の手順</span><span class="sxs-lookup"><span data-stu-id="f3c43-267">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3c43-268">会議で使用するアプリを有効Teamsする</span><span class="sxs-lookup"><span data-stu-id="f3c43-268">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
