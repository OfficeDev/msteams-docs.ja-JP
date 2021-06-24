---
title: Teams 会議アプリへの前提条件と API リファレンス
author: surbhigupta
description: 会議のアプリをTeamsする
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 6a773720f55f2b4e0aeb3a61bfdbde63a775abb8
ms.sourcegitcommit: 4ac93d69927791a8ccf678ca5ee83e63b51566b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2021
ms.locfileid: "53095508"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="1d2ec-104">Teams 会議アプリへの前提条件と API リファレンス</span><span class="sxs-lookup"><span data-stu-id="1d2ec-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="1d2ec-105">会議のライフサイクル全体にわたってアプリの機能を拡張するには、Teams会議用のアプリTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="1d2ec-106">前提条件を確認し、会議アプリ API 参照を使用して会議のエクスペリエンスを向上させる必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d2ec-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="1d2ec-107">Prerequisites</span></span>

<span data-ttu-id="1d2ec-108">会議のアプリをTeams前に、次の情報を理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="1d2ec-109">アプリを開発する方法に関する知識Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="1d2ec-110">詳細については、「アプリ開発の[Teams」を参照してください](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="1d2ec-111">アプリが会議でTeamsを示すために、アプリ マニフェストを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="1d2ec-112">詳細については、「アプリ マニフェスト [」を参照してください](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="1d2ec-113">アプリが会議のライフサイクルでタブとして機能するには、アプリが groupchat スコープで構成可能なタブをサポートしている必要があります。詳細については[、「groupchat スコープ」を参照し、](../resources/schema/manifest-schema.md#configurabletabs)[グループ タブを作成するを参照してください](../build-your-first-app/build-channel-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="1d2ec-114">会議前および会議後のシナリオTeams一般的なタブデザインガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="1d2ec-115">会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="1d2ec-116">詳細については、「[タブデザイン](../tabs/design/tabs.md)Teams、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)および会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="1d2ec-117">会議前および会議後のチャットでアプリを有効にするには、この `groupchat` 範囲をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="1d2ec-118">会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="1d2ec-119">会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果やフィードバックなど、会議の結果を表示できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="1d2ec-120">会議 API の URL パラメーターには、、 `meetingId` 、 `userId` および を指定する必要があります `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="1d2ec-121">これらは、クライアント SDK およびボット アクティビティTeams使用できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="1d2ec-122">さらに、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="1d2ec-123">認証 `GetParticipant` トークンを生成するには、API にボット登録と ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="1d2ec-124">詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="1d2ec-125">アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="1d2ec-126">これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="1d2ec-127">[会議内] ダイアログ ボックスについては、「API の完了 `bot Id` パラメーター」を参照 `NotificationSignal` してください。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

* <span data-ttu-id="1d2ec-128">会議の詳細 API には、ボット登録とボット ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-128">Meeting Details API must have a bot registration and bot ID.</span></span> <span data-ttu-id="1d2ec-129">ボット SDK を取得する必要があります `TurnContext` 。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-129">It requires Bot SDK to get `TurnContext`.</span></span>

* <span data-ttu-id="1d2ec-130">リアルタイムの会議イベントの場合は、ボット SDK で使用できる `TurnContext` オブジェクトに精通している必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-130">For real-time meeting events, you must be familiar with the `TurnContext` object available through the Bot SDK.</span></span> <span data-ttu-id="1d2ec-131">オブジェクト `Activity` には、 `TurnContext` 実際の開始時刻と終了時刻を含むペイロードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-131">The `Activity` object in `TurnContext` contains the payload with the actual start and end time.</span></span> <span data-ttu-id="1d2ec-132">リアルタイム会議イベントでは、会議プラットフォームから登録済みのボット ID がTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-132">Real-time meeting events require a registered bot ID from the Teams platform.</span></span>

<span data-ttu-id="1d2ec-133">前提条件を満たした後、会議アプリ API リファレンス 、、および会議の詳細 API を使用して、属性を使用して情報にアクセスし、関連するコンテンツ `GetUserContext` `GetParticipant` `NotificationSignal` を表示できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-133">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, `NotificationSignal`, and Meeting Details API that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="1d2ec-134">会議アプリ API の参照</span><span class="sxs-lookup"><span data-stu-id="1d2ec-134">Meeting apps API references</span></span>

<span data-ttu-id="1d2ec-135">新しい会議の機能は、会議のエクスペリエンスを変革する API を提供します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-135">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="1d2ec-136">この新しい機能を使用すると、会議のライフサイクル内でアプリを構築したり、既存のアプリを統合することができます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-136">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="1d2ec-137">API を使用すると、アプリで会議を認識できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-137">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="1d2ec-138">会議のエクスペリエンスを強化するために使用する API を選択できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-138">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="1d2ec-139">次の表に、これらの API の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-139">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="1d2ec-140">API</span><span class="sxs-lookup"><span data-stu-id="1d2ec-140">API</span></span>|<span data-ttu-id="1d2ec-141">説明</span><span class="sxs-lookup"><span data-stu-id="1d2ec-141">Description</span></span>|<span data-ttu-id="1d2ec-142">要求</span><span class="sxs-lookup"><span data-stu-id="1d2ec-142">Request</span></span>|<span data-ttu-id="1d2ec-143">ソース</span><span class="sxs-lookup"><span data-stu-id="1d2ec-143">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="1d2ec-144">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-144">**GetUserContext**</span></span>| <span data-ttu-id="1d2ec-145">この API を使用すると、コンテキスト情報を取得して、関連するコンテンツを [コンテンツ] タブTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-145">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="1d2ec-146">_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="1d2ec-146">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="1d2ec-147">Microsoft Teamsクライアント SDK</span><span class="sxs-lookup"><span data-stu-id="1d2ec-147">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="1d2ec-148">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-148">**GetParticipant**</span></span>| <span data-ttu-id="1d2ec-149">この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-149">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="1d2ec-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="1d2ec-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="1d2ec-151">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="1d2ec-151">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="1d2ec-152">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-152">**NotificationSignal**</span></span> | <span data-ttu-id="1d2ec-153">この API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-153">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="1d2ec-154">これにより、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-154">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="1d2ec-155">**POST** _**/v3/conversation/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="1d2ec-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="1d2ec-156">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="1d2ec-156">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="1d2ec-157">**会議の詳細**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-157">**Meeting Details**</span></span> | <span data-ttu-id="1d2ec-158">この API を使用すると、静的な会議のメタデータを取得できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-158">This API enables you to get static meeting metadata.</span></span> |<span data-ttu-id="1d2ec-159">**GET** _**/v1/meetings/{meetingId}**_</span><span class="sxs-lookup"><span data-stu-id="1d2ec-159">**GET** _**/v1/meetings/{meetingId}**_</span></span>| <span data-ttu-id="1d2ec-160">ボット SDK</span><span class="sxs-lookup"><span data-stu-id="1d2ec-160">Bot SDK</span></span> |

### <a name="getusercontext-api"></a><span data-ttu-id="1d2ec-161">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="1d2ec-161">GetUserContext API</span></span>

<span data-ttu-id="1d2ec-162">タブ コンテンツのコンテキスト情報を特定して取得するには[、「get context for your Teams タブ」を参照してください](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`は、会議コンテキストで実行するときにタブで使用され、応答ペイロードに追加されます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-162">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="1d2ec-163">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="1d2ec-163">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="1d2ec-164">会議の開催者がいつでも役割を変更できるので、参加者の役割をキャッシュしない。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-164">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="1d2ec-165">Teams現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズはサポート `GetParticipant` されていません。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-165">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="1d2ec-166">API `GetParticipant` を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-166">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="1d2ec-167">API には、クエリ パラメーター、例、および応答コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-167">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="1d2ec-168">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="1d2ec-168">Query parameters</span></span>

<span data-ttu-id="1d2ec-169">`GetParticipant`API には、次のクエリ パラメーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-169">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="1d2ec-170">値</span><span class="sxs-lookup"><span data-stu-id="1d2ec-170">Value</span></span>|<span data-ttu-id="1d2ec-171">型</span><span class="sxs-lookup"><span data-stu-id="1d2ec-171">Type</span></span>|<span data-ttu-id="1d2ec-172">必須</span><span class="sxs-lookup"><span data-stu-id="1d2ec-172">Required</span></span>|<span data-ttu-id="1d2ec-173">説明</span><span class="sxs-lookup"><span data-stu-id="1d2ec-173">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="1d2ec-174">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-174">**meetingId**</span></span>| <span data-ttu-id="1d2ec-175">String</span><span class="sxs-lookup"><span data-stu-id="1d2ec-175">String</span></span> | <span data-ttu-id="1d2ec-176">はい</span><span class="sxs-lookup"><span data-stu-id="1d2ec-176">Yes</span></span> | <span data-ttu-id="1d2ec-177">会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-177">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="1d2ec-178">**participantId**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-178">**participantId**</span></span>| <span data-ttu-id="1d2ec-179">String</span><span class="sxs-lookup"><span data-stu-id="1d2ec-179">String</span></span> | <span data-ttu-id="1d2ec-180">はい</span><span class="sxs-lookup"><span data-stu-id="1d2ec-180">Yes</span></span> | <span data-ttu-id="1d2ec-181">参加者 ID はユーザー ID です。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-181">The participant ID is the user ID.</span></span> <span data-ttu-id="1d2ec-182">これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-182">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="1d2ec-183">Tab SSO から参加者 ID を取得する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-183">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="1d2ec-184">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-184">**tenantId**</span></span>| <span data-ttu-id="1d2ec-185">String</span><span class="sxs-lookup"><span data-stu-id="1d2ec-185">String</span></span> | <span data-ttu-id="1d2ec-186">はい</span><span class="sxs-lookup"><span data-stu-id="1d2ec-186">Yes</span></span> | <span data-ttu-id="1d2ec-187">テナントユーザーにはテナント ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-187">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="1d2ec-188">これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-188">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="1d2ec-189">Tab SSO からテナント ID を取得する方法をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-189">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="1d2ec-190">例</span><span class="sxs-lookup"><span data-stu-id="1d2ec-190">Example</span></span>

<span data-ttu-id="1d2ec-191">`GetParticipant`API には、次の例が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-191">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="1d2ec-192">C#</span><span class="sxs-lookup"><span data-stu-id="1d2ec-192">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="1d2ec-193">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d2ec-193">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="1d2ec-194">JSON</span><span class="sxs-lookup"><span data-stu-id="1d2ec-194">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="1d2ec-195">API の JSON 応答 `GetParticipant` 本文は次の形式です。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-195">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="1d2ec-196">応答コード</span><span class="sxs-lookup"><span data-stu-id="1d2ec-196">Response codes</span></span>

<span data-ttu-id="1d2ec-197">`GetParticipant`API には、次の応答コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-197">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="1d2ec-198">応答コード</span><span class="sxs-lookup"><span data-stu-id="1d2ec-198">Response code</span></span>|<span data-ttu-id="1d2ec-199">説明</span><span class="sxs-lookup"><span data-stu-id="1d2ec-199">Description</span></span>|
|---|---|
| <span data-ttu-id="1d2ec-200">**403**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-200">**403**</span></span> | <span data-ttu-id="1d2ec-201">アプリは参加者情報の取得を許可されません。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-201">The app is not allowed to get participant information.</span></span> <span data-ttu-id="1d2ec-202">これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-202">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="1d2ec-203">たとえば、テナント管理者によってアプリが無効になっている場合や、ライブ サイトの移行中にブロックされている場合などです。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-203">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="1d2ec-204">**200**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-204">**200**</span></span> | <span data-ttu-id="1d2ec-205">参加者情報が正常に取得されます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-205">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="1d2ec-206">**401**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-206">**401**</span></span> | <span data-ttu-id="1d2ec-207">アプリは無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-207">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="1d2ec-208">**404**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-208">**404**</span></span> | <span data-ttu-id="1d2ec-209">会議の有効期限が切れているか、参加者が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-209">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="1d2ec-210">**500**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-210">**500**</span></span> | <span data-ttu-id="1d2ec-211">会議が終了した後、会議の有効期限が切れている (60 日を超える) か、参加者が自分の役割に基づいてアクセス許可を持っていません。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-211">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="1d2ec-212">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="1d2ec-212">NotificationSignal API</span></span>

<span data-ttu-id="1d2ec-213">会議のすべてのユーザーは、API を介して送信された通知を受け取 `NotificationSignal` る。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-213">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="1d2ec-214">会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-214">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="1d2ec-215">現在、ターゲット通知の送信はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-215">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="1d2ec-216">`NotificationSignal` API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-216">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="1d2ec-217">この API を使用すると、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-217">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="1d2ec-218">API には、クエリ パラメーター、例、および応答コードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-218">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="1d2ec-219">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="1d2ec-219">Query parameter</span></span>

<span data-ttu-id="1d2ec-220">`NotificationSignal`API には、次のクエリ パラメーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-220">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="1d2ec-221">値</span><span class="sxs-lookup"><span data-stu-id="1d2ec-221">Value</span></span>|<span data-ttu-id="1d2ec-222">型</span><span class="sxs-lookup"><span data-stu-id="1d2ec-222">Type</span></span>|<span data-ttu-id="1d2ec-223">必須</span><span class="sxs-lookup"><span data-stu-id="1d2ec-223">Required</span></span>|<span data-ttu-id="1d2ec-224">説明</span><span class="sxs-lookup"><span data-stu-id="1d2ec-224">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="1d2ec-225">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-225">**conversationId**</span></span>| <span data-ttu-id="1d2ec-226">String</span><span class="sxs-lookup"><span data-stu-id="1d2ec-226">String</span></span> | <span data-ttu-id="1d2ec-227">はい</span><span class="sxs-lookup"><span data-stu-id="1d2ec-227">Yes</span></span> | <span data-ttu-id="1d2ec-228">会話識別子は、ボット呼び出しの一部として使用できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-228">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="1d2ec-229">例</span><span class="sxs-lookup"><span data-stu-id="1d2ec-229">Examples</span></span>

<span data-ttu-id="1d2ec-230">は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-230">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="1d2ec-231">要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、the のパラメーターは省略可能です。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-231">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="1d2ec-232">`Bot ID` はマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-232">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="1d2ec-233">幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-233">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="1d2ec-234">寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-234">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="1d2ec-235">URL は、会議中のダイアログ ボックスに表示 `<iframe>` されるページです。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-235">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="1d2ec-236">ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-236">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="1d2ec-237">`NotificationSignal`API には、次の例が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-237">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="1d2ec-238">C#</span><span class="sxs-lookup"><span data-stu-id="1d2ec-238">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="1d2ec-239">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d2ec-239">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="1d2ec-240">JSON</span><span class="sxs-lookup"><span data-stu-id="1d2ec-240">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="1d2ec-241">応答コード</span><span class="sxs-lookup"><span data-stu-id="1d2ec-241">Response codes</span></span>

<span data-ttu-id="1d2ec-242">`NotificationSignal`API には、次の応答コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-242">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="1d2ec-243">応答コード</span><span class="sxs-lookup"><span data-stu-id="1d2ec-243">Response code</span></span>|<span data-ttu-id="1d2ec-244">説明</span><span class="sxs-lookup"><span data-stu-id="1d2ec-244">Description</span></span>|
|---|---|
| <span data-ttu-id="1d2ec-245">**201**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-245">**201**</span></span> | <span data-ttu-id="1d2ec-246">シグナルを含むアクティビティが正常に送信されます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-246">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="1d2ec-247">**401**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-247">**401**</span></span> | <span data-ttu-id="1d2ec-248">アプリは無効なトークンで応答します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-248">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="1d2ec-249">**403**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-249">**403**</span></span> | <span data-ttu-id="1d2ec-250">アプリは信号を送信できません。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-250">The app is unable to send the signal.</span></span> <span data-ttu-id="1d2ec-251">これは、テナント管理者がアプリを無効にし、アプリがライブ サイトの移行中にブロックされるなど、さまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-251">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="1d2ec-252">この場合、ペイロードには詳細なエラー メッセージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-252">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="1d2ec-253">**404**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-253">**404**</span></span> | <span data-ttu-id="1d2ec-254">会議チャットが存在しません。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-254">The meeting chat does not exist.</span></span> |

### <a name="meeting-details-api"></a><span data-ttu-id="1d2ec-255">会議の詳細 API</span><span class="sxs-lookup"><span data-stu-id="1d2ec-255">Meeting Details API</span></span>

> [!NOTE]
> <span data-ttu-id="1d2ec-256">この機能は現在、パブリック開発者 [プレビューでのみ利用](../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-256">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="1d2ec-257">会議の詳細 API を使用すると、アプリは静的な会議のメタデータを取得できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-257">The Meeting Details API enables your app to get static meeting metadata.</span></span> <span data-ttu-id="1d2ec-258">これらは、動的に変更されないデータ ポイントです。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-258">These are data points that do not change dynamically.</span></span>
<span data-ttu-id="1d2ec-259">API はボット サービスを通じて利用できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-259">The API is available through Bot Services.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="1d2ec-260">クエリ パラメーター</span><span class="sxs-lookup"><span data-stu-id="1d2ec-260">Query parameter</span></span>

<span data-ttu-id="1d2ec-261">会議の詳細 API には、次のクエリ パラメーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-261">The Meeting Details API includes the following query parameter:</span></span>

|<span data-ttu-id="1d2ec-262">値</span><span class="sxs-lookup"><span data-stu-id="1d2ec-262">Value</span></span>|<span data-ttu-id="1d2ec-263">型</span><span class="sxs-lookup"><span data-stu-id="1d2ec-263">Type</span></span>|<span data-ttu-id="1d2ec-264">必須</span><span class="sxs-lookup"><span data-stu-id="1d2ec-264">Required</span></span>|<span data-ttu-id="1d2ec-265">説明</span><span class="sxs-lookup"><span data-stu-id="1d2ec-265">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="1d2ec-266">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="1d2ec-266">**meetingId**</span></span>| <span data-ttu-id="1d2ec-267">String</span><span class="sxs-lookup"><span data-stu-id="1d2ec-267">String</span></span> | <span data-ttu-id="1d2ec-268">はい</span><span class="sxs-lookup"><span data-stu-id="1d2ec-268">Yes</span></span> | <span data-ttu-id="1d2ec-269">会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-269">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span> |

#### <a name="example"></a><span data-ttu-id="1d2ec-270">例</span><span class="sxs-lookup"><span data-stu-id="1d2ec-270">Example</span></span>

<span data-ttu-id="1d2ec-271">会議の詳細 API には、次の例が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-271">The Meeting Details API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="1d2ec-272">C#</span><span class="sxs-lookup"><span data-stu-id="1d2ec-272">C#</span></span>](#tab/dotnet)

```csharp
var connectorClient = parameters.TurnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[<span data-ttu-id="1d2ec-273">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d2ec-273">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="1d2ec-274">利用不可</span><span class="sxs-lookup"><span data-stu-id="1d2ec-274">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="1d2ec-275">JSON</span><span class="sxs-lookup"><span data-stu-id="1d2ec-275">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

<span data-ttu-id="1d2ec-276">会議の詳細 API の JSON 応答本文は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-276">The JSON response body for Meeting Details API is as follows:</span></span>

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a><span data-ttu-id="1d2ec-277">リアルタイムの会議Teamsイベント</span><span class="sxs-lookup"><span data-stu-id="1d2ec-277">Real-time Teams meeting events</span></span>

> [!NOTE]
> <span data-ttu-id="1d2ec-278">この機能は現在、パブリック開発者 [プレビューでのみ利用](../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-278">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="1d2ec-279">ユーザーはリアルタイムの会議イベントを受信できます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-279">The user can receive real-time meeting events.</span></span> <span data-ttu-id="1d2ec-280">アプリが会議に関連付けられるとすぐに、実際の会議の開始時刻と会議の終了時刻がボットと共有されます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-280">As soon as any app is associated with a meeting, the actual meeting start and meeting end time are shared with the bot.</span></span>

<span data-ttu-id="1d2ec-281">会議の実際の開始時刻と終了時刻は、スケジュールされた開始時刻と終了時刻とは異なります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-281">Actual start and end time of a meeting are different from the scheduled start and end time.</span></span> <span data-ttu-id="1d2ec-282">会議の詳細 API はスケジュールされた開始時刻と終了時刻を提供し、イベントは実際の開始時刻と終了時刻を提供します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-282">The meeting details API provides the scheduled start and end time while the event provides the actual start and end time.</span></span>

### <a name="example-of-meeting-start-event-payload"></a><span data-ttu-id="1d2ec-283">会議の開始イベント ペイロードの例</span><span class="sxs-lookup"><span data-stu-id="1d2ec-283">Example of meeting start event payload</span></span>

<span data-ttu-id="1d2ec-284">次のコードは、会議の開始イベント ペイロードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-284">The following code provides an example of meeting start event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id":"meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a><span data-ttu-id="1d2ec-285">会議の終了イベント ペイロードの例</span><span class="sxs-lookup"><span data-stu-id="1d2ec-285">Example of meeting end event payload</span></span>

<span data-ttu-id="1d2ec-286">次のコードは、会議の終了イベント ペイロードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-286">The following code provides an example of meeting end event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-getting-metadata-of-a-meeting"></a><span data-ttu-id="1d2ec-287">会議のメタデータを取得する例</span><span class="sxs-lookup"><span data-stu-id="1d2ec-287">Example of getting metadata of a meeting</span></span>

<span data-ttu-id="1d2ec-288">ボットはハンドラーを介してイベントを受け取 `OnEventActivityAsync` ります。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-288">Your bot receives the event through the `OnEventActivityAsync` handler.</span></span>

<span data-ttu-id="1d2ec-289">json ペイロードを逆シリアル化するために、会議のメタデータを取得するためにモデル オブジェクトが導入されます。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-289">To deserialize the json payload, a model object is introduced to get the metadata of a meeting.</span></span> <span data-ttu-id="1d2ec-290">会議のメタデータは、イベント ペイロード `value` 内のプロパティに存在します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-290">The metadata of a meeting resides in the `value` property in the event payload.</span></span> <span data-ttu-id="1d2ec-291">model `MeetingStartEndEventvalue` オブジェクトが作成され、メンバー変数はイベント ペイロード内のプロパティの `value` キーに対応します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-291">The `MeetingStartEndEventvalue` model object is created, whose member variables correspond to the keys under the `value` property in the event payload.</span></span>

<span data-ttu-id="1d2ec-292">次のコードは、会議の開始イベントと終了イベントのメタデータをキャプチャする方法 `MeetingType` `Title` `Id` `JoinUrl` `StartTime` `EndTime` を示しています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-292">The following code shows how to capture the metadata of a meeting that is `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime`, and `EndTime` from a meeting start and end event:</span></span>

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

<span data-ttu-id="1d2ec-293">MeetingStartEndEventvalue.cs には、次のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-293">The MeetingStartEndEventvalue.cs includes the following code:</span></span>

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a><span data-ttu-id="1d2ec-294">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="1d2ec-294">Code sample</span></span>

|<span data-ttu-id="1d2ec-295">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="1d2ec-295">Sample name</span></span> | <span data-ttu-id="1d2ec-296">説明</span><span class="sxs-lookup"><span data-stu-id="1d2ec-296">Description</span></span> | <span data-ttu-id="1d2ec-297">.NET</span><span class="sxs-lookup"><span data-stu-id="1d2ec-297">.NET</span></span> | <span data-ttu-id="1d2ec-298">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d2ec-298">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="1d2ec-299">会議の機能拡張</span><span class="sxs-lookup"><span data-stu-id="1d2ec-299">Meetings extensibility</span></span> | <span data-ttu-id="1d2ec-300">Microsoft Teams渡しに関する会議機能拡張サンプル。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-300">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="1d2ec-301">View</span><span class="sxs-lookup"><span data-stu-id="1d2ec-301">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="1d2ec-302">View</span><span class="sxs-lookup"><span data-stu-id="1d2ec-302">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="1d2ec-303">会議コンテンツ バブル ボット</span><span class="sxs-lookup"><span data-stu-id="1d2ec-303">Meeting content bubble bot</span></span> | <span data-ttu-id="1d2ec-304">Microsoft Teamsでコンテンツ バブル ボットを操作するための会議機能拡張サンプルを作成します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-304">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="1d2ec-305">View</span><span class="sxs-lookup"><span data-stu-id="1d2ec-305">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="1d2ec-306">View</span><span class="sxs-lookup"><span data-stu-id="1d2ec-306">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="1d2ec-307">MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="1d2ec-307">Meeting meetingSidePanel</span></span> | <span data-ttu-id="1d2ec-308">Microsoft Teamsのサイド パネルを操作するための会議機能拡張サンプルを作成します。</span><span class="sxs-lookup"><span data-stu-id="1d2ec-308">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="1d2ec-309">View</span><span class="sxs-lookup"><span data-stu-id="1d2ec-309">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="1d2ec-310">View</span><span class="sxs-lookup"><span data-stu-id="1d2ec-310">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|

## <a name="see-also"></a><span data-ttu-id="1d2ec-311">関連項目</span><span class="sxs-lookup"><span data-stu-id="1d2ec-311">See also</span></span>

* [<span data-ttu-id="1d2ec-312">会議中のダイアログの設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="1d2ec-312">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="1d2ec-313">Teamsの認証フロー</span><span class="sxs-lookup"><span data-stu-id="1d2ec-313">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="1d2ec-314">会議のTeamsアプリ</span><span class="sxs-lookup"><span data-stu-id="1d2ec-314">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="1d2ec-315">次の手順</span><span class="sxs-lookup"><span data-stu-id="1d2ec-315">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d2ec-316">会議で使用するアプリを有効Teamsする</span><span class="sxs-lookup"><span data-stu-id="1d2ec-316">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
