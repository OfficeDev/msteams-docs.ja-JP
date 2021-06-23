---
title: 会議で使用するアプリを有効Teamsする
author: surbhigupta
description: 会議で使用するアプリを有効Teamsする
ms.topic: conceptual
ms.openlocfilehash: e31e241a61f40a8dc2b8a1221765bd4755d346ed
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068642"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a><span data-ttu-id="63c6f-103">会議で使用するアプリを有効Teamsする</span><span class="sxs-lookup"><span data-stu-id="63c6f-103">Enable and configure your apps for Teams meetings</span></span>

<span data-ttu-id="63c6f-104">すべてのチームは、タスクのコミュニケーションと共同作業の異なる方法を持っています。</span><span class="sxs-lookup"><span data-stu-id="63c6f-104">Every team has a different way of communicating and collaborating tasks.</span></span> <span data-ttu-id="63c6f-105">これらの異なるタスクを実現するには、会議Teamsをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="63c6f-105">You can achieve these different tasks by customizing Teams with apps for meetings.</span></span> <span data-ttu-id="63c6f-106">異なるタスクをカスタマイズして達成するには、アプリを会議に対して有効にし、Teamsマニフェスト内の会議スコープで使用できるアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-106">To customize and to achieve different tasks, you must enable your apps for Teams meetings and configure your apps to be available in meeting scope within their app manifest.</span></span>

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="63c6f-107">会議でアプリを有効Teamsする</span><span class="sxs-lookup"><span data-stu-id="63c6f-107">Enable your app for Teams meetings</span></span>

<span data-ttu-id="63c6f-108">会議でアプリを有効にするにはTeamsマニフェストを更新し、コンテキスト プロパティを使用してアプリを表示する場所を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-108">To enable your app for Teams meetings, you must update your app manifest and use the context properties to determine where your app must appear.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="63c6f-109">アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="63c6f-109">Update your app manifest</span></span>

<span data-ttu-id="63c6f-110">会議アプリの機能は、、 、および配列を使用してアプリ マニフェスト `configurableTabs` `scopes` で宣言 `context` されます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-110">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="63c6f-111">スコープは、アプリを使用できる場所を定義するユーザーとコンテキストを定義します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-111">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> * <span data-ttu-id="63c6f-112">マニフェスト スキーマを使用してアプリ マニフェストを [更新してみてください](../resources/schema/manifest-schema-dev-preview.md)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-112">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> * <span data-ttu-id="63c6f-113">会議のアプリには、グループチャットスコープが必要です。</span><span class="sxs-lookup"><span data-stu-id="63c6f-113">Apps in meetings require groupchat scope.</span></span> <span data-ttu-id="63c6f-114">チーム スコープは、チャネル内のタブでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-114">The team scope works for tabs in channels only.</span></span>

<span data-ttu-id="63c6f-115">アプリ マニフェストには、次のコード スニペットが含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-115">The app manifest must include the following code snippet:</span></span>

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
> <span data-ttu-id="63c6f-116">`meetingStage` は現在、開発者 [プレビューでのみ使用](../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-116">`meetingStage` is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

### <a name="context-property"></a><span data-ttu-id="63c6f-117">Context プロパティ</span><span class="sxs-lookup"><span data-stu-id="63c6f-117">Context property</span></span>

<span data-ttu-id="63c6f-118">プロパティは、ユーザーがアプリを呼び出す場所に応じて、ユーザーが会議でアプリを呼び出す際に表示 `context` する必要がある内容を決定します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-118">The `context` property determines what must be shown when a user invokes an app in a meeting depending on where the user invokes the app.</span></span> <span data-ttu-id="63c6f-119">タブと `context` プロパティ `scopes` を使用すると、アプリを表示する必要がある場所を特定できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-119">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="63c6f-120">またはスコープ内 `team` のタブ `groupchat` には、複数のコンテキストを指定できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-120">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="63c6f-121">値のすべてまたは一部を使用できるプロパティの値を `context` 次に示します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-121">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="63c6f-122">値</span><span class="sxs-lookup"><span data-stu-id="63c6f-122">Value</span></span>|<span data-ttu-id="63c6f-123">説明</span><span class="sxs-lookup"><span data-stu-id="63c6f-123">Description</span></span>|
|---|---|
| <span data-ttu-id="63c6f-124">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="63c6f-124">**channelTab**</span></span> | <span data-ttu-id="63c6f-125">チーム チャネルのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="63c6f-125">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="63c6f-126">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="63c6f-126">**privateChatTab**</span></span> | <span data-ttu-id="63c6f-127">チームまたは会議のコンテキストではなく、一連のユーザー間のグループ チャットのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="63c6f-127">A tab in the header of a group chat between a set of users, not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="63c6f-128">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="63c6f-128">**meetingChatTab**</span></span> | <span data-ttu-id="63c6f-129">スケジュールされた会議のコンテキスト内の一連のユーザー間のグループ チャットのヘッダー内のタブ。</span><span class="sxs-lookup"><span data-stu-id="63c6f-129">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="63c6f-130">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="63c6f-130">**meetingDetailsTab**</span></span> | <span data-ttu-id="63c6f-131">予定表の会議の詳細ビューのヘッダーにあるタブ。</span><span class="sxs-lookup"><span data-stu-id="63c6f-131">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="63c6f-132">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="63c6f-132">**meetingSidePanel**</span></span> | <span data-ttu-id="63c6f-133">統合バー (U バー) を介して開いた会議内パネル。</span><span class="sxs-lookup"><span data-stu-id="63c6f-133">An in-meeting panel opened through the unified bar (U-bar).</span></span> |
| <span data-ttu-id="63c6f-134">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="63c6f-134">**meetingStage**</span></span> | <span data-ttu-id="63c6f-135">meetingSidePanel のアプリを会議ステージに共有できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-135">An app from the meetingSidePanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="63c6f-136">`Context` プロパティは現在、モバイル クライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="63c6f-136">`Context` property is currently not supported on mobile clients.</span></span>

<span data-ttu-id="63c6f-137">会議でアプリを有効Teams、会議の前、会議中、会議の後にアプリを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-137">After you enable your app for Teams meetings, you must configure your app before a meeting, during a meeting, and after a meeting.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="63c6f-138">会議シナリオ用にアプリを構成する</span><span class="sxs-lookup"><span data-stu-id="63c6f-138">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="63c6f-139">タブ ギャラリーにアプリを表示するには、構成可能なタブとグループ チャット スコープをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-139">For your app to be visible in the tab gallery, it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="63c6f-140">モバイル クライアントは、会議の開催前と開催後のステージでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="63c6f-140">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="63c6f-141">現在、モバイル クライアントでは、会議中のダイアログ ボックスとタブである会議内エクスペリエンスはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="63c6f-141">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="63c6f-142">詳細については、「モバイル用の [タブを作成する際の](../tabs/design/tabs-mobile.md) モバイルタブのガイダンス」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="63c6f-142">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) while creating your tabs for mobile.</span></span>

<span data-ttu-id="63c6f-143">Teams会議は、組織に固有の共同作業エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-143">Teams meetings provides a unique collaborative experience for your organization.</span></span> <span data-ttu-id="63c6f-144">さまざまな会議シナリオ用にアプリを構成する機会を提供します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-144">It provides the opportunity to configure your app for different meeting scenarios.</span></span> <span data-ttu-id="63c6f-145">参加者の役割またはユーザーの種類に基づいて会議のエクスペリエンスを向上させるアプリを構成できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-145">You can configure your apps to enhance the meeting experience based on participant role or user type.</span></span> <span data-ttu-id="63c6f-146">これで、次の会議シナリオで実行できるアクションを特定できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-146">Now you can identify what actions can be taken in the following meeting scenarios:</span></span>
* [<span data-ttu-id="63c6f-147">事前会議</span><span class="sxs-lookup"><span data-stu-id="63c6f-147">Pre-meeting</span></span>](#pre-meeting)
* [<span data-ttu-id="63c6f-148">会議中</span><span class="sxs-lookup"><span data-stu-id="63c6f-148">In-meeting</span></span>](#in-meeting)
* [<span data-ttu-id="63c6f-149">会議後</span><span class="sxs-lookup"><span data-stu-id="63c6f-149">Post-meeting</span></span>](#post-meeting)

### <a name="pre-meeting"></a><span data-ttu-id="63c6f-150">事前会議</span><span class="sxs-lookup"><span data-stu-id="63c6f-150">Pre-meeting</span></span>

<span data-ttu-id="63c6f-151">会議の前に、ユーザーはタブ、ボット、メッセージング拡張機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-151">Before a meeting, users can add tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="63c6f-152">開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-152">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="63c6f-153">**タブを会議に追加するには**</span><span class="sxs-lookup"><span data-stu-id="63c6f-153">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="63c6f-154">予定表で、タブを追加する会議を選択します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-154">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="63c6f-155">[詳細] **タブを選択** し、[</span><span class="sxs-lookup"><span data-stu-id="63c6f-155">Select the **Details** tab and select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="63c6f-156">.</span><span class="sxs-lookup"><span data-stu-id="63c6f-156">.</span></span>

    ![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="63c6f-158">表示されるタブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。</span><span class="sxs-lookup"><span data-stu-id="63c6f-158">In the tab gallery that appears, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="63c6f-159">アプリはタブとしてインストールされます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-159">The app is installed as a tab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="63c6f-160">現在、会議タブでは、会議の詳細と参加者情報の取得はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="63c6f-160">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="63c6f-161">**会議にメッセージング拡張機能を追加するには**</span><span class="sxs-lookup"><span data-stu-id="63c6f-161">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="63c6f-162">チャット内のメッセージ &#x25CF;&#x25CF;&#x25CF; にある省略記号を選択します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-162">Select the ellipses &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="63c6f-163">追加するアプリを選択し、必要に応じて手順に従います。</span><span class="sxs-lookup"><span data-stu-id="63c6f-163">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="63c6f-164">アプリはメッセージング拡張機能としてインストールされます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-164">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="63c6f-165">**ボットを会議に追加するには**</span><span class="sxs-lookup"><span data-stu-id="63c6f-165">**To add a bot to a meeting**</span></span>

<span data-ttu-id="63c6f-166">会議チャットで、キーを入力し **@** 、[ボットの取得 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="63c6f-166">In a meeting chat, enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="63c6f-167">ユーザー ID は、Tabs SSO を使用して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-167">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="63c6f-168">認証後、アプリは API を使用してユーザー ロールを取得 `GetParticipant` できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-168">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="63c6f-169">ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-169">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="63c6f-170">たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-170">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="63c6f-171">会議の進行中に役割の割り当てを変更できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-171">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="63c6f-172">詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-172">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="in-meeting"></a><span data-ttu-id="63c6f-173">会議中</span><span class="sxs-lookup"><span data-stu-id="63c6f-173">In-meeting</span></span>

<span data-ttu-id="63c6f-174">会議中に、meetingSidePanel または会議内ダイアログ ボックスを使用して、アプリに固有のエクスペリエンスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-174">During a meeting, you can use the meetingSidePanel or the in-meeting dialog box to build unique experiences for your apps.</span></span>

#### <a name="meetingsidepanel"></a><span data-ttu-id="63c6f-175">meetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="63c6f-175">meetingSidePanel</span></span>

<span data-ttu-id="63c6f-176">meetingSidePanel を使用すると、会議のエクスペリエンスをカスタマイズして、開催者と発表者が異なる一連のビューとアクションを持つ事が可能です。</span><span class="sxs-lookup"><span data-stu-id="63c6f-176">With the meetingSidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="63c6f-177">アプリ マニフェストで、コンテキスト配列に meetingSidePanel を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-177">In your app manifest, you must add meetingSidePanel to the context array.</span></span> <span data-ttu-id="63c6f-178">会議およびすべてのシナリオで、アプリは幅 320 ピクセルの会議内タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-178">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="63c6f-179">詳細については [、「FrameContext インターフェイス」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-179">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="63c6f-180">API を使用して要求を必要に応じてルーティングするには、「SDK `userContext` Teams[参照してください](../tabs/how-to/access-teams-context.md#user-context)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-180">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="63c6f-181">詳細については、「タブの認証[フロー Teamsを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-181">For more information, see [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="63c6f-182">タブの認証フローは、Web サイトの認証フローと非常に似ています。</span><span class="sxs-lookup"><span data-stu-id="63c6f-182">Authentication flow for tabs is very similar to the authentication flow for websites.</span></span> <span data-ttu-id="63c6f-183">したがって、タブは OAuth 2.0 を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-183">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="63c6f-184">詳細については、「Microsoft ID プラットフォーム[OAuth 2.0 認証コード フロー」を参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-184">For more information, see [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="63c6f-185">メッセージング拡張機能は、ユーザーが会議内ビューに表示され、ユーザーが作成メッセージ内線カードを投稿できる場合に期待通り機能します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-185">Messaging extension works as expected when a user is in an in-meeting view, and the user can post compose message extension cards.</span></span> <span data-ttu-id="63c6f-186">AppName in-meeting は、会議中の U バーのアプリ名を示すツールヒントです。</span><span class="sxs-lookup"><span data-stu-id="63c6f-186">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="63c6f-187">バージョン 1.7.0 以上の[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用します。前のバージョンではサイド パネルはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="63c6f-187">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog-box"></a><span data-ttu-id="63c6f-188">[会議内] ダイアログ ボックス</span><span class="sxs-lookup"><span data-stu-id="63c6f-188">In-meeting dialog box</span></span>

<span data-ttu-id="63c6f-189">[会議中] ダイアログ ボックスを使用すると、会議中に参加者を引き付け、会議中に情報やフィードバックを収集できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-189">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="63c6f-190">API を [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) 使用して、バブル通知をトリガーする必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-190">Use the [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="63c6f-191">通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含める。</span><span class="sxs-lookup"><span data-stu-id="63c6f-191">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="63c6f-192">会議中のダイアログでは、タスク モジュールを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="63c6f-192">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="63c6f-193">タスク モジュールは、会議チャットでは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="63c6f-193">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="63c6f-194">外部リソース URL を使用して、会議にコンテンツ バブルを表示します。</span><span class="sxs-lookup"><span data-stu-id="63c6f-194">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="63c6f-195">このメソッドを使用 `submitTask` して、会議チャットでデータを送信できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-195">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="63c6f-196">ユーザーが Web ビューでアクションを実行した後に自動的に終了するには [、submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-196">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web view.</span></span> <span data-ttu-id="63c6f-197">これは、アプリの申請に必要な要件です。</span><span class="sxs-lookup"><span data-stu-id="63c6f-197">This is a requirement for app submission.</span></span> <span data-ttu-id="63c6f-198">詳細については、「SDK タスク モジュール[Teamsを参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-198">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="63c6f-199">アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、要求メタデータではなく、オブジェクト内の要求メタデータ `from.id` `from` に `from.aadObjectId` 依存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-199">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="63c6f-200">`from.id`はユーザー ID であり `from.aadObjectId` 、ユーザー Azure Active Directory (AAD) ID です。</span><span class="sxs-lookup"><span data-stu-id="63c6f-200">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="63c6f-201">詳細については、「タブでタスク [モジュールを使用する」を参照し](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、 [タスク モジュールを作成して送信します](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="63c6f-201">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="63c6f-202">ステージ間の共有</span><span class="sxs-lookup"><span data-stu-id="63c6f-202">Share to stage</span></span>

> [!NOTE]
> * <span data-ttu-id="63c6f-203">この機能は現在、開発者プレビュー [でのみ使用](../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-203">This capability is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>
> * <span data-ttu-id="63c6f-204">この機能を使用するには、アプリが会議中の meetingSidePanel をサポートしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-204">To use this feature, the app must support an in-meeting meetingSidePanel.</span></span>

<span data-ttu-id="63c6f-205">この機能により、開発者はアプリを会議ステージに共有できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-205">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="63c6f-206">会議ステージへの共有を有効にすると、会議の参加者はリアルタイムで共同作業できます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-206">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span>

<span data-ttu-id="63c6f-207">必要なコンテキストは `meetingStage` 、アプリ マニフェスト内です。</span><span class="sxs-lookup"><span data-stu-id="63c6f-207">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="63c6f-208">このための前提条件は、コンテキストを持 `meetingSidePanel` つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="63c6f-208">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="63c6f-209">これにより **、meetingSidePanel** で共有が有効です。</span><span class="sxs-lookup"><span data-stu-id="63c6f-209">This enables **Share** in the meetingSidePanel.</span></span>

![会議のエクスペリエンス中にステージに共有する](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="63c6f-211">この機能を有効にするために必要なマニフェストの変更は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="63c6f-211">The manifest change that is needed to enable this capability is as follows:</span></span>

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

### <a name="post-meeting"></a><span data-ttu-id="63c6f-212">会議後</span><span class="sxs-lookup"><span data-stu-id="63c6f-212">Post-meeting</span></span>

<span data-ttu-id="63c6f-213">会議後と会議 [前の](#pre-meeting) 構成は同じです。</span><span class="sxs-lookup"><span data-stu-id="63c6f-213">The post-meeting and [pre-meeting](#pre-meeting) configurations are the same.</span></span>

## <a name="code-sample"></a><span data-ttu-id="63c6f-214">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="63c6f-214">Code sample</span></span>

|<span data-ttu-id="63c6f-215">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="63c6f-215">Sample name</span></span> | <span data-ttu-id="63c6f-216">説明</span><span class="sxs-lookup"><span data-stu-id="63c6f-216">Description</span></span> | <span data-ttu-id="63c6f-217">サンプル</span><span class="sxs-lookup"><span data-stu-id="63c6f-217">Sample</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="63c6f-218">会議アプリ</span><span class="sxs-lookup"><span data-stu-id="63c6f-218">Meeting app</span></span> | <span data-ttu-id="63c6f-219">会議トークン ジェネレーター アプリを使用してトークンを要求する方法を示します。このトークンは、各参加者が対話する公平な機会を得る機会を得る順番に生成されます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-219">Demonstrates how to use the Meeting Token Generator app to request a token, which is generated sequentially so that each participant has a fair opportunity to interact.</span></span> <span data-ttu-id="63c6f-220">これは、スクラム会議、Q&セッションなど、状況に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="63c6f-220">This can be useful in situations like scrum meetings, Q&A sessions, and so on.</span></span> | [<span data-ttu-id="63c6f-221">View</span><span class="sxs-lookup"><span data-stu-id="63c6f-221">View</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a><span data-ttu-id="63c6f-222">関連項目</span><span class="sxs-lookup"><span data-stu-id="63c6f-222">See also</span></span>

* [<span data-ttu-id="63c6f-223">会議中のダイアログの設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="63c6f-223">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="63c6f-224">Teamsの認証フロー</span><span class="sxs-lookup"><span data-stu-id="63c6f-224">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
