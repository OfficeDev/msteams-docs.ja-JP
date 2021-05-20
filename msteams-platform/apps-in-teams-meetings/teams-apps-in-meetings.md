---
title: 会議でのアプリTeams
author: laujan
description: 参加者とユーザーの役割に基づくTeams会議でのアプリの概要
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: チーム アプリ 会議ユーザー参加者ロール API
ms.openlocfilehash: c5419565d8defd03a3dcfcc5b05b9517cb4269e2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565926"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="da8bd-104">会議でのアプリTeams</span><span class="sxs-lookup"><span data-stu-id="da8bd-104">Apps in Teams meetings</span></span>

<span data-ttu-id="da8bd-105">ミーティングは、包括的で活発なフォーラムでのコラボレーション、パートナーシップ、情報に基づいたコミュニケーション、および共有フィードバックを可能にします。</span><span class="sxs-lookup"><span data-stu-id="da8bd-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="da8bd-106">会議アプリは、出席者の状況に応じて、会議前、会議中、会議後のアプリエクスペリエンスなど、会議のライフサイクルの各段階に対してユーザー エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="da8bd-107">Teamsエンドユーザーは、次の例に示すタブ ギャラリーを使用して、会議中にアプリにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-107">Teams end-users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="da8bd-108">かんばんボードの事前ステージ</span><span class="sxs-lookup"><span data-stu-id="da8bd-108">Pre-stage a Kanban board</span></span>
* <span data-ttu-id="da8bd-109">会議中のアクション可能なダイアログを起動する</span><span class="sxs-lookup"><span data-stu-id="da8bd-109">Launch an in-meeting actionable dialog</span></span>
* <span data-ttu-id="da8bd-110">会議後のアンケートを作成する</span><span class="sxs-lookup"><span data-stu-id="da8bd-110">Create a post-meeting poll</span></span>

<span data-ttu-id="da8bd-111">Teamsの会議アプリの機能拡張は、次の概念に基づいています。</span><span class="sxs-lookup"><span data-stu-id="da8bd-111">Teams’ meeting app extensibility is based on the following concepts:</span></span>

<span data-ttu-id="da8bd-112">✔ミーティングのライフサイクルには、会議の前、中、および会議の期間後などの段階があります。</span><span class="sxs-lookup"><span data-stu-id="da8bd-112">✔ Meeting lifecycle has stages such as before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="da8bd-113">✔会議の開催者、発表者、出席者などの会議の参加者の役割。</span><span class="sxs-lookup"><span data-stu-id="da8bd-113">✔ Participant roles in a meeting such as meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="da8bd-114">✔テナント内、ゲスト、フェデレーション、匿名のユーザーなどの会議のユーザータイプTeams。</span><span class="sxs-lookup"><span data-stu-id="da8bd-114">✔ User types in a meeting such as in-tenant, guest, federated, or anonymous Teams user.</span></span>

<span data-ttu-id="da8bd-115">この記事では、会議のライフサイクルに関する情報と、会議でタブ、ボット、およびメッセージング拡張機能を統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-115">This article covers information about the meeting lifecycle and how to integrate tabs, bots, and messaging extensions in your meeting.</span></span> <span data-ttu-id="da8bd-116">また、参加者ロールを識別し、さまざまなユーザータイプを使用してタスクを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-116">It also enables you to identify participant roles and also use different user types to perform tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="da8bd-117">会議アプリの機能拡張機能を使用するには、適切なアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="da8bd-117">To work with the meeting app extensibility features, you must have the appropriate permissions.</span></span>

### <a name="meeting-lifecycle"></a><span data-ttu-id="da8bd-118">会議のライフサイクル</span><span class="sxs-lookup"><span data-stu-id="da8bd-118">Meeting lifecycle</span></span>

<span data-ttu-id="da8bd-119">会議のライフサイクルは、会議前、会議中、および会議後のアプリ エクスペリエンスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-119">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="da8bd-120">会議のライフサイクルの各段階で、タブ、ボット、およびメッセージング拡張機能を統合できます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-120">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="da8bd-121">タブを会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="da8bd-121">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="da8bd-122">タブを使用すると、チーム メンバーはチャネルまたはチャット内の特定のスペース内のサービスやコンテンツにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-122">Tabs allow team members to access services and content in a specific space within a channel or chat.</span></span> <span data-ttu-id="da8bd-123">これにより、チームはタブを直接操作し、タブ内で使用可能なツールやデータに関する会話を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-123">This lets the team work directly with tabs and have conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="da8bd-124">会議Teamsで、ユーザーはプラス</span><span class="sxs-lookup"><span data-stu-id="da8bd-124">In Teams meeting, users can add a tab by selecting plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="da8bd-125">をクリックし、タブとしてインストールするアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-125">, and choosing the app that they want to install as a tab.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da8bd-126">タブを会議に統合した場合、アプリはタブの[シングル サインオン (SSO) 認証フロー](../tabs/how-to/authentication/auth-aad-sso.md) Teamsに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="da8bd-126">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="da8bd-127">モバイル クライアントは、会議の前後のステージでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="da8bd-127">Mobile clients support tabs only in pre and post meeting stages.</span></span> <span data-ttu-id="da8bd-128">会議中のダイアログおよびパネルである会議内のエクスペリエンスは、現在、モバイルでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-128">The in-meeting experiences that is in-meeting dialog and panel are currently not available on mobile.</span></span>
> * <span data-ttu-id="da8bd-129">アプリは非公開のスケジュールされた会議でのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-129">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="da8bd-130">事前会議アプリエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="da8bd-130">Pre-meeting app experience</span></span>

<span data-ttu-id="da8bd-131">**事前会議の経験:**</span><span class="sxs-lookup"><span data-stu-id="da8bd-131">**Pre-meeting experience:**</span></span>

![会議前の経験](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="da8bd-133">**[会議前] タブ:**</span><span class="sxs-lookup"><span data-stu-id="da8bd-133">**Pre-meeting tab:**</span></span>

![会議前のタブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="da8bd-135">✔ 権限を持つユーザーとは、会議のライフサイクルのさまざまな段階で、会議にアプリを追加できるユーザーのことです。</span><span class="sxs-lookup"><span data-stu-id="da8bd-135">✔ Permissioned users are users who can add apps to a meeting during different stages of the meeting lifecycle.</span></span> <span data-ttu-id="da8bd-136">これらのユーザーは、次の 2 つの方法でタブ ギャラリーを使用して会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-136">These users can add apps to a meeting through the tab gallery in two ways:</span></span>

   * <span data-ttu-id="da8bd-137">Teams スケジューリング フォームの **[詳細**] タブを使用します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-137">Using the **Details** tab on the Teams scheduling form.</span></span>

   * <span data-ttu-id="da8bd-138">既存の会議で **[チャット** ] タブを使用する。</span><span class="sxs-lookup"><span data-stu-id="da8bd-138">Using the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="da8bd-139">✔タブ アプリは、ミーティングの **[詳細]** ページと [ **チャット** ] ページで、プラス ➕ ボタンを使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-139">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus ➕ button.</span></span>

<span data-ttu-id="da8bd-140">✔ 10 以上のアンケートまたはアンケートがある場合、タブ レイアウトは組織化された状態にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="da8bd-140">✔ Tab layout must be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="da8bd-141">会議中のアプリエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="da8bd-141">In-meeting app experience</span></span>

<span data-ttu-id="da8bd-142">ミーティング アプリ✔、チャット ウィンドウの上部バーにホストされ、[会議中] タブを使用して会議内のタブエクスペリエンスとしてホストされます。ユーザーがタブ ギャラリーを通じて会議にタブを追加すると、 **会議エクスペリエンス中** のアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-142">✔ Meeting apps are hosted in the top upper bar of the chat window and as in-meeting tab experience using the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences are shown.</span></span>

<span data-ttu-id="da8bd-143">✔アクセス許可ユーザーは、会議中にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-143">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="da8bd-144">✔会議のコンテキストで読み込まれると、アプリは Teams クライアント SDK を利用して `meetingId` `userMri` 、 にアクセスし、 `frameContext` エクスペリエンスを適切にレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-144">✔ When loaded in the context of a meeting, apps can leverage the Teams client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="da8bd-145">✔アンケートまたはアンケートの結果をエクスポートすると、結果が正常にダウンロードされたことをユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-145">✔ Exporting a result of a survey or poll notifies the users that the results successfully downloaded.</span></span>

<span data-ttu-id="da8bd-146">✔サイド パネルまたは会議中のダイアログ ボックスで、Teams会議でアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-146">✔ An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span> <span data-ttu-id="da8bd-147">会議の参加者の操作可能なコンテンツを表示するには、会議中のダイアログ ボックスを使用します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-147">Use the in-meeting dialog box to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="da8bd-148">詳しくは[、Teams会議用のアプリの作成に関する](create-apps-for-teams-meetings.md)ページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="da8bd-148">For more information, see [create apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="da8bd-149">アプリ マニフェストでは、タブが [サイド パネル に最適化され](create-apps-for-teams-meetings.md#during-a-meeting)、表示される場所が指定されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-149">Your app manifest specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it is displayed.</span></span> <span data-ttu-id="da8bd-150">また、指定された設計ガイドラインに従って、共有トレイ エクスペリエンスの一部にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-150">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="da8bd-151">次の図は、会議内のダイアログ ボックスおよび別のサイド パネルとしてアプリを表示します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-151">The following images display the app as an in-meeting dialog box and as a separate side panel:</span></span>

![会議中の経験](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議内のダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a><span data-ttu-id="da8bd-154">ユーザーの会議中のアクション可能なダイアログ</span><span class="sxs-lookup"><span data-stu-id="da8bd-154">In-meeting actionable dialog for users</span></span>

![ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="da8bd-156">会議後のアプリエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="da8bd-156">Post-meeting app experience</span></span>

![会議の表示を投稿](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="da8bd-158">✔ 会議後のアプリのシナリオは、現在の会議後のエクスペリエンスに似ています。</span><span class="sxs-lookup"><span data-stu-id="da8bd-158">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span>

<span data-ttu-id="da8bd-159">✔アクセス許可ユーザーは、Teamsスケジュール フォームの **[詳細**] タブと既存の会議の [会議 **チャット**] タブを使用して、タブ ギャラリーから会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-159">✔ Permissioned users can add apps from the tab gallery to a meeting using the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="da8bd-160">✔タブレイアウトは、アンケートまたはアンケートが 10 件を超える場合に整理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da8bd-160">✔  Tab layout must be organized when there are more than ten polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="da8bd-161">ボットを会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="da8bd-161">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="da8bd-162">ボットの実装については、[まずボットのビルド](../build-your-first-app/build-bot.md)から開始し[、Teams会議用のアプリの作成](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)に進みます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-162">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="da8bd-163">メッセージング拡張機能を会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="da8bd-163">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="da8bd-164">メッセージング拡張機能の実装の場合は、まず[メッセージング拡張機能の構築](../messaging-extensions/how-to/create-messaging-extension.md)から始めて[、Teams会議用のアプリの作成](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)に進みます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-164">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="da8bd-165">会議の参加者ロールとユーザー タイプ</span><span class="sxs-lookup"><span data-stu-id="da8bd-165">Participant roles and user types in a meeting</span></span>

![ミーティングの参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="da8bd-167">参加者の役割</span><span class="sxs-lookup"><span data-stu-id="da8bd-167">Participant roles</span></span>

<span data-ttu-id="da8bd-168">既定の参加者設定は、組織の IT 管理者によって決定されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-168">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="da8bd-169">ミーティングの参加者の役割は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="da8bd-169">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="da8bd-170">**開催** 者 : 開催者は会議のスケジュールを設定し、会議のオプションを設定し、会議の役割を割り当て、会議を開始します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-170">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="da8bd-171">Teamsライセンスを持つ M365 アカウントを持つユーザーのみが開催者になり、出席者のアクセス許可を制御できます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-171">Only users with a M365 account with a Teams license can be organizers and control attendee permissions.</span></span> <span data-ttu-id="da8bd-172">会議の開催者は、特定の会議の設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-172">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="da8bd-173">開催者は、 **会議オプション** Web ページでこれらの変更を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-173">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="da8bd-174">**発表** 者 : 発表者は主催者と同じ機能を持っています。</span><span class="sxs-lookup"><span data-stu-id="da8bd-174">**Presenter**: Presenters have the same capabilities as organizer.</span></span> <span data-ttu-id="da8bd-175">ただし、発表者は、セッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-175">However, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="da8bd-176">既定では、ミーティングに参加する参加者には発表者の役割があります。</span><span class="sxs-lookup"><span data-stu-id="da8bd-176">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="da8bd-177">**出席者**: 出席者とは、会議に出席するように招待されたが、発表者として行動する権限がないユーザーです。</span><span class="sxs-lookup"><span data-stu-id="da8bd-177">**Attendee**: An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="da8bd-178">出席者は他の会議メンバーと対話できますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-178">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="da8bd-179">アプリを追加、削除、またはアンインストールできるのは、主催者または発表者のみです。</span><span class="sxs-lookup"><span data-stu-id="da8bd-179">Only an organizer or presenter can add, remove, or uninstall apps.</span></span> <span data-ttu-id="da8bd-180">会議で投票を作成できるのは、開催者または発表者のみです。</span><span class="sxs-lookup"><span data-stu-id="da8bd-180">Only organizer or presenter can create polls in a meeting.</span></span>

<span data-ttu-id="da8bd-181">詳細については、「 [Teams会議でのロール](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da8bd-181">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="da8bd-182">**[ミーティングのオプション]** ページには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-182">You can access the  **Meeting options** page as follows:</span></span>

* <span data-ttu-id="da8bd-183">Teamsで、[予定表の ![ ロゴ] に移動 ](../assets/images/apps-in-meetings/calendar-logo.png) し、会議を選択し、[**会議のオプション]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="da8bd-183">In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

* <span data-ttu-id="da8bd-184">会議出席依頼で、[ **ミーティング のオプション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-184">In a meeting invitation, select **Meeting options**.</span></span>

* <span data-ttu-id="da8bd-185">会議中に、[参加者 **を表示する**] ![ を ](../assets/images/apps-in-meetings/show-participants.png) 選択して会議コントロールの参加者を表示します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-185">During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="da8bd-186">次に、参加者のリストの上にある [ **権限の管理**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-186">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="da8bd-187">ユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="da8bd-187">User types</span></span>

> [!NOTE]
> <span data-ttu-id="da8bd-188">特定のユーザー タイプが割り当てられているユーザーは、ミーティングに参加し、 [参加者](#participant-roles)ロールで説明されている参加者ロールの 1 つを引き受けることができます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-188">Users with specific user types assigned to them can join meetings and assume one of the participant roles described in [participant roles](#participant-roles).</span></span> <span data-ttu-id="da8bd-189">ユーザータイプは **、getParticipantRole** API に含まれていません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-189">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="da8bd-190">次のユーザーの種類は、各ユーザーが実行できる操作と、アクセスできる操作を識別します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-190">The following user types identify what each user can do and what they can access:</span></span>

* <span data-ttu-id="da8bd-191">**テナント内**: テナント内のユーザーは組織に属し、テナントの資格情報Azure Active Directory (AAD) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="da8bd-191">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="da8bd-192">通常、フルタイム、オンサイト、またはリモートの従業員です。</span><span class="sxs-lookup"><span data-stu-id="da8bd-192">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="da8bd-193">テナント内のユーザーは、開催者、発表者、または出席者です。</span><span class="sxs-lookup"><span data-stu-id="da8bd-193">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="da8bd-194">**ゲスト**: ゲストとは、組織のテナント内のTeamsやその他のリソースにアクセスするよう招待された別の組織の参加者です。</span><span class="sxs-lookup"><span data-stu-id="da8bd-194">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="da8bd-195">ゲストは組織の AAD に追加され、チーム チャット、会議、ファイルにアクセスできるネイティブ チーム メンバーと同じTeams機能を持ちます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-195">Guests are added to your organization’s AAD and have the same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="da8bd-196">ゲスト ユーザーは、開催者、発表者、または出席者です。</span><span class="sxs-lookup"><span data-stu-id="da8bd-196">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="da8bd-197">詳細については、「 Teams[のゲスト アクセス 」](/microsoftteams/guest-access)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da8bd-197">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="da8bd-198">**フェデレーションまたは外部**: フェデレーション ユーザーは、会議に招待された別の組織の外部Teamsユーザーです。</span><span class="sxs-lookup"><span data-stu-id="da8bd-198">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="da8bd-199">これらのユーザーは、フェデレーション パートナーとの有効な資格情報を持ち、Teamsによって承認されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-199">These users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="da8bd-200">チームや組織の他の共有リソースにはアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-200">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="da8bd-201">ゲスト アクセスは、外部ユーザーがチームやチャネルにアクセスするためのより良いオプションです。</span><span class="sxs-lookup"><span data-stu-id="da8bd-201">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="da8bd-202">詳細については、「 [Teams での外部アクセスの管理](/microsoftteams/manage-external-access)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da8bd-202">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>
* <span data-ttu-id="da8bd-203">**匿名**: 匿名ユーザーは AAD ID を持たないし、テナントとフェデレーションされません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-203">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="da8bd-204">匿名参加者は外部ユーザーと似ていますが、その ID は会議で投影されません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-204">The anonymous participant is like an external user, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="da8bd-205">匿名ユーザーは開催者になれませんが、発表者または出席者になることもできます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-205">An anonymous user cannot be an organizer but can be a presenter or an attendee.</span></span>

> [!NOTE]
> <span data-ttu-id="da8bd-206">匿名ユーザーは、グローバルな既定のユーザー レベルアプリのアクセス許可ポリシーを継承します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-206">Anonymous users inherit the global default user-level app permission policy.</span></span> <span data-ttu-id="da8bd-207">詳細については、「 [アプリの管理](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="da8bd-207">For more information, see [Manage Apps](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).</span></span>

<span data-ttu-id="da8bd-208">次の表に、ユーザーの種類と各ユーザーがアクセスできる機能を示します。</span><span class="sxs-lookup"><span data-stu-id="da8bd-208">The following table provides the user types and what features each user can access:</span></span>

| <span data-ttu-id="da8bd-209">ユーザータイプ</span><span class="sxs-lookup"><span data-stu-id="da8bd-209">User type</span></span> | <span data-ttu-id="da8bd-210">タブ</span><span class="sxs-lookup"><span data-stu-id="da8bd-210">Tabs</span></span> | <span data-ttu-id="da8bd-211">ボット</span><span class="sxs-lookup"><span data-stu-id="da8bd-211">Bots</span></span> | <span data-ttu-id="da8bd-212">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="da8bd-212">Messaging extensions</span></span> | <span data-ttu-id="da8bd-213">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="da8bd-213">Adaptive Cards</span></span> | <span data-ttu-id="da8bd-214">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="da8bd-214">Task modules</span></span> | <span data-ttu-id="da8bd-215">会議中ダイアログ</span><span class="sxs-lookup"><span data-stu-id="da8bd-215">In-meeting dialog</span></span> |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| <span data-ttu-id="da8bd-216">匿名ユーザー</span><span class="sxs-lookup"><span data-stu-id="da8bd-216">Anonymous user</span></span> | <span data-ttu-id="da8bd-217">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-217">Not available</span></span> | <span data-ttu-id="da8bd-218">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-218">Not available</span></span> | <span data-ttu-id="da8bd-219">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-219">Not available</span></span> | <span data-ttu-id="da8bd-220">会議チャットでの対話が許可されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-220">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="da8bd-221">アダプティブ カードからの会議チャットでのインタラクションが許可されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-221">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="da8bd-222">利用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-222">Not available</span></span> |
| <span data-ttu-id="da8bd-223">テナント AAD の一部であるゲスト</span><span class="sxs-lookup"><span data-stu-id="da8bd-223">Guest that is part of the tenant AAD</span></span> | <span data-ttu-id="da8bd-224">インタラクションが許可されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-224">Interaction is allowed.</span></span> <span data-ttu-id="da8bd-225">作成、更新、および削除は許可されません。</span><span class="sxs-lookup"><span data-stu-id="da8bd-225">Creating, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="da8bd-226">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-226">Not available</span></span> | <span data-ttu-id="da8bd-227">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-227">Not available</span></span> | <span data-ttu-id="da8bd-228">会議チャットでの対話が許可されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-228">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="da8bd-229">アダプティブ カードからの会議チャットでのインタラクションが許可されます。</span><span class="sxs-lookup"><span data-stu-id="da8bd-229">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="da8bd-230">Available</span><span class="sxs-lookup"><span data-stu-id="da8bd-230">Available</span></span> |
| <span data-ttu-id="da8bd-231">フェデレーション</span><span class="sxs-lookup"><span data-stu-id="da8bd-231">Federated</span></span> | <span data-ttu-id="da8bd-232">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-232">Not available</span></span> | <span data-ttu-id="da8bd-233">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-233">Not available</span></span> | <span data-ttu-id="da8bd-234">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-234">Not available</span></span> | <span data-ttu-id="da8bd-235">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-235">Not available</span></span> | <span data-ttu-id="da8bd-236">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-236">Not available</span></span> | <span data-ttu-id="da8bd-237">使用不可</span><span class="sxs-lookup"><span data-stu-id="da8bd-237">Not available</span></span> |

## <a name="see-also"></a><span data-ttu-id="da8bd-238">関連項目</span><span class="sxs-lookup"><span data-stu-id="da8bd-238">See also</span></span>

* [<span data-ttu-id="da8bd-239">Tab</span><span class="sxs-lookup"><span data-stu-id="da8bd-239">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="da8bd-240">ボット</span><span class="sxs-lookup"><span data-stu-id="da8bd-240">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="da8bd-241">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="da8bd-241">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="da8bd-242">アプリをデザインする</span><span class="sxs-lookup"><span data-stu-id="da8bd-242">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="da8bd-243">次の手順</span><span class="sxs-lookup"><span data-stu-id="da8bd-243">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="da8bd-244">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="da8bd-244">Build your app</span></span>](create-apps-for-teams-meetings.md)
