---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 51fe2e0ebdaa56197bbebd1e5dbcf90698fb1f92
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753554"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="44164-104">Teams 会議のアプリ</span><span class="sxs-lookup"><span data-stu-id="44164-104">Apps in Teams meetings</span></span>

<span data-ttu-id="44164-105">会議は Teams の生産性の重要なポイントです。</span><span class="sxs-lookup"><span data-stu-id="44164-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="44164-106">包括的でアクティブなフォーラムで、コラボレーション、パートナーシップ、情報に基づいたコミュニケーション、共有フィードバックを有効にします。</span><span class="sxs-lookup"><span data-stu-id="44164-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="44164-107">開発者は、Teams 会議のエクスペリエンスを強化[](../bots/what-are-bots.md)し、強化[](../messaging-extensions/what-are-messaging-extensions.md)するために、構成可能なタブ、ボット、およびメッセージ拡張アプリケーションを作成できます。 [](../tabs/what-are-tabs.md#how-do-tabs-work)</span><span class="sxs-lookup"><span data-stu-id="44164-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="44164-108">会議ユーザーは、タブ ギャラリーを介してアプリにアクセスして、かんばんボードの事前ステージング、会議中の操作可能なダイアログの起動、会議後のポーリングの作成など、関連するシナリオを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="44164-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="44164-109">会議アプリは、出席者の状態に基づいて、会議ライフサイクルの各ステージのユーザー エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="44164-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="44164-110">Teams の会議アプリの機能拡張は、次の 3 つの概念を中心に行います。</span><span class="sxs-lookup"><span data-stu-id="44164-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="44164-111">**✔、会議の時間の** 前、中、および後の会議のライフサイクルを設定します。</span><span class="sxs-lookup"><span data-stu-id="44164-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="44164-112">✔ **参加者の役割** - 会議の開催者、発表者、または出席者。</span><span class="sxs-lookup"><span data-stu-id="44164-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="44164-113">✔ **ユーザーの種類** ( テナント内、ゲスト、フェデレーション、または匿名の Teams ユーザー)。</span><span class="sxs-lookup"><span data-stu-id="44164-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="44164-114">会議のライフサイクル シナリオ</span><span class="sxs-lookup"><span data-stu-id="44164-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="44164-115">タブ</span><span class="sxs-lookup"><span data-stu-id="44164-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44164-116">すべてのタブ アプリケーションと同様に、アプリはタブの Teams [SSO 認証フローに従う](../tabs/how-to/authentication/auth-aad-sso.md) 必要があります。</span><span class="sxs-lookup"><span data-stu-id="44164-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="44164-117">モバイル クライアントは、会議前および会議後のサーフェスでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="44164-117">Mobile clients support tabs only in pre-meeting and post-meeting surfaces.</span></span> <span data-ttu-id="44164-118">会議中のダイアログやモバイル上のパネルなどの会議中のエクスペリエンスは、近日利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="44164-118">The in-meeting experiences, such as in-meeting dialog and panel on mobile will be available soon.</span></span>
> * <span data-ttu-id="44164-119">アプリは、プライベートスケジュールされた会議でのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="44164-119">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="44164-120">会議前アプリのエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="44164-120">Pre-meeting app experience</span></span>

<span data-ttu-id="44164-121">**会議前のエクスペリエンス:**</span><span class="sxs-lookup"><span data-stu-id="44164-121">**Pre-meeting experience:**</span></span>

![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="44164-123">**[会議前] タブ:**</span><span class="sxs-lookup"><span data-stu-id="44164-123">**Pre-meeting tab:**</span></span>

![会議前のタブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="44164-125">✔アクセス許可ユーザーは、次の 2 つの方法でタブ ギャラリーを介して会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="44164-125">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="44164-126">&emsp;&emsp;&#9679; Teams スケジュール **フォームの [** 詳細] タブを使用します。</span><span class="sxs-lookup"><span data-stu-id="44164-126">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="44164-127">&emsp;&emsp;&#9679;既存の会議の **[会議チャット** ] タブを使用します。</span><span class="sxs-lookup"><span data-stu-id="44164-127">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="44164-128">✔ タブ アプリは、プラス アイコン(➕) ボタンを使用して会議の詳細ページとチャット ページでアクセスできます。| </span><span class="sxs-lookup"><span data-stu-id="44164-128">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="44164-129">✔が 10 件を超える場合は、タブ レイアウトが整理された状態である必要があります。</span><span class="sxs-lookup"><span data-stu-id="44164-129">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="44164-130">会議中のアプリ エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="44164-130">In-meeting app experience</span></span>

<span data-ttu-id="44164-131">✔会議アプリは、チャット ウィンドウの上部バーでホストされ、会議内タブエクスペリエンスとして会議内タブエクスペリエンスとしてホストされます。ユーザーがタブ ギャラリーを通じて会議にタブを追加すると、会議のエクスペリエンス中のアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="44164-131">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="44164-132">✔アクセス許可を持つユーザーは、会議中にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="44164-132">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="44164-133">✔会議のコンテキストに読み込まれると、アプリは Teams クライアント SDK を利用して 、アクセスし、エクスペリエンスを適切に `meetingId` `userMri` `frameContext` レンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="44164-133">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="44164-134">✔アンケートまたはアンケートの結果をエクスポートすると、ユーザーに「結果が正常にダウンロードされました」と通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44164-134">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="44164-135">✔ 2 つの領域で Teams 会議にアプリを表示するには、次の 2 つの領域を使用します。</span><span class="sxs-lookup"><span data-stu-id="44164-135">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="44164-136">&emsp;&emsp;&#9679; **サイド パネル**。</span><span class="sxs-lookup"><span data-stu-id="44164-136">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="44164-137">アプリ マニフェスト _でタブ_ がサイド パネル用 [](create-apps-for-teams-meetings.md#during-a-meeting)に最適化されている場合、それが表示される場所です。</span><span class="sxs-lookup"><span data-stu-id="44164-137">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="44164-138">また、指定された設計ガイドラインに従って、共有トレイエクスペリエンスの一部になれ得る。</span><span class="sxs-lookup"><span data-stu-id="44164-138">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="44164-139">&emsp;&emsp;&#9679; **会議中ダイアログ を開きます**。</span><span class="sxs-lookup"><span data-stu-id="44164-139">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="44164-140">会議の参加者に対してアクション可能なコンテンツを表示するには、会議内ダイアログを使用します。</span><span class="sxs-lookup"><span data-stu-id="44164-140">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="44164-141">*「Create* [Apps for Teams 会議」を参照してください](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="44164-141">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="44164-142">**会議中のエクスペリエンス:**</span><span class="sxs-lookup"><span data-stu-id="44164-142">**In-meeting experience:**</span></span>

![会議中のエクスペリエンス](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議内ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="44164-145">**ユーザーの会議中の操作可能なダイアログ:**</span><span class="sxs-lookup"><span data-stu-id="44164-145">**In-meeting actionable dialog for users:**</span></span>

![ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="44164-147">会議後のアプリ エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="44164-147">Post-meeting app experience</span></span>

<span data-ttu-id="44164-148">**会議後のエクスペリエンス:**</span><span class="sxs-lookup"><span data-stu-id="44164-148">**Post-meeting experience:**</span></span>

![会議ビューの投稿](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="44164-150">✔会議後アプリのシナリオは、現在の会議後のエクスペリエンスと似ています。表面内にタブが存在する利点が追加されています。</span><span class="sxs-lookup"><span data-stu-id="44164-150">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="44164-151">✔権限を持つユーザーは、[Teams のスケジュール] フォームの [詳細] タブと既存の会議の [会議チャット] タブを使用して、タブ ギャラリーから会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="44164-151">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="44164-152">✔が 10 件を超える場合は、タブ レイアウトが整理された状態である必要があります。</span><span class="sxs-lookup"><span data-stu-id="44164-152">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="44164-153">ボット</span><span class="sxs-lookup"><span data-stu-id="44164-153">Bots</span></span>

<span data-ttu-id="44164-154">ボットの実装については、ボットの [ビルドから始め](../build-your-first-app/build-bot.md) 、Teams 会議用 [のアプリの作成を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="44164-154">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="44164-155">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="44164-155">Messaging extensions</span></span>

<span data-ttu-id="44164-156">メッセージング拡張機能の実装では、まずメッセージング [拡張機能を](../messaging-extensions/how-to/create-messaging-extension.md) ビルドしてから、Teams 会議用のアプリの作成 [を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="44164-156">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="44164-157">会議の参加者の役割とユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="44164-157">Participant roles and user types in a meeting</span></span>

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="44164-159">参加者の役割</span><span class="sxs-lookup"><span data-stu-id="44164-159">Participant roles</span></span>

<span data-ttu-id="44164-160">参加者固有の承認を使用してアプリを設計できます。</span><span class="sxs-lookup"><span data-stu-id="44164-160">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="44164-161">たとえば、開催者や発表者だけが会議で投票を作成できる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="44164-161">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="44164-162">既定の参加者設定は組織の IT 管理者によって決まりますが、会議の開催者は特定の会議の設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="44164-162">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="44164-163">開催者は、[会議のオプション] Web ページでこれらの変更を行えます。</span><span class="sxs-lookup"><span data-stu-id="44164-163">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="44164-164">**オーガナイザー**.</span><span class="sxs-lookup"><span data-stu-id="44164-164">**Organizer**.</span></span> <span data-ttu-id="44164-165">開催者は会議をスケジュールし、会議のオプションを設定し、会議の役割を割り当て、会議を開始します。</span><span class="sxs-lookup"><span data-stu-id="44164-165">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="44164-166">M365 アカウントを持つユーザー (Teams ライセンスを所有している) のみを開催者にし、出席者のアクセス許可を制御できます。</span><span class="sxs-lookup"><span data-stu-id="44164-166">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="44164-167">**発表者**.</span><span class="sxs-lookup"><span data-stu-id="44164-167">**Presenter**.</span></span> <span data-ttu-id="44164-168">発表者は、開催者とほぼ同じ機能を持っています。ただし、発表者はセッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="44164-168">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="44164-169">既定では、会議に参加する参加者には発表者の役割があります。</span><span class="sxs-lookup"><span data-stu-id="44164-169">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="44164-170">**出席者**。</span><span class="sxs-lookup"><span data-stu-id="44164-170">**Attendee**.</span></span> <span data-ttu-id="44164-171">出席者とは、会議に出席するために招待されたが、発表者として機能する権限を持つユーザーです。</span><span class="sxs-lookup"><span data-stu-id="44164-171">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="44164-172">出席者は他の会議メンバーとやり取りできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="44164-172">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="44164-173">_「Teams_ [**会議での役割」を参照してください。**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="44164-173">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="44164-174">[会議のオプション]  **ページには、次** のようにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="44164-174">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="44164-175">&#11200; Teams で、[ **予定表の予定表** のロゴ] に移動し、 ![ 会議を ](../assets/images/apps-in-meetings/calendar-logo.png) 選択し、[会議のオプション] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="44164-175">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="44164-176">&#11200;会議出席依頼で、[会議のオプション] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="44164-176">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="44164-177">&#11200;会議中に、[会議コントロールに参加者 ![ を表示する] ](../assets/images/apps-in-meetings/show-participants.png) アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="44164-177">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="44164-178">次に、参加者の一覧の上で、[アクセス許可の **管理] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="44164-178">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="44164-179">ユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="44164-179">User types</span></span>

> [!NOTE]
> <span data-ttu-id="44164-180">ユーザーの種類は、会議に参加し、上記のいずれかの参加者の役割を引き受け取ります。</span><span class="sxs-lookup"><span data-stu-id="44164-180">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="44164-181">User 型は **getParticipantRole** API の一部として公開されません。</span><span class="sxs-lookup"><span data-stu-id="44164-181">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="44164-182">**テナント内**。</span><span class="sxs-lookup"><span data-stu-id="44164-182">**In-tenant**.</span></span> <span data-ttu-id="44164-183">これらのユーザーは組織に属し、テナントの Azure Active Directory の資格情報を持ちます。</span><span class="sxs-lookup"><span data-stu-id="44164-183">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="44164-184">通常、フルタイム、オンサイト、またはリモートの従業員です。</span><span class="sxs-lookup"><span data-stu-id="44164-184">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="44164-185">**ゲスト**。</span><span class="sxs-lookup"><span data-stu-id="44164-185">**Guest**.</span></span> <span data-ttu-id="44164-186">ゲストは、組織のテナント内の Teams または他のリソースにアクセスするために招待された別の組織の参加者です。</span><span class="sxs-lookup"><span data-stu-id="44164-186">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="44164-187">ゲストは組織の Active Directory に追加され、チーム チャット、会議、ファイルにフル アクセスできるネイティブ チーム メンバーと同じ Teams 機能をほぼすべて提供できます。</span><span class="sxs-lookup"><span data-stu-id="44164-187">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="44164-188">_「Microsoft_ [Teams のゲスト アクセス」を参照してください。](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="44164-188">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="44164-189">**フェデレーション/外部**.</span><span class="sxs-lookup"><span data-stu-id="44164-189">**Federated/External**.</span></span> <span data-ttu-id="44164-190">フェデレーション ユーザーは、会議への参加を招待された別の組織の外部 Teams ユーザーです。</span><span class="sxs-lookup"><span data-stu-id="44164-190">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="44164-191">これらのユーザーはフェデレーション パートナーと有効な資格情報を持つので、Teams によって認証されますが、組織からチームや他の共有リソースにアクセスできないと処理されます。</span><span class="sxs-lookup"><span data-stu-id="44164-191">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="44164-192">外部ユーザーにチームとチャネルへのアクセスを許可する場合は、ゲスト アクセスの方が良いオプションになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="44164-192">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="44164-193">_「Microsoft_ [Teams での外部アクセスの管理」を参照してください。](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="44164-193">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="44164-194">**匿名**.</span><span class="sxs-lookup"><span data-stu-id="44164-194">**Anonymous**.</span></span> <span data-ttu-id="44164-195">匿名ユーザーは Active Directory ID を持ち、テナントとフェデレーションされません。</span><span class="sxs-lookup"><span data-stu-id="44164-195">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="44164-196">匿名参加者は外部ユーザーに似ていましたが、その ID は会議に投影されません。</span><span class="sxs-lookup"><span data-stu-id="44164-196">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="44164-197">匿名ユーザーは、会議ウィンドウでアプリにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="44164-197">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44164-198">次の手順</span><span class="sxs-lookup"><span data-stu-id="44164-198">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="44164-199">アプリをデザインする</span><span class="sxs-lookup"><span data-stu-id="44164-199">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="44164-200">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="44164-200">Build your app</span></span>](create-apps-for-teams-meetings.md)
