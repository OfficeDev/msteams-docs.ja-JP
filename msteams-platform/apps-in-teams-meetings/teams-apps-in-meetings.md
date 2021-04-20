---
title: Teams 会議のアプリ
author: laujan
description: 参加者とユーザーの役割に基づく Teams 会議のアプリの概要
ms.topic: overview
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 201fa58cc375440cf6c495028135e32fd51f740c
ms.sourcegitcommit: ee8c4800da3b3569d80c6f3661a2f20aa1f2c5e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2021
ms.locfileid: "51885081"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="130db-104">Teams 会議のアプリ</span><span class="sxs-lookup"><span data-stu-id="130db-104">Apps in Teams meetings</span></span>

<span data-ttu-id="130db-105">会議では、包括的でアクティブなフォーラムで、共同作業、パートナーシップ、情報に基づいたコミュニケーション、共有フィードバックが可能になります。</span><span class="sxs-lookup"><span data-stu-id="130db-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="130db-106">会議アプリは、出席者の状態に応じて、会議前、会議中、会議後のアプリ エクスペリエンスなど、会議のライフサイクルの各段階でユーザー エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="130db-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="130db-107">Teams のエンド ユーザーは、次に示すタブ ギャラリーを使用して会議中にアプリにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="130db-107">Teams end-users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="130db-108">かんばんボードの事前ステージ</span><span class="sxs-lookup"><span data-stu-id="130db-108">Pre-stage a Kanban board</span></span>
* <span data-ttu-id="130db-109">会議内の操作可能なダイアログを起動する</span><span class="sxs-lookup"><span data-stu-id="130db-109">Launch an in-meeting actionable dialog</span></span>
* <span data-ttu-id="130db-110">会議後のポーリングを作成する</span><span class="sxs-lookup"><span data-stu-id="130db-110">Create a post-meeting poll</span></span>

<span data-ttu-id="130db-111">Teams の会議アプリの機能拡張は、次の概念に基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="130db-111">Teams’ meeting app extensibility is based on the following concepts:</span></span>

<span data-ttu-id="130db-112">✔のライフサイクルには、会議の時間枠の前、中、後などのステージがあります。</span><span class="sxs-lookup"><span data-stu-id="130db-112">✔ Meeting lifecycle has stages such as before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="130db-113">✔開催者、発表者、出席者などの会議の参加者の役割。</span><span class="sxs-lookup"><span data-stu-id="130db-113">✔ Participant roles in a meeting such as meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="130db-114">✔、ゲスト、フェデレーション、匿名の Teams ユーザーなどの会議のユーザーの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="130db-114">✔ User types in a meeting such as in-tenant, guest, federated, or anonymous Teams user.</span></span>

<span data-ttu-id="130db-115">この記事では、会議のライフサイクルと、タブ、ボット、メッセージング拡張機能を会議に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="130db-115">This article covers information about the meeting lifecycle and how to integrate tabs, bots, and messaging extensions in your meeting.</span></span> <span data-ttu-id="130db-116">また、参加者の役割を識別し、さまざまなユーザーの種類を使用してタスクを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="130db-116">It also enables you to identify participant roles and also use different user types to perform tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="130db-117">会議アプリの機能拡張機能を使用するには、適切なアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="130db-117">To work with the meeting app extensibility features, you must have the appropriate permissions.</span></span>

### <a name="meeting-lifecycle"></a><span data-ttu-id="130db-118">会議のライフサイクル</span><span class="sxs-lookup"><span data-stu-id="130db-118">Meeting lifecycle</span></span>

<span data-ttu-id="130db-119">会議のライフサイクルは、会議前、会議中、会議後のアプリ エクスペリエンスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="130db-119">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="130db-120">会議のライフサイクルの各段階で、タブ、ボット、メッセージング拡張機能を統合できます。</span><span class="sxs-lookup"><span data-stu-id="130db-120">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="130db-121">タブを会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="130db-121">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="130db-122">タブを使用すると、チーム メンバーはチャネルまたはチャット内の特定の領域のサービスとコンテンツにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="130db-122">Tabs allow team members to access services and content in a specific space within a channel or chat.</span></span> <span data-ttu-id="130db-123">これにより、チームはタブを直接処理し、タブ内で使用可能なツールとデータに関する会話を行います。</span><span class="sxs-lookup"><span data-stu-id="130db-123">This lets the team work directly with tabs and have conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="130db-124">Teams 会議で、ユーザーはプラスを選択してタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="130db-124">In Teams meeting, users can add a tab by selecting plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="130db-125">をクリックし、タブとしてインストールするアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="130db-125">, and choosing the app that they want to install as a tab.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="130db-126">タブを会議に統合している場合、アプリはタブの Teams シングル サインオン [(SSO) 認証フロー](../tabs/how-to/authentication/auth-aad-sso.md) に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="130db-126">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="130db-127">モバイル クライアントは、会議の開催前と開催後のステージでのみタブをサポートします。</span><span class="sxs-lookup"><span data-stu-id="130db-127">Mobile clients support tabs only in pre and post meeting stages.</span></span> <span data-ttu-id="130db-128">現在、会議中のダイアログとパネルである会議中のエクスペリエンスは、モバイルでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="130db-128">The in-meeting experiences that is in-meeting dialog and panel are currently not available on mobile.</span></span>
> * <span data-ttu-id="130db-129">アプリは、プライベートスケジュールされた会議でのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="130db-129">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="130db-130">会議前アプリのエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="130db-130">Pre-meeting app experience</span></span>

<span data-ttu-id="130db-131">**会議前のエクスペリエンス:**</span><span class="sxs-lookup"><span data-stu-id="130db-131">**Pre-meeting experience:**</span></span>

![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="130db-133">**[会議前] タブ:**</span><span class="sxs-lookup"><span data-stu-id="130db-133">**Pre-meeting tab:**</span></span>

![会議前のタブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="130db-135">✔アクセス許可ユーザーとは、会議のライフサイクルの異なる段階で会議にアプリを追加できるユーザーです。</span><span class="sxs-lookup"><span data-stu-id="130db-135">✔ Permissioned users are users who can add apps to a meeting during different stages of the meeting lifecycle.</span></span> <span data-ttu-id="130db-136">これらのユーザーは、次の 2 つの方法でタブ ギャラリーを介して会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="130db-136">These users can add apps to a meeting through the tab gallery in two ways:</span></span>

   * <span data-ttu-id="130db-137">[Teams の **スケジュール設定]** フォームの [詳細] タブを使用します。</span><span class="sxs-lookup"><span data-stu-id="130db-137">Using the **Details** tab on the Teams scheduling form.</span></span>

   * <span data-ttu-id="130db-138">既存の会議 **で [** 会議チャット] タブを使用する。</span><span class="sxs-lookup"><span data-stu-id="130db-138">Using the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="130db-139">✔タブ アプリは、プラスボタンを使用して会議の詳細ページとチャット ページ➕できます。</span><span class="sxs-lookup"><span data-stu-id="130db-139">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus ➕ button.</span></span>

<span data-ttu-id="130db-140">✔が 10 件を超える場合は、タブ レイアウトが整理された状態である必要があります。</span><span class="sxs-lookup"><span data-stu-id="130db-140">✔ Tab layout must be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="130db-141">会議中のアプリ エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="130db-141">In-meeting app experience</span></span>

<span data-ttu-id="130db-142">✔アプリは、チャット ウィンドウの上部バーでホストされ、会議内タブを使用して会議内タブエクスペリエンスとしてホストされます。ユーザーがタブ ギャラリーを通じて会議にタブを追加すると、会議のエクスペリエンス中の **アプリが** 表示されます。</span><span class="sxs-lookup"><span data-stu-id="130db-142">✔ Meeting apps are hosted in the top upper bar of the chat window and as in-meeting tab experience using the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences are shown.</span></span>

<span data-ttu-id="130db-143">✔アクセス許可を持つユーザーは、会議中にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="130db-143">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="130db-144">✔会議のコンテキストで読み込まれると、アプリは Teams クライアント SDK を利用して 、 にアクセスし、エクスペリエンスを適切に `meetingId` `userMri` `frameContext` レンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="130db-144">✔ When loaded in the context of a meeting, apps can leverage the Teams client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="130db-145">✔アンケートまたはポーリングの結果をエクスポートすると、結果が正常にダウンロードされたことをユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="130db-145">✔ Exporting a result of a survey or poll notifies the users that the results successfully downloaded.</span></span>

<span data-ttu-id="130db-146">✔サイド パネルまたは会議内ダイアログ ボックスの Teams 会議にアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="130db-146">✔ An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span> <span data-ttu-id="130db-147">会議の参加者に対してアクション可能なコンテンツを紹介するには、会議内ダイアログ ボックスを使用します。</span><span class="sxs-lookup"><span data-stu-id="130db-147">Use the in-meeting dialog box to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="130db-148">詳細については [、「Create apps for Teams meetings」を参照してください](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="130db-148">For more information, see [create apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="130db-149">アプリ マニフェストは、タブがサイド[](create-apps-for-teams-meetings.md#during-a-meeting)パネル用に最適化され、表示される場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="130db-149">Your app manifest specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it is displayed.</span></span> <span data-ttu-id="130db-150">また、指定された設計ガイドラインに従って、共有トレイエクスペリエンスの一部になれ得る。</span><span class="sxs-lookup"><span data-stu-id="130db-150">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="130db-151">次の画像は、アプリを会議中のダイアログ ボックスとして、別のサイド パネルとして表示します。</span><span class="sxs-lookup"><span data-stu-id="130db-151">The following images display the app as an in-meeting dialog box and as a separate side panel:</span></span>

![会議中のエクスペリエンス](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会議内ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a><span data-ttu-id="130db-154">ユーザーの会議中の操作可能なダイアログ</span><span class="sxs-lookup"><span data-stu-id="130db-154">In-meeting actionable dialog for users</span></span>

![ダイアログ ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="130db-156">会議後のアプリ エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="130db-156">Post-meeting app experience</span></span>

![会議ビューの投稿](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="130db-158">✔会議後アプリのシナリオは、現在の会議後のエクスペリエンスと似ています。表面内にタブが存在する利点が追加されています。</span><span class="sxs-lookup"><span data-stu-id="130db-158">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span>

<span data-ttu-id="130db-159">✔権限を持つユーザーは、[Teams のスケジュール] フォームの [詳細] タブと既存の会議の[会議チャット] タブを使用して、タブ ギャラリーから会議にアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="130db-159">✔ Permissioned users can add apps from the tab gallery to a meeting using the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="130db-160">✔が 10 件を超える場合は、タブ レイアウトを整理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="130db-160">✔  Tab layout must be organized when there are more than ten polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="130db-161">ボットを会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="130db-161">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="130db-162">ボットの実装については、ボットの [ビルドから始め](../build-your-first-app/build-bot.md) 、Teams 会議用 [のアプリの作成を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="130db-162">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="130db-163">メッセージング拡張機能を会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="130db-163">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="130db-164">メッセージング拡張機能の実装では、まずメッセージング [拡張機能を](../messaging-extensions/how-to/create-messaging-extension.md) ビルドしてから、Teams 会議用のアプリの作成 [を続行します](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="130db-164">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="130db-165">会議の参加者の役割とユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="130db-165">Participant roles and user types in a meeting</span></span>

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="130db-167">参加者の役割</span><span class="sxs-lookup"><span data-stu-id="130db-167">Participant roles</span></span>

<span data-ttu-id="130db-168">既定の参加者設定は、組織の IT 管理者によって決まります。</span><span class="sxs-lookup"><span data-stu-id="130db-168">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="130db-169">会議の参加者の役割を次に示します。</span><span class="sxs-lookup"><span data-stu-id="130db-169">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="130db-170">**開催** 者 : 開催者は会議をスケジュールし、会議のオプションを設定し、会議の役割を割り当て、会議を開始します。</span><span class="sxs-lookup"><span data-stu-id="130db-170">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="130db-171">Teams ライセンスを持つ M365 アカウントを持つユーザーだけが開催者として使用し、出席者のアクセス許可を制御できます。</span><span class="sxs-lookup"><span data-stu-id="130db-171">Only users with a M365 account with a Teams license can be organizers and control attendee permissions.</span></span> <span data-ttu-id="130db-172">会議の開催者は、特定の会議の設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="130db-172">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="130db-173">開催者は、[会議のオプション] Web ページ **でこれらの変更を** 行えます。</span><span class="sxs-lookup"><span data-stu-id="130db-173">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="130db-174">**発表者**: 発表者は開催者と同じ機能を持っています。</span><span class="sxs-lookup"><span data-stu-id="130db-174">**Presenter**: Presenters have the same capabilities as organizer.</span></span> <span data-ttu-id="130db-175">ただし、発表者はセッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="130db-175">However, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="130db-176">既定では、会議に参加する参加者には発表者の役割があります。</span><span class="sxs-lookup"><span data-stu-id="130db-176">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="130db-177">**出席者**: 出席者とは、会議に出席するために招待されたが、発表者として機能する権限を持つユーザーです。</span><span class="sxs-lookup"><span data-stu-id="130db-177">**Attendee**: An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="130db-178">出席者は他の会議メンバーとやり取りできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="130db-178">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="130db-179">アプリを追加、削除、またはアンインストールできるのは、開催者または発表者のみです。</span><span class="sxs-lookup"><span data-stu-id="130db-179">Only an organizer or presenter can add, remove, or uninstall apps.</span></span> <span data-ttu-id="130db-180">開催者または発表者だけが会議でポーリングを作成できます。</span><span class="sxs-lookup"><span data-stu-id="130db-180">Only organizer or presenter can create polls in a meeting.</span></span>

<span data-ttu-id="130db-181">詳細については [、「Teams 会議の役割」を参照してください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="130db-181">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="130db-182">[会議のオプション]  **ページには、次** のようにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="130db-182">You can access the  **Meeting options** page as follows:</span></span>

* <span data-ttu-id="130db-183">Teams で、[予定表] の **ロゴに** ![ 移動し ](../assets/images/apps-in-meetings/calendar-logo.png) 、会議を選択し、[会議のオプション] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="130db-183">In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

* <span data-ttu-id="130db-184">会議出席依頼で、[会議のオプション] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="130db-184">In a meeting invitation, select **Meeting options**.</span></span>

* <span data-ttu-id="130db-185">会議中に、[会議コントロールに **参加者** ![ を表示する ](../assets/images/apps-in-meetings/show-participants.png) ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="130db-185">During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="130db-186">次に、参加者の一覧の上で、[アクセス許可の **管理] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="130db-186">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="130db-187">ユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="130db-187">User types</span></span>

> [!NOTE]
> <span data-ttu-id="130db-188">特定のユーザーの種類が割り当てられているユーザーは、会議に参加し、参加者の役割で説明されている参加者の役割の 1 つを [引き受け取ります](#participant-roles)。</span><span class="sxs-lookup"><span data-stu-id="130db-188">Users with specific user types assigned to them can join meetings and assume one of the participant roles described in [participant roles](#participant-roles).</span></span> <span data-ttu-id="130db-189">ユーザーの種類は **getParticipantRole** API には含まれません。</span><span class="sxs-lookup"><span data-stu-id="130db-189">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="130db-190">次のユーザーの種類は、各ユーザーが実行できる操作と、ユーザーがアクセスできる操作を識別します。</span><span class="sxs-lookup"><span data-stu-id="130db-190">The following user types identify what each user can do and what they can access:</span></span>

* <span data-ttu-id="130db-191">**テナント内 :** テナント内ユーザーは組織に属し、テナントの Azure Active Directory (AAD) に資格情報を持ちます。</span><span class="sxs-lookup"><span data-stu-id="130db-191">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="130db-192">通常、フルタイム、オンサイト、またはリモートの従業員です。</span><span class="sxs-lookup"><span data-stu-id="130db-192">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="130db-193">テナント内のユーザーには、開催者、発表者、または出席者を指定できます。</span><span class="sxs-lookup"><span data-stu-id="130db-193">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="130db-194">**ゲスト**: ゲストは、Teams または組織のテナント内の他のリソースにアクセスするために招待された別の組織の参加者です。</span><span class="sxs-lookup"><span data-stu-id="130db-194">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="130db-195">ゲストは組織の AAD に追加され、チーム チャット、会議、ファイルにアクセスできるネイティブ チーム メンバーと同じ Teams 機能を持ちます。</span><span class="sxs-lookup"><span data-stu-id="130db-195">Guests are added to your organization’s AAD and have the same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="130db-196">ゲスト ユーザーには、開催者、発表者、または出席者を指定できます。</span><span class="sxs-lookup"><span data-stu-id="130db-196">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="130db-197">詳細については [、「Teams でのゲスト アクセス」を参照してください](/microsoftteams/guest-access)。</span><span class="sxs-lookup"><span data-stu-id="130db-197">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="130db-198">**フェデレーションまたは外部**: フェデレーション ユーザーとは、会議への参加を招待された別の組織の外部 Teams ユーザーです。</span><span class="sxs-lookup"><span data-stu-id="130db-198">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="130db-199">これらのユーザーは、フェデレーション パートナーと有効な資格情報を持ち、Teams によって承認されています。</span><span class="sxs-lookup"><span data-stu-id="130db-199">These users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="130db-200">組織からチームや他の共有リソースにアクセスできない。</span><span class="sxs-lookup"><span data-stu-id="130db-200">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="130db-201">ゲスト アクセスは、外部ユーザーがチームとチャネルにアクセスできる優れたオプションです。</span><span class="sxs-lookup"><span data-stu-id="130db-201">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="130db-202">詳細については、「Teams での外部 [アクセスの管理」を参照してください](/microsoftteams/manage-external-access)。</span><span class="sxs-lookup"><span data-stu-id="130db-202">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>
* <span data-ttu-id="130db-203">**匿名**: 匿名ユーザーは AAD ID を持ち、テナントとフェデレーションされません。</span><span class="sxs-lookup"><span data-stu-id="130db-203">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="130db-204">匿名参加者は外部ユーザーに似ていましたが、その ID は会議に投影されません。</span><span class="sxs-lookup"><span data-stu-id="130db-204">The anonymous participant is like an external user, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="130db-205">匿名ユーザーは開催者にすることはできませんが、発表者または出席者にできます。</span><span class="sxs-lookup"><span data-stu-id="130db-205">An anonymous user cannot be an organizer but can be a presenter or an attendee.</span></span>

> [!NOTE]
> <span data-ttu-id="130db-206">匿名ユーザーは、グローバル既定のユーザー レベルのアプリアクセス許可ポリシーを継承します。</span><span class="sxs-lookup"><span data-stu-id="130db-206">Anonymous users inherit the global default user-level app permission policy.</span></span> <span data-ttu-id="130db-207">詳細については、「アプリの管理 [」を参照してください](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。</span><span class="sxs-lookup"><span data-stu-id="130db-207">For more information, see [Manage Apps](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).</span></span>

<span data-ttu-id="130db-208">次の表に、ユーザーの種類と、各ユーザーがアクセスできる機能を示します。</span><span class="sxs-lookup"><span data-stu-id="130db-208">The following table provides the user types and what features each user can access:</span></span>

| <span data-ttu-id="130db-209">ユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="130db-209">User type</span></span> | <span data-ttu-id="130db-210">タブ</span><span class="sxs-lookup"><span data-stu-id="130db-210">Tabs</span></span> | <span data-ttu-id="130db-211">ボット</span><span class="sxs-lookup"><span data-stu-id="130db-211">Bots</span></span> | <span data-ttu-id="130db-212">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="130db-212">Messaging extensions</span></span> | <span data-ttu-id="130db-213">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="130db-213">Adaptive Cards</span></span> | <span data-ttu-id="130db-214">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="130db-214">Task modules</span></span> | <span data-ttu-id="130db-215">会議中ダイアログ</span><span class="sxs-lookup"><span data-stu-id="130db-215">In-meeting dialog</span></span> |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| <span data-ttu-id="130db-216">匿名ユーザー</span><span class="sxs-lookup"><span data-stu-id="130db-216">Anonymous user</span></span> | <span data-ttu-id="130db-217">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-217">Not available</span></span> | <span data-ttu-id="130db-218">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-218">Not available</span></span> | <span data-ttu-id="130db-219">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-219">Not available</span></span> | <span data-ttu-id="130db-220">会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="130db-220">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="130db-221">アダプティブ カードからの会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="130db-221">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="130db-222">利用不可</span><span class="sxs-lookup"><span data-stu-id="130db-222">Not available</span></span> |
| <span data-ttu-id="130db-223">テナント AAD の一部であるゲスト</span><span class="sxs-lookup"><span data-stu-id="130db-223">Guest that is part of the tenant AAD</span></span> | <span data-ttu-id="130db-224">対話は許可されます。</span><span class="sxs-lookup"><span data-stu-id="130db-224">Interaction is allowed.</span></span> <span data-ttu-id="130db-225">作成、更新、削除は許可されません。</span><span class="sxs-lookup"><span data-stu-id="130db-225">Creating, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="130db-226">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-226">Not available</span></span> | <span data-ttu-id="130db-227">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-227">Not available</span></span> | <span data-ttu-id="130db-228">会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="130db-228">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="130db-229">アダプティブ カードからの会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="130db-229">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="130db-230">Available</span><span class="sxs-lookup"><span data-stu-id="130db-230">Available</span></span> |
| <span data-ttu-id="130db-231">フェデレーション</span><span class="sxs-lookup"><span data-stu-id="130db-231">Federated</span></span> | <span data-ttu-id="130db-232">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-232">Not available</span></span> | <span data-ttu-id="130db-233">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-233">Not available</span></span> | <span data-ttu-id="130db-234">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-234">Not available</span></span> | <span data-ttu-id="130db-235">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-235">Not available</span></span> | <span data-ttu-id="130db-236">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-236">Not available</span></span> | <span data-ttu-id="130db-237">使用不可</span><span class="sxs-lookup"><span data-stu-id="130db-237">Not available</span></span> |

## <a name="see-also"></a><span data-ttu-id="130db-238">関連項目</span><span class="sxs-lookup"><span data-stu-id="130db-238">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="130db-239">Tab</span><span class="sxs-lookup"><span data-stu-id="130db-239">Tab</span></span>](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [<span data-ttu-id="130db-240">Bot</span><span class="sxs-lookup"><span data-stu-id="130db-240">Bot</span></span>](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="130db-241">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="130db-241">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="130db-242">アプリをデザインする</span><span class="sxs-lookup"><span data-stu-id="130db-242">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a><span data-ttu-id="130db-243">次の手順</span><span class="sxs-lookup"><span data-stu-id="130db-243">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="130db-244">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="130db-244">Build your app</span></span>](create-apps-for-teams-meetings.md)
