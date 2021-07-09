---
title: 会議アプリ拡張性
author: surbhigupta
description: 会議アプリの機能拡張を理解する
ms.topic: conceptual
ms.openlocfilehash: 1b9cc381879a12d5c9d26711dde93e308d3e4231
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335395"
---
# <a name="meeting-app-extensibility"></a><span data-ttu-id="9ebe9-103">会議アプリ拡張性</span><span class="sxs-lookup"><span data-stu-id="9ebe9-103">Meeting app extensibility</span></span>

<span data-ttu-id="9ebe9-104">Teamsの会議アプリの機能拡張は、次の概念に基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-104">Teams’ meeting app extensibility is based on the following concepts:</span></span>

* <span data-ttu-id="9ebe9-105">会議のライフサイクルには、会議前、会議中、会議後など、さまざまなステージがあります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-105">Meeting lifecycle has different stages such as pre-meeting, in-meeting, and post-meeting.</span></span>  
* <span data-ttu-id="9ebe9-106">会議には、開催者、発表者、出席者の 3 つの異なる参加者の役割があります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-106">There are three distinct participant roles in a meeting: organizer, presenter, and attendee.</span></span> <span data-ttu-id="9ebe9-107">詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-107">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>  
* <span data-ttu-id="9ebe9-108">会議には、[テナント内、](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.)ゲストユーザー、フェデレーション ユーザー、[](/microsoftteams/guest-access)匿名ユーザーなど[、さまざまな](/microsoftteams/manage-external-access)ユーザーの種類があります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-108">There are various [user types](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) in a meeting: in-tenant, [guest](/microsoftteams/guest-access), [federated](/microsoftteams/manage-external-access), and anonymous users.</span></span>

<span data-ttu-id="9ebe9-109">この記事では、会議のライフサイクルと、タブ、ボット、メッセージング拡張機能を会議に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-109">This article covers information about meeting lifecycle and how to integrate tabs, bots, and messaging extensions in the meeting.</span></span> <span data-ttu-id="9ebe9-110">タスクを実行するためのさまざまな参加者の役割とさまざまなユーザーの種類を識別するための情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-110">It provides information to identify different participant roles and different user types to perform tasks.</span></span>

## <a name="meeting-lifecycle"></a><span data-ttu-id="9ebe9-111">会議のライフサイクル</span><span class="sxs-lookup"><span data-stu-id="9ebe9-111">Meeting lifecycle</span></span>

<span data-ttu-id="9ebe9-112">会議のライフサイクルは、会議前、会議中、会議後のアプリ エクスペリエンスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-112">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="9ebe9-113">会議のライフサイクルの各段階で、タブ、ボット、メッセージング拡張機能を統合できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-113">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="9ebe9-114">タブを会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="9ebe9-114">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="9ebe9-115">タブを使用すると、チーム メンバーは会議内の特定の領域内のサービスとコンテンツにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-115">Tabs allow team members to access services and content in a specific space within a meeting.</span></span> <span data-ttu-id="9ebe9-116">チームはタブを直接処理し、タブ内で使用可能なツールとデータに関する会話を行います。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-116">The team works directly with tabs and has conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="9ebe9-117">会議Teams、ユーザーはタブを追加するには、</span><span class="sxs-lookup"><span data-stu-id="9ebe9-117">In Teams meeting, users can add a tab by selecting</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="9ebe9-118">をクリックし、インストールするアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-118">, and choosing the app that they want to install.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ebe9-119">タブを会議に統合している場合、アプリはタブのシングル サインオン (SSO) 認証フロー Teamsに従[う必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-119">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow for tabs](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9ebe9-120">アプリは、プライベートスケジュールされた会議でのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-120">Apps are supported in private scheduled meetings only.</span></span>

#### <a name="pre-meeting-app-experience"></a><span data-ttu-id="9ebe9-121">会議前アプリのエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="9ebe9-121">Pre-meeting app experience</span></span>

<span data-ttu-id="9ebe9-122">会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、アンケート会議参加者への投票の開発など、会議前のタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-122">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks, such as developing a poll to survey meeting participants.</span></span>

<span data-ttu-id="9ebe9-123">**既存の会議にタブを追加するには**</span><span class="sxs-lookup"><span data-stu-id="9ebe9-123">**To add tabs to an existing meeting**</span></span>

1. <span data-ttu-id="9ebe9-124">予定表で、タブを追加する会議を選択します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-124">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="9ebe9-125">[詳細] **タブを選択** し、[</span><span class="sxs-lookup"><span data-stu-id="9ebe9-125">Select the **Details** tab and select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="9ebe9-126">.</span><span class="sxs-lookup"><span data-stu-id="9ebe9-126">.</span></span> <span data-ttu-id="9ebe9-127">タブ ギャラリーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-127">The tab gallery appears.</span></span>

    ![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="9ebe9-129">タブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-129">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="9ebe9-130">アプリはタブとしてインストールされます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-130">The app is installed as a tab.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="9ebe9-131">既存の会議の [会議チャット] タブ **を使用して** タブを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-131">You can also add a tab using the meeting **Chat** tab in an existing meeting.</span></span>
    > * <span data-ttu-id="9ebe9-132">10 件を超えるポーリングまたはアンケートがある場合、タブ レイアウトは整理された状態である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-132">Tab layout must be in an organized state, if there are more than ten polls or surveys.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9ebe9-133">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="9ebe9-133">Desktop</span></span>](#tab/desktop)

![会議前タブ ビュー](../assets/images/apps-in-meetings/PreMeetingTab.png)

# <a name="mobile"></a>[<span data-ttu-id="9ebe9-135">モバイル</span><span class="sxs-lookup"><span data-stu-id="9ebe9-135">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="9ebe9-136">デスクトップまたは Web 上の既存の会議にタブを追加すると、会議の詳細の [その他] セクションにある会議前のエクスペリエンスで同じアプリを確認できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-136">After the tabs are added to an existing meeting on desktop or web, you can see the same apps in pre-meeting experience under **More** section of the meeting details.</span></span>

<img src="../assets/images/apps-in-meetings/mobilepremeeting.png" alt="Mobile pre-meeting experience" width="200"/>  

---

#### <a name="in-meeting-app-experience"></a><span data-ttu-id="9ebe9-137">会議中のアプリ エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="9ebe9-137">In-meeting app experience</span></span>

<span data-ttu-id="9ebe9-138">会議中のアプリ エクスペリエンスを使用すると、アプリと会議内ダイアログ ボックスを使用して、会議中に参加者を参加できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-138">With the in-meeting app experience, you can engage participants during the meeting by using apps and the in-meeting dialog box.</span></span> <span data-ttu-id="9ebe9-139">会議アプリは、会議ウィンドウの上部バーで会議内タブとしてホストされます。会議の参加者に対してアクション可能なコンテンツを紹介するには、会議内ダイアログ ボックスを使用します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-139">Meeting apps are hosted in the top upper bar of the meeting window as an in-meeting tab. Use the in-meeting dialog box to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="9ebe9-140">詳細については、「会議のアプリを[作成する」をTeamsしてください](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-140">For more information, see [create apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="9ebe9-141">モバイルの場合、会議アプリは、会議内>省略 &#x25CF;&#x25CF;&#x25CF; アプリから利用できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-141">For mobile, meeting apps are available from **Apps** > ellipses &#x25CF;&#x25CF;&#x25CF; in the meeting.</span></span> <span data-ttu-id="9ebe9-142">[アプリ **] を** 選択して、会議で利用可能なすべてのアプリを表示します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-142">Select **Apps** to view all the apps available in the meeting.</span></span>

<span data-ttu-id="9ebe9-143">**会議中にタブを使用するには**</span><span class="sxs-lookup"><span data-stu-id="9ebe9-143">**To use tabs during a meeting**</span></span>

1. <span data-ttu-id="9ebe9-144">[次へ] Teams。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-144">Go to Teams.</span></span>
1. <span data-ttu-id="9ebe9-145">予定表で、タブを使用する会議を選択します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-145">In your calendar, select a meeting where you want to use a tab.</span></span>
1. <span data-ttu-id="9ebe9-146">会議に入った後、チャット ウィンドウの上部バーから、必要なアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-146">After entering the meeting, from the top upper bar of the chat window, select the required app.</span></span>
    <span data-ttu-id="9ebe9-147">アプリは、サイド パネルTeams会議内の会議に表示されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-147">An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span>
1. <span data-ttu-id="9ebe9-148">[会議内] ダイアログ ボックスで、フィードバックとして応答を入力します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-148">In the in-meeting dialog box, enter your response as a feedback.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9ebe9-149">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="9ebe9-149">Desktop</span></span>](#tab/desktop)

![ダイアログ ボックス ビュー](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

# <a name="mobile"></a>[<span data-ttu-id="9ebe9-151">モバイル</span><span class="sxs-lookup"><span data-stu-id="9ebe9-151">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="9ebe9-152">会議に参加し、デスクトップまたは Web からアプリを追加すると、アプリはモバイル 会議Teams [アプリ] セクションに **表示** されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-152">After entering the meeting and adding the app from desktop or web, the app is visible in mobile Teams meeting under the **Apps** section.</span></span> <span data-ttu-id="9ebe9-153">[アプリ **] を** 選択してアプリの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-153">Select **Apps** to show the list of apps.</span></span> <span data-ttu-id="9ebe9-154">ユーザーは、任意のアプリをアプリの会議内サイド パネルとして起動できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-154">User can launch any of the apps as an in-meeting side panel of the app.</span></span>

<span data-ttu-id="9ebe9-155">[会議内] ダイアログ ボックスが表示され、フィードバックとして応答を入力できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-155">The in-meeting dialog box is displayed where you can enter your response as a feedback.</span></span>

<img src="../assets/images/apps-in-meetings/mobile-in-meeting-dialog-view.png" alt="Mobile dialog box view" width="200"/>

> [!NOTE]
> <span data-ttu-id="9ebe9-156">アプリがモバイルで動作するには、アプリ マニフェストを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-156">You need not change the app manifest for the apps to work on mobile.</span></span>

---

> [!NOTE]
> * <span data-ttu-id="9ebe9-157">アプリは、クライアント SDK Teamsを利用して、 にアクセスし、エクスペリエンス `meetingId` `userMri` `frameContext` を適切にレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-157">Apps can leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to render the experience appropriately.</span></span>
> * <span data-ttu-id="9ebe9-158">会議中のダイアログ ボックスが正常にレンダリングされると、結果が正常にダウンロードされたことを通知します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-158">If the in-meeting dialog box is rendered successfully, you will get a notification that the results are successfully downloaded.</span></span>
> * <span data-ttu-id="9ebe9-159">アプリ マニフェストは、表示する場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-159">Your app manifest specifies the places that you want them to appear.</span></span> <span data-ttu-id="9ebe9-160">コンテキスト フィールドは、この目的のために使用されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-160">The context field is used for this purpose.</span></span> <span data-ttu-id="9ebe9-161">また、指定された設計ガイドラインに従って、共有トレイ エクスペリエンスの一部です。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-161">It is also the part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="9ebe9-162">次の図は、会議中のサイド パネルを示しています。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-162">The following image illustrates the in-meeting side panel:</span></span>

![会議中のサイド パネル](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="9ebe9-164">次の表に、アプリが承認され、承認されていない場合のアプリの動作を示します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-164">The following table describes the behavior of app when it is approved and not approved:</span></span>

|<span data-ttu-id="9ebe9-165">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="9ebe9-165">App capability</span></span> | <span data-ttu-id="9ebe9-166">アプリが承認されている</span><span class="sxs-lookup"><span data-stu-id="9ebe9-166">App is approved</span></span> | <span data-ttu-id="9ebe9-167">アプリが承認されていない</span><span class="sxs-lookup"><span data-stu-id="9ebe9-167">App is not approved</span></span> |
|---|---|---|
| <span data-ttu-id="9ebe9-168">会議の機能拡張</span><span class="sxs-lookup"><span data-stu-id="9ebe9-168">Meeting extensibility</span></span> | <span data-ttu-id="9ebe9-169">アプリは会議に表示されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-169">The app will appear in meetings.</span></span> | <span data-ttu-id="9ebe9-170">アプリは、モバイル クライアントの会議には表示されません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-170">The app will not appear in meetings for the mobile clients.</span></span> |

#### <a name="post-meeting-app-experience"></a><span data-ttu-id="9ebe9-171">会議後のアプリ エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="9ebe9-171">Post-meeting app experience</span></span>

<span data-ttu-id="9ebe9-172">会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果やフィードバックなど、会議の結果を表示できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-172">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span> <span data-ttu-id="9ebe9-173">Select</span><span class="sxs-lookup"><span data-stu-id="9ebe9-173">Select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> <span data-ttu-id="9ebe9-174">をクリックしてタブを追加し、会議メモを取得し、開催者と出席者がアクションを実行する必要がある結果を取得します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-174">to add a tab, get meeting notes, and results on which organizers and attendees must take action.</span></span>

<span data-ttu-id="9ebe9-175">次の図は **、[Contoso]** タブを表示し、会議の出席者から受け取ったポーリングとフィードバックの結果を示します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-175">The following image displays the **Contoso** tab with results of poll and feedback received from meeting attendees:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9ebe9-176">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="9ebe9-176">Desktop</span></span>](#tab/desktop)

![会議ビューの投稿](../assets/images/apps-in-meetings/PostMeeting.png)

# <a name="mobile"></a>[<span data-ttu-id="9ebe9-178">モバイル</span><span class="sxs-lookup"><span data-stu-id="9ebe9-178">Mobile</span></span>](#tab/mobile)

<img src="../assets/images/apps-in-meetings/mobilePostMeeting.png" alt="Mobile post meeting view" width="200"/>

---

> [!NOTE]
> <span data-ttu-id="9ebe9-179">10 件を超えるポーリングまたはアンケートがある場合は、タブ レイアウトを整理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-179">Tab layout must be organized when there are more than 10 polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="9ebe9-180">ボットを会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="9ebe9-180">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="9ebe9-181">グループチャット スコープで有効になっているボットは、会議で機能し始める。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-181">Bots enabled in groupchat scope start functioning in meetings.</span></span> <span data-ttu-id="9ebe9-182">ボットを実装するには、ボットのビルド[から始](../build-your-first-app/build-bot.md)め、次に、会議のアプリを作成[Teamsします](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-182">To implement bots, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="9ebe9-183">メッセージング拡張機能を会議のライフサイクルに統合する</span><span class="sxs-lookup"><span data-stu-id="9ebe9-183">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="9ebe9-184">メッセージング拡張機能を実装するには、まずメッセージング拡張機能[](../messaging-extensions/how-to/create-messaging-extension.md)を作成してから、会議用アプリの作成[Teamsします](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-184">To implement messaging extensions, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references).</span></span>

<span data-ttu-id="9ebe9-185">会議Teams機能拡張により、会議の参加者の役割に基づいてアプリを設計できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-185">The Teams meeting app extensibility allows you to design your app based on participant roles in a meeting.</span></span>

## <a name="participant-roles-in-a-meeting"></a><span data-ttu-id="9ebe9-186">会議の参加者の役割</span><span class="sxs-lookup"><span data-stu-id="9ebe9-186">Participant roles in a meeting</span></span>

![会議の参加者](../assets/images/apps-in-meetings/participant-roles.png)

<span data-ttu-id="9ebe9-188">既定の参加者設定は、組織の IT 管理者によって決まります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-188">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="9ebe9-189">会議の参加者の役割を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-189">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="9ebe9-190">**開催** 者 : 開催者は会議をスケジュールし、会議のオプションを設定し、会議の役割を割り当て、会議を開始します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-190">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="9ebe9-191">M365 アカウントとユーザー ライセンスを持Teams、参加者のアクセス許可を制御できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-191">Only users with M365 account and Teams license can be organizers, and control attendee permissions.</span></span> <span data-ttu-id="9ebe9-192">会議の開催者は、特定の会議の設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-192">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="9ebe9-193">開催者は、[会議のオプション] Web ページ **でこれらの変更を** 行えます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-193">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="9ebe9-194">**発表者**: 発表者は、除外を含む開催者と同じ機能を持っています。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-194">**Presenter**: Presenters have same capabilities of organizers with exclusions.</span></span> <span data-ttu-id="9ebe9-195">発表者は、セッションから開催者を削除したり、セッションの会議オプションを変更したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-195">A presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="9ebe9-196">既定では、会議に参加する参加者には発表者の役割があります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-196">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="9ebe9-197">**出席者**: 出席者とは、会議に出席するために招待されたが、発表者として機能する権限を持たされていないユーザーです。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-197">**Attendee**: An attendee is a user who has been invited to attend a meeting but is not authorized to act as a presenter.</span></span> <span data-ttu-id="9ebe9-198">出席者は他の会議メンバーとやり取りできますが、会議の設定を管理したり、コンテンツを共有したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-198">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

> [!NOTE]
> <span data-ttu-id="9ebe9-199">アプリを追加、削除、またはアンインストールできるのは、開催者または発表者のみです。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-199">Only an organizer or presenter can add, remove, or uninstall apps.</span></span>

<span data-ttu-id="9ebe9-200">詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-200">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="9ebe9-201">会議の参加者の役割に基づいてアプリを設計した後、会議の各ユーザーの種類を特定し、アクセスできるユーザーを選択できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-201">After you design your app based on participant roles in a meeting, you can identify each user type for meetings and select what they can access.</span></span>

## <a name="user-types-in-a-meeting"></a><span data-ttu-id="9ebe9-202">会議内のユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="9ebe9-202">User types in a meeting</span></span>

> [!NOTE]
> <span data-ttu-id="9ebe9-203">ユーザーの種類は **getParticipantRole** API には含まれません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-203">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="9ebe9-204">会議の開催者、発表者、出席者などのユーザーの種類は、会議で参加者の役割の 1 [つを実行できます](#participant-roles-in-a-meeting)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-204">User types, such as, organizer, presenter, or attendee in a meeting can perform one of the [participant roles in a meeting](#participant-roles-in-a-meeting).</span></span>

<span data-ttu-id="9ebe9-205">次の一覧では、アクセシビリティとパフォーマンスに加え、さまざまなユーザーの種類について説明します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-205">The following list details the different user types along with their accessibility and performance:</span></span>

* <span data-ttu-id="9ebe9-206">**テナント内 :** テナント内ユーザーは組織に属し、テナントの Azure Active Directory (AAD) に資格情報を持ちます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-206">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="9ebe9-207">通常、フルタイム、オンサイト、またはリモートの従業員です。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-207">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="9ebe9-208">テナント内のユーザーには、開催者、発表者、または出席者を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-208">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="9ebe9-209">**ゲスト**: ゲストは、組織のテナント内の他のリソースTeamsにアクセスするために招待された別の組織の参加者です。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-209">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="9ebe9-210">ゲストは組織の AAD に追加され、チーム チャット、会議、ファイルTeamsアクセスできるネイティブ チーム メンバーと同じ機能を持ちます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-210">Guests are added to the organization’s AAD and have same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="9ebe9-211">ゲスト ユーザーには、開催者、発表者、または出席者を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-211">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="9ebe9-212">詳細については、「ゲスト アクセス[」を参照Teams。](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="9ebe9-212">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="9ebe9-213">**フェデレーションまたは外部**: フェデレーション ユーザーは、会議への参加をTeams組織の外部ユーザーです。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-213">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="9ebe9-214">フェデレーション ユーザーは、フェデレーション パートナーと有効な資格情報を持ち、Teams。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-214">Federated users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="9ebe9-215">組織からチームや他の共有リソースにアクセスできない。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-215">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="9ebe9-216">ゲスト アクセスは、外部ユーザーがチームとチャネルにアクセスできる優れたオプションです。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-216">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="9ebe9-217">詳細については、「外部アクセスの[管理」を参照Teams。](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="9ebe9-217">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ebe9-218">ユーザー Teams、他の組織との会議やチャットをホストするときにアプリを追加できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-218">Your Teams users can add apps when they host meetings or chats with other organizations.</span></span> <span data-ttu-id="9ebe9-219">ユーザーは、ユーザーが他の組織がホストする会議やチャットに参加するときに、外部ユーザーが共有するアプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-219">The users can use apps shared by external users when your users join meetings or chats hosted by other organizations.</span></span> <span data-ttu-id="9ebe9-220">ホスティング ユーザーの組織のデータ ポリシーと、そのユーザーの組織が共有するサード パーティ製アプリのデータ共有プラクティスが有効になります。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-220">The data policies of the hosting user's organization, as well as the data sharing practices of the third-party apps shared by that user's organization, will be in effect.</span></span>

* <span data-ttu-id="9ebe9-221">**匿名**: 匿名ユーザーは AAD ID を持ち、テナントとフェデレーションされません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-221">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="9ebe9-222">匿名の参加者は外部ユーザーと同じですが、その ID は会議に投影されません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-222">The anonymous participants are like external users, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="9ebe9-223">匿名ユーザーは、会議ウィンドウでアプリにアクセスできない。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-223">Anonymous users are not able to access apps in a meeting window.</span></span> <span data-ttu-id="9ebe9-224">匿名ユーザーを開催者にすることはできませんが、発表者または出席者を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-224">An anonymous user cannot be an organizer but can be a presenter or attendee.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ebe9-225">匿名ユーザーは、グローバル既定のユーザー レベルのアプリアクセス許可ポリシーを継承します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-225">Anonymous users inherit the global default user-level app permission policy.</span></span> <span data-ttu-id="9ebe9-226">詳細については、「アプリの管理 [」を参照してください](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-226">For more information, see [manage Apps](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).</span></span>

<span data-ttu-id="9ebe9-227">ゲストまたは匿名ユーザーは、アプリを追加、削除、アンインストールできません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-227">A guest or anonymous user cannot add, remove, or uninstall apps.</span></span>

<span data-ttu-id="9ebe9-228">次の表に、ユーザーの種類と、各ユーザーがアクセスできる機能を示します。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-228">The following table provides the user types and what features each user can access:</span></span>

| <span data-ttu-id="9ebe9-229">ユーザーの種類</span><span class="sxs-lookup"><span data-stu-id="9ebe9-229">User type</span></span> | <span data-ttu-id="9ebe9-230">タブ</span><span class="sxs-lookup"><span data-stu-id="9ebe9-230">Tabs</span></span> | <span data-ttu-id="9ebe9-231">ボット</span><span class="sxs-lookup"><span data-stu-id="9ebe9-231">Bots</span></span> | <span data-ttu-id="9ebe9-232">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="9ebe9-232">Messaging extensions</span></span> | <span data-ttu-id="9ebe9-233">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="9ebe9-233">Adaptive Cards</span></span> | <span data-ttu-id="9ebe9-234">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="9ebe9-234">Task modules</span></span> | <span data-ttu-id="9ebe9-235">会議中ダイアログ</span><span class="sxs-lookup"><span data-stu-id="9ebe9-235">In-meeting dialog</span></span> |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| <span data-ttu-id="9ebe9-236">匿名ユーザー</span><span class="sxs-lookup"><span data-stu-id="9ebe9-236">Anonymous user</span></span> | <span data-ttu-id="9ebe9-237">使用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-237">Not available</span></span> | <span data-ttu-id="9ebe9-238">使用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-238">Not available</span></span> | <span data-ttu-id="9ebe9-239">使用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-239">Not available</span></span> | <span data-ttu-id="9ebe9-240">会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-240">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="9ebe9-241">アダプティブ カードからの会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-241">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="9ebe9-242">利用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-242">Not available</span></span> |
| <span data-ttu-id="9ebe9-243">テナント AAD の一部であるゲスト</span><span class="sxs-lookup"><span data-stu-id="9ebe9-243">Guest that is part of the tenant AAD</span></span> | <span data-ttu-id="9ebe9-244">対話は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-244">Interaction is allowed.</span></span> <span data-ttu-id="9ebe9-245">作成、更新、削除は許可されません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-245">Creating, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="9ebe9-246">使用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-246">Not available</span></span> | <span data-ttu-id="9ebe9-247">使用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-247">Not available</span></span> | <span data-ttu-id="9ebe9-248">会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-248">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="9ebe9-249">アダプティブ カードからの会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-249">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="9ebe9-250">Available</span><span class="sxs-lookup"><span data-stu-id="9ebe9-250">Available</span></span> |
| <span data-ttu-id="9ebe9-251">フェデレーション ユーザー。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-251">Federated user.</span></span> <span data-ttu-id="9ebe9-252">詳細については、「標準以外の [ユーザー」を参照してください](/microsoftteams/non-standard-users)。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-252">For more information, see [non-standard users](/microsoftteams/non-standard-users).</span></span> | <span data-ttu-id="9ebe9-253">対話は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-253">Interaction is allowed.</span></span> <span data-ttu-id="9ebe9-254">作成、更新、削除は許可されません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-254">Creating, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="9ebe9-255">対話は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-255">Interaction is allowed.</span></span> <span data-ttu-id="9ebe9-256">取得、更新、および削除は許可されません。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-256">Acquiring, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="9ebe9-257">利用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-257">Not available</span></span> | <span data-ttu-id="9ebe9-258">会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-258">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="9ebe9-259">アダプティブ カードからの会議チャットでの操作は許可されます。</span><span class="sxs-lookup"><span data-stu-id="9ebe9-259">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="9ebe9-260">利用不可</span><span class="sxs-lookup"><span data-stu-id="9ebe9-260">Not available</span></span> |

## <a name="see-also"></a><span data-ttu-id="9ebe9-261">関連項目</span><span class="sxs-lookup"><span data-stu-id="9ebe9-261">See also</span></span>

* [<span data-ttu-id="9ebe9-262">Tab</span><span class="sxs-lookup"><span data-stu-id="9ebe9-262">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="9ebe9-263">Bot</span><span class="sxs-lookup"><span data-stu-id="9ebe9-263">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="9ebe9-264">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="9ebe9-264">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="9ebe9-265">アプリをデザインする</span><span class="sxs-lookup"><span data-stu-id="9ebe9-265">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="9ebe9-266">次の手順</span><span class="sxs-lookup"><span data-stu-id="9ebe9-266">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ebe9-267">Teams 会議アプリへの前提条件と API リファレンス</span><span class="sxs-lookup"><span data-stu-id="9ebe9-267">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)