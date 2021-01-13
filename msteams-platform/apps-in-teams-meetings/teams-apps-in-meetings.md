---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
keywords: Teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: 217737cbbf73104d4d78cf817e6df0244229c53c
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797758"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="5d395-104">Teams 会議のアプリ</span><span class="sxs-lookup"><span data-stu-id="5d395-104">Apps in Teams meetings</span></span>

<span data-ttu-id="5d395-105">会議は、Teams の生産性の鍵です。</span><span class="sxs-lookup"><span data-stu-id="5d395-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="5d395-106">共同作業、パートナーシップ、情報に基づいたコミュニケーション、包括的でアクティブなフォーラムでのフィードバックの共有を可能にします。</span><span class="sxs-lookup"><span data-stu-id="5d395-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="5d395-107">開発者は、構成可能なタブ、ボット、[](../bots/what-are-bots.md)およびメッセージ拡張[](../messaging-extensions/what-are-messaging-extensions.md)アプリケーションを作成して、Teams の会議エクスペリエンスを強化および強化できます。 [](../tabs/what-are-tabs.md#how-do-tabs-work)</span><span class="sxs-lookup"><span data-stu-id="5d395-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="5d395-108">会議ユーザーは、タブ ギャラリーを介してアプリにアクセスして、カンバボードの事前設定、会議内の操作可能なダイアログの起動、会議後の投票の作成などの関連シナリオを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="5d395-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="5d395-109">会議アプリは、出席者の状態に基づいて、会議のライフサイクルの各段階でユーザー エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="5d395-110">Teams の会議アプリの拡張性は、次の 3 つの概念を中心に行います。</span><span class="sxs-lookup"><span data-stu-id="5d395-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="5d395-111">✔ **のライフサイクル (会議** の時間枠の前、中、および後) を管理します。</span><span class="sxs-lookup"><span data-stu-id="5d395-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="5d395-112">✔ **参加者の役割** — 会議の開催者、発表者、または出席者。</span><span class="sxs-lookup"><span data-stu-id="5d395-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="5d395-113">✔ **ユーザーの種類** — テナント内、ゲスト、フェデレーション、または匿名の Teams ユーザー。</span><span class="sxs-lookup"><span data-stu-id="5d395-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="5d395-114">会議ライフサイクルのシナリオ</span><span class="sxs-lookup"><span data-stu-id="5d395-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="5d395-115">タブ</span><span class="sxs-lookup"><span data-stu-id="5d395-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d395-116">すべてのタブ アプリケーションと同様に、アプリはタブの Teams [SSO](../tabs/how-to/authentication/auth-aad-sso.md) 認証フローに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d395-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> <span data-ttu-id="5d395-117">モバイル クライアントは、会議前サーフェスと会議後サーフェスでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="5d395-117">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="5d395-118">モバイルでの会議中のエクスペリエンス (会議中のダイアログとパネル) は間もなく利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="5d395-118">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="5d395-119">会議前アプリのエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="5d395-119">Pre-meeting app experience</span></span>

<span data-ttu-id="5d395-120">**会議前のエクスペリエンス:**</span><span class="sxs-lookup"><span data-stu-id="5d395-120">**Pre-meeting experience:**</span></span>

![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="5d395-122">**[会議前] タブ:**</span><span class="sxs-lookup"><span data-stu-id="5d395-122">**Pre-meeting tab:**</span></span>

![会議前タブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="5d395-124">✔アクセス許可を持つユーザーは、次の 2 つの方法でタブ ギャラリーを介して会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-124">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="5d395-125">&emsp;&emsp;&#9679; Teams のスケジュール **フォームの** [詳細] タブを使用します。</span><span class="sxs-lookup"><span data-stu-id="5d395-125">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="5d395-126">&emsp;&emsp;&#9679;既存の会議の **[会議チャット** ] タブを使用します。</span><span class="sxs-lookup"><span data-stu-id="5d395-126">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="5d395-127">✔タブ アプリは、プラスアイコン (➕)ボタンを使用して会議の [詳細] ページと [チャット] ページでアクセスできます。| </span><span class="sxs-lookup"><span data-stu-id="5d395-127">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="5d395-128">✔投票またはアンケートが 10 件を超える場合、タブ レイアウトは整理された状態である必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d395-128">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="5d395-129">会議中アプリのエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="5d395-129">In-meeting app experience</span></span>

<span data-ttu-id="5d395-130">✔アプリは、チャット ウィンドウの上部バーにホストされ、会議内タブから会議内タブエクスペリエンスとしてホストされます。ユーザーがタブ ギャラリーを使用して会議にタブを追加すると、会議のエクスペリエンス中のアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d395-130">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="5d395-131">✔アクセス許可を持つユーザーは、会議中にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-131">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="5d395-132">✔会議のコンテキストで読み込まれると、アプリは Teams クライアント SDK を利用して、エクスペリエンスにアクセスし、適切にレンダリング `meetingId` `userMri` `frameContext` することができます。</span><span class="sxs-lookup"><span data-stu-id="5d395-132">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="5d395-133">✔または投票の結果をエクスポートする場合は、ユーザーに "結果が正常にダウンロードされました" と通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d395-133">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="5d395-134">✔ Teams 会議にアプリを表示するには、次の 2 つの領域を使用します。</span><span class="sxs-lookup"><span data-stu-id="5d395-134">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="5d395-135">&emsp;&emsp;&#9679; **パネル**。</span><span class="sxs-lookup"><span data-stu-id="5d395-135">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="5d395-136">アプリ マニフェスト _で、_ タブがサイド パネル [](create-apps-for-teams-meetings.md#during-a-meeting)用に最適化されている場合、それが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5d395-136">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="5d395-137">また、指定された設計ガイドラインに従って、共有トレイ エクスペリエンスの一部にできます。</span><span class="sxs-lookup"><span data-stu-id="5d395-137">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="5d395-138">&emsp;&emsp;&#9679; **ダイアログを表示します**。</span><span class="sxs-lookup"><span data-stu-id="5d395-138">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="5d395-139">会議内ダイアログを使用して、会議参加者の操作可能なコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="5d395-139">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="5d395-140">*「Teams* [会議用アプリの作成」を参照してください](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="5d395-140">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="5d395-141">**会議中のエクスペリエンス:**</span><span class="sxs-lookup"><span data-stu-id="5d395-141">**In-meeting experience:**</span></span>

![会議内エクスペリエンス](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議内ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="5d395-144">**ユーザーの会議中の操作可能なダイアログ:**</span><span class="sxs-lookup"><span data-stu-id="5d395-144">**In-meeting actionable dialog for users:**</span></span>

![ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="5d395-146">会議後のアプリエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="5d395-146">Post-meeting app experience</span></span>

<span data-ttu-id="5d395-147">**会議後のエクスペリエンス:**</span><span class="sxs-lookup"><span data-stu-id="5d395-147">**Post-meeting experience:**</span></span>

![会議後ビュー](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="5d395-149">✔会議後のアプリのシナリオは、現在の会議後のエクスペリエンスと似ていますが、サーフェス内にタブが存在するという利点があります。</span><span class="sxs-lookup"><span data-stu-id="5d395-149">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="5d395-150">✔アクセス許可を持つユーザーは、Teams のスケジュール フォームの [詳細] タブと既存の会議の [会議チャット] タブを使用して、タブ ギャラリーから会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-150">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="5d395-151">✔投票またはアンケートが 10 件を超える場合、タブ レイアウトは整理された状態である必要があります。</span><span class="sxs-lookup"><span data-stu-id="5d395-151">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="5d395-152">ボット</span><span class="sxs-lookup"><span data-stu-id="5d395-152">Bots</span></span>

<span data-ttu-id="5d395-153">ボットの実装については、Teams 会議のドキュメント [のボットを参照](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) してください。</span><span class="sxs-lookup"><span data-stu-id="5d395-153">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="5d395-154">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="5d395-154">Messaging Extensions</span></span>

<span data-ttu-id="5d395-155">メッセージング拡張機能の実装については、Teams 会議のドキュメントの [メッセージング拡張機能を参照](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) してください。</span><span class="sxs-lookup"><span data-stu-id="5d395-155">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="5d395-156">会議の参加者の役割とユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="5d395-156">Participant roles and user types in a meeting</span></span>

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="5d395-158">参加者の役割</span><span class="sxs-lookup"><span data-stu-id="5d395-158">Participant roles</span></span>

<span data-ttu-id="5d395-159">参加者固有の承認を使用してアプリを設計できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-159">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="5d395-160">たとえば、開催者や発表者だけが会議で投票を作成できるとします。</span><span class="sxs-lookup"><span data-stu-id="5d395-160">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="5d395-161">既定の参加者設定は組織の IT 管理者によって決まりますが、会議の開催者は特定の会議の設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-161">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="5d395-162">開催者は、会議オプション Web ページでこれらの変更を行えます。</span><span class="sxs-lookup"><span data-stu-id="5d395-162">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="5d395-163">**開催者**。</span><span class="sxs-lookup"><span data-stu-id="5d395-163">**Organizer**.</span></span> <span data-ttu-id="5d395-164">開催者が会議をスケジュールし、会議オプションを設定し、会議の役割を割り当て、会議を開始します。</span><span class="sxs-lookup"><span data-stu-id="5d395-164">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="5d395-165">M365 アカウント (Teams ライセンスを所有) を持つユーザーだけが開催者になされ、出席者のアクセス許可を制御できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-165">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="5d395-166">**発表者**。</span><span class="sxs-lookup"><span data-stu-id="5d395-166">**Presenter**.</span></span> <span data-ttu-id="5d395-167">発表者の機能は開催者とほぼ同じです。ただし、発表者は、セッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="5d395-167">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="5d395-168">既定では、会議に参加する参加者は発表者の役割を持っています。</span><span class="sxs-lookup"><span data-stu-id="5d395-168">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="5d395-169">**Attendee**.</span><span class="sxs-lookup"><span data-stu-id="5d395-169">**Attendee**.</span></span> <span data-ttu-id="5d395-170">出席者とは、会議に招待されているが、発表者として機能する権限が与えされていないユーザーです。</span><span class="sxs-lookup"><span data-stu-id="5d395-170">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="5d395-171">出席者は他の会議メンバーと対話できますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="5d395-171">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="5d395-172"> [ **「Teams 会議での役割」を参照**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="5d395-172">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="5d395-173">[会議オプション]  **ページには、次** のようにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5d395-173">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="5d395-174">&#11200; Teams で、[予定表のロゴ] に移動し、会議を選択して、[会議オプション] ![ ](../assets/images/apps-in-meetings/calendar-logo.png) **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="5d395-174">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="5d395-175">&#11200;会議出席依頼で、[会議オプション] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="5d395-175">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="5d395-176">&#11200;会議中に、会議コントロールの \*\*[参加者\*\* に参加者 ![ を表示する] ](../assets/images/apps-in-meetings/show-participants.png) アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="5d395-176">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="5d395-177">次に、参加者の一覧の上で、[アクセス許可の管理 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="5d395-177">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="5d395-178">ユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="5d395-178">User types</span></span>

> [!NOTE]
> <span data-ttu-id="5d395-179">ユーザーの種類は会議に参加し、上記の参加者の役割のいずれかを想定できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-179">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="5d395-180">ユーザーの種類は **、getParticipantRole** API の一部として公開されません。</span><span class="sxs-lookup"><span data-stu-id="5d395-180">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="5d395-181">**テナント内。**</span><span class="sxs-lookup"><span data-stu-id="5d395-181">**In-tenant**.</span></span> <span data-ttu-id="5d395-182">これらのユーザーは組織に属し、テナントの Azure Active Directory の資格情報を持っています。</span><span class="sxs-lookup"><span data-stu-id="5d395-182">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="5d395-183">通常、フルタイム、オンサイト、またはリモートの従業員です。</span><span class="sxs-lookup"><span data-stu-id="5d395-183">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="5d395-184">**ゲスト 。**</span><span class="sxs-lookup"><span data-stu-id="5d395-184">**Guest**.</span></span> <span data-ttu-id="5d395-185">ゲストとは、Teams または組織のテナント内の他のリソースにアクセスするために招待された別の組織の参加者です。</span><span class="sxs-lookup"><span data-stu-id="5d395-185">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="5d395-186">ゲストは組織の Active Directory に追加され、チーム チャット、会議、ファイルにフル アクセスできるネイティブ チーム メンバーと同じ Teams 機能をほぼすべて提供できます。</span><span class="sxs-lookup"><span data-stu-id="5d395-186">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="5d395-187"> [Microsoft Teams でのゲスト アクセスを確認する](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="5d395-187">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="5d395-188">**フェデレーション/外部**。</span><span class="sxs-lookup"><span data-stu-id="5d395-188">**Federated/External**.</span></span> <span data-ttu-id="5d395-189">フェデレーション ユーザーとは、会議への参加を招待された別の組織の外部 Teams ユーザーです。</span><span class="sxs-lookup"><span data-stu-id="5d395-189">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="5d395-190">これらのユーザーはフェデレーション パートナーとの有効な資格情報を持つので、Teams によって認証済みとして扱われるが、チームや組織の他の共有リソースにアクセスできない。</span><span class="sxs-lookup"><span data-stu-id="5d395-190">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="5d395-191">外部ユーザーにチームとチャネルへのアクセスを許可する場合は、ゲスト アクセスの方が優れたオプションである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5d395-191">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="5d395-192">_「Microsoft_ [Teams での外部アクセスの管理」を参照](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="5d395-192">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="5d395-193">**匿名**。</span><span class="sxs-lookup"><span data-stu-id="5d395-193">**Anonymous**.</span></span> <span data-ttu-id="5d395-194">匿名ユーザーは Active Directory ID を持ち、テナントとフェデレーションされません。</span><span class="sxs-lookup"><span data-stu-id="5d395-194">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="5d395-195">匿名参加者は外部ユーザーに似たユーザーですが、その ID は会議に投影されません。</span><span class="sxs-lookup"><span data-stu-id="5d395-195">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="5d395-196">匿名ユーザーは、会議ウィンドウでアプリにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5d395-196">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d395-197">次の手順</span><span class="sxs-lookup"><span data-stu-id="5d395-197">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d395-198">アプリをデザインする</span><span class="sxs-lookup"><span data-stu-id="5d395-198">Design your app</span></span>](create-apps-for-teams-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="5d395-199">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="5d395-199">Build your app</span></span>](create-apps-for-teams-meetings.md)
