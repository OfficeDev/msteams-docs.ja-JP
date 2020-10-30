---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: 13fc44e9831cf58f0ab847eab06cc5b99ed8cc70
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796226"
---
# <a name="apps-in-teams-meetings-developer-preview"></a><span data-ttu-id="e3a47-104">Teams 会議のアプリ (開発者プレビュー)</span><span class="sxs-lookup"><span data-stu-id="e3a47-104">Apps in Teams meetings (Developer Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="e3a47-105">Microsoft Teams の開発者プレビューに含まれる機能は、すぐにアクセス、テスト、フィードバック目的のみに提供されています。</span><span class="sxs-lookup"><span data-stu-id="e3a47-105">Features included in Microsoft Teams Developer Preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="e3a47-106">公開リリースで利用できるようになる前に変更が行われ、運用アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

<span data-ttu-id="e3a47-107">会議は、Teams の生産性にとって重要です。</span><span class="sxs-lookup"><span data-stu-id="e3a47-107">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="e3a47-108">このツールを使用すると、包括的でアクティブなフォーラムで、コラボレーション、パートナーシップ、情報を伝えるコミュニケーション、および共有フィードバックを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-108">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="e3a47-109">開発者は、 [構成可能なタブ](../tabs/what-are-tabs.md#how-do-tabs-work)、 [ボット](../bots/what-are-bots.md)、および [メッセージ拡張](../messaging-extensions/what-are-messaging-extensions.md) アプリケーションを作成して、Teams の会議環境を強化し、充実させることができます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-109">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="e3a47-110">会議ユーザーは、タブギャラリーを使用してアプリにアクセスし、かんばんボードの事前ステージング、会議中のアクション可能なダイアログの開始、会議後の投票の作成など、関連するシナリオを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-110">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="e3a47-111">会議アプリは、出席者の状態に基づいて、会議のライフサイクルの各段階でユーザー環境を提供できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-111">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="e3a47-112">Teams のアプリの拡張機能センターは3つの概念に基づいています。</span><span class="sxs-lookup"><span data-stu-id="e3a47-112">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="e3a47-113">会議の **ライフサイクル** の✔ (会議の時間枠の前、前後、および後)。</span><span class="sxs-lookup"><span data-stu-id="e3a47-113">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="e3a47-114">✔ **参加者の役割** —会議の開催者、発表者、または出席者。</span><span class="sxs-lookup"><span data-stu-id="e3a47-114">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="e3a47-115">✔ **ユーザーの種類** -テナント、ゲスト、フェデレーション、または匿名 Teams ユーザー。</span><span class="sxs-lookup"><span data-stu-id="e3a47-115">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="e3a47-116">会議のライフサイクルのシナリオ</span><span class="sxs-lookup"><span data-stu-id="e3a47-116">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="e3a47-117">タブ</span><span class="sxs-lookup"><span data-stu-id="e3a47-117">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3a47-118">すべてのタブアプリケーションと同様に、アプリは、タブの Teams [SSO 認証フロー](../tabs/how-to/authentication/auth-aad-sso.md) に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3a47-118">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a47-119">モバイルクライアントは、会議のプレおよびポストの表面でのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="e3a47-119">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="e3a47-120">モバイルでの会議中のエクスペリエンス (会議中のダイアログとパネル) は近日中に利用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="e3a47-120">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="e3a47-121">ミーティング前アプリの作業</span><span class="sxs-lookup"><span data-stu-id="e3a47-121">Pre-meeting app experience</span></span>

<span data-ttu-id="e3a47-122">**ミーティング前の環境:**</span><span class="sxs-lookup"><span data-stu-id="e3a47-122">**Pre-meeting experience:**</span></span>

![ミーティング前の環境](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="e3a47-124">**[会議前] タブ:**</span><span class="sxs-lookup"><span data-stu-id="e3a47-124">**Pre-meeting tab:**</span></span>

![会議前のタブビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="e3a47-126">✔権限ユーザーは、次の2つの方法で、タブギャラリーを使用して会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-126">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="e3a47-127">&emsp;&emsp; Teams スケジュールフォームの [ **詳細** ] タブを使用して&#9679; します。</span><span class="sxs-lookup"><span data-stu-id="e3a47-127">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="e3a47-128">&emsp;&emsp; 既存の会議の [ミーティングの **チャット** ] タブを使用して&#9679; します。</span><span class="sxs-lookup"><span data-stu-id="e3a47-128">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="e3a47-129">✔タブアプリは、プラスアイコン (➕) ボタンを使用して、会議の **詳細** と **チャット** ページからアクセスできます。 |</span><span class="sxs-lookup"><span data-stu-id="e3a47-129">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="e3a47-130">会議中のアプリ環境</span><span class="sxs-lookup"><span data-stu-id="e3a47-130">In-meeting app experience</span></span>

<span data-ttu-id="e3a47-131">✔ Meeting アプリは、[会議中] タブを使用して、チャットウィンドウの上部上のバーと、会議のタブ操作としてホストされます。ユーザーがタブギャラリーを使用して会議にタブを追加すると、 **会議** のエクスペリエンス中のアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-131">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="e3a47-132">✔権限ユーザーは、会議中にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-132">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="e3a47-133">✔会議のコンテキストでロードされた場合、アプリは Teams クライアント SDK を活用して、にアクセス `meetingId` し、を `userMri` 適切に表示することができ `frameContext` ます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-133">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="e3a47-134">アプリの✔は、次の2つの領域で Teams 会議に表示できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-134">✔ For an app can be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="e3a47-135">&emsp;&emsp;&#9679; **サイドパネル** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-135">&emsp;&emsp;&#9679; **Side panel** .</span></span> </br>

> [!NOTE]
> <span data-ttu-id="e3a47-136">アプリの _マニフェスト_ で、タブが [サイドパネル用に最適化](create-apps-for-teams-meetings.md#in-meeting)されていることが指定されている場合は、それが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-136">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#in-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="e3a47-137">また、この機能は、指定された設計ガイドラインに従って、共有トレイの環境の一部にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-137">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="e3a47-138">&emsp;&emsp;&#9679; **会議中] ダイアログ** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-138">&emsp;&emsp;&#9679; **In-meeting dialog** .</span></span> <span data-ttu-id="e3a47-139">会議中のダイアログを使用して、会議の参加者に対して操作可能なコンテンツを示します。</span><span class="sxs-lookup"><span data-stu-id="e3a47-139">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="e3a47-140">「 [Teams 会議用アプリの作成」を](create-apps-for-teams-meetings.md)*参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-140">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="e3a47-141">**ミーティング中の環境:**</span><span class="sxs-lookup"><span data-stu-id="e3a47-141">**In-meeting experience:**</span></span>

![会議中の作業](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議中のダイアログ表示](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="e3a47-144">**ユーザーに対する会議中のアクション可能なダイアログ:**</span><span class="sxs-lookup"><span data-stu-id="e3a47-144">**In-meeting actionable dialog for users:**</span></span>

![ダイアログビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="e3a47-146">ミーティング後のアプリの作業</span><span class="sxs-lookup"><span data-stu-id="e3a47-146">Post-meeting app experience</span></span>

<span data-ttu-id="e3a47-147">**ミーティング後の環境:**</span><span class="sxs-lookup"><span data-stu-id="e3a47-147">**Post-meeting experience:**</span></span>

![投稿会議の表示](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="e3a47-149">ミーティング後のアプリのシナリオは、現在の会議の後の状態と似ています。これには、タブが表面内に存在するという利点があります。</span><span class="sxs-lookup"><span data-stu-id="e3a47-149">The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs exist within the surface.</span></span> <span data-ttu-id="e3a47-150">権限ユーザーは、[チームのスケジュール] フォームの [ **詳細** ] タブと既存の会議の [会議 **チャット** ] タブを使用して、タブギャラリーからアプリケーションを会議に追加できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-150">Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

### <a name="bots"></a><span data-ttu-id="e3a47-151">ボット</span><span class="sxs-lookup"><span data-stu-id="e3a47-151">Bots</span></span>

<span data-ttu-id="e3a47-152">Bot 実装の場合は、 [Teams の会議のドキュメントでボット](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e3a47-152">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="e3a47-153">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="e3a47-153">Messaging Extensions</span></span>

<span data-ttu-id="e3a47-154">メッセージング拡張機能の実装については、「 [Teams 会議のドキュメント」の「メッセージング拡張機能](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e3a47-154">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="e3a47-155">会議での参加者の役割とユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="e3a47-155">Participant roles and user types in a meeting</span></span>

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="e3a47-157">参加者の役割</span><span class="sxs-lookup"><span data-stu-id="e3a47-157">Participant roles</span></span>

<span data-ttu-id="e3a47-158">参加者固有の承認を使用してアプリを設計できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-158">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="e3a47-159">たとえば、開催者または発表者のみが会議で投票を作成できるとします。</span><span class="sxs-lookup"><span data-stu-id="e3a47-159">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="e3a47-160">既定の参加者設定は組織の IT 管理者によって決定されますが、会議の開催者は特定の会議の設定を変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e3a47-160">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="e3a47-161">開催者は、会議オプション web ページでこれらの変更を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-161">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="e3a47-162">**開催者** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-162">**Organizer** .</span></span> <span data-ttu-id="e3a47-163">開催者が会議をスケジュールし、会議オプションを設定し、会議の役割を割り当て、会議を開始します。</span><span class="sxs-lookup"><span data-stu-id="e3a47-163">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="e3a47-164">M365 アカウント (Teams ライセンスを所有) を持つユーザーのみが、開催者と参加者のアクセス許可を管理できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-164">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="e3a47-165">**プレゼンター** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-165">**Presenter** .</span></span> <span data-ttu-id="e3a47-166">プレゼンターには開催者とほぼ同じ機能があります。ただし、発表者はセッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-166">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="e3a47-167">既定では、会議に参加する参加者には発表者の役割が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-167">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="e3a47-168">**出席者** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-168">**Attendee** .</span></span> <span data-ttu-id="e3a47-169">出席者は、会議への参加を招待されているが、発表者としての権限を持っていないユーザーです。</span><span class="sxs-lookup"><span data-stu-id="e3a47-169">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="e3a47-170">出席者が他の会議メンバーと対話することはできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-170">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="e3a47-171">_See_ [ **Teams 会議でのロールの** 表示](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="e3a47-171">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="e3a47-172">[  **会議オプション** ] ページには、次のようにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-172">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="e3a47-173">&#11200; Teams で、 **予定** 表の予定表のロゴに移動し、 ![ 会議を選択し ](../assets/images/apps-in-meetings/calendar-logo.png) てから、[ **会議のオプション** ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e3a47-173">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options** .</span></span>

<span data-ttu-id="e3a47-174">会議出席依頼の &#11200; で、[ **会議オプション** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3a47-174">&#11200; In a meeting invitation, select **Meeting options** .</span></span>

<span data-ttu-id="e3a47-175">会議中に &#11200; は、[ **参加者** に参加者を表示する ![ ] アイコンをミーティングのコントロールに選択し ](../assets/images/apps-in-meetings/show-participants.png) ます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-175">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="e3a47-176">次に、参加者のリストの上にある [ **権限の管理** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3a47-176">Then, above the list of participants, choose **Manage permissions** .</span></span>

### <a name="user-types"></a><span data-ttu-id="e3a47-177">ユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="e3a47-177">User types</span></span>

> [!NOTE]
> <span data-ttu-id="e3a47-178">ユーザーの種類は会議に参加でき、前述の参加者の役割の1つを引き受けます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-178">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="e3a47-179">ユーザーの種類は、 **getParticipantRole** API の一部として公開されません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-179">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="e3a47-180">**テナント内** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-180">**In-tenant** .</span></span> <span data-ttu-id="e3a47-181">これらのユーザーは組織に属しており、テナントの Azure Active Directory に資格情報を持っています。</span><span class="sxs-lookup"><span data-stu-id="e3a47-181">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="e3a47-182">通常は、フルタイム、オンサイト、またはリモートの従業員です。</span><span class="sxs-lookup"><span data-stu-id="e3a47-182">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="e3a47-183">**ゲスト** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-183">**Guest** .</span></span> <span data-ttu-id="e3a47-184">ゲストは、組織のテナント内の Teams またはその他のリソースへのアクセスを招待された別の組織からの参加者です。</span><span class="sxs-lookup"><span data-stu-id="e3a47-184">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="e3a47-185">ゲストは組織の Active Directory に追加され、チームのチャット、会議、およびファイルへのフルアクセスを備えたネイティブのチームメンバーと同じ Teams の機能をほぼすべて提供できます。</span><span class="sxs-lookup"><span data-stu-id="e3a47-185">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="e3a47-186">[Microsoft Teams でのゲストアクセスを](/microsoftteams/guest-access)_参照してください_ 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-186">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="e3a47-187">**フェデレーション/外部** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-187">**Federated/External** .</span></span> <span data-ttu-id="e3a47-188">フェデレーションユーザーは、会議への参加を招待された別の組織の外部 Teams ユーザーです。</span><span class="sxs-lookup"><span data-stu-id="e3a47-188">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="e3a47-189">これらのユーザーは、フェデレーションパートナーとの間に有効な資格情報を持っているため、これらのユーザーは Teams によって認証されたものとして扱われますが、組織からチームや他の共有リソースにアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-189">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="e3a47-190">外部ユーザーが teams やチャネルにアクセスできるようにする場合は、ゲストアクセスの方が適していることがあります。</span><span class="sxs-lookup"><span data-stu-id="e3a47-190">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="e3a47-191">「 [Microsoft Teams で外部アクセスを管理](/microsoftteams/manage-external-access)する _」を参照してください_ 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-191">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="e3a47-192">**匿名** 。</span><span class="sxs-lookup"><span data-stu-id="e3a47-192">**Anonymous** .</span></span> <span data-ttu-id="e3a47-193">匿名ユーザーは、Active Directory id を持たず、テナントと共にフェデレーションされません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-193">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="e3a47-194">匿名の参加者は外部ユーザーのようになりますが、その id は会議に投影されません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-194">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="e3a47-195">匿名ユーザーは、会議ウィンドウでアプリにアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="e3a47-195">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3a47-196">次の手順</span><span class="sxs-lookup"><span data-stu-id="e3a47-196">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3a47-197">Teams 会議用のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="e3a47-197">Create apps for Teams meetings</span></span>](create-apps-for-teams-meetings.md)
