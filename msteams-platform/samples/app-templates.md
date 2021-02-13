---
title: Microsoft Teams アプリ テンプレート
description: Microsoft Teams プラットフォーム用のアプリ テンプレートのリンクと説明
ms.topic: reference
keywords: Microsoft Teams テンプレートのサンプル デモ
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 21721848ba7893380ac217b5f47ce6a6e669e869
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231639"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="0d197-104">Microsoft Teams のアプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="0d197-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="0d197-105">アプリ テンプレートは、オープン ソースで GitHub で利用できる Microsoft Teams 用の完全なアプリの例です。</span><span class="sxs-lookup"><span data-stu-id="0d197-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="0d197-106">各アプリ テンプレートには、組織用にアプリを展開およびインストールする詳細な手順が含されています。</span><span class="sxs-lookup"><span data-stu-id="0d197-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="0d197-107">また、すぐにインストールして使用を開始できるサンプル アプリも提供します。</span><span class="sxs-lookup"><span data-stu-id="0d197-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="0d197-108">完全なソース コードも使用できます。これにより、詳細を参照したり、コードをフォークして、特定の要件を満たして変更することができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="0d197-109">すべてのアプリ テンプレートは、MIT ライセンス条項 [に従って提供](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) されます。</span><span class="sxs-lookup"><span data-stu-id="0d197-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
>[!NOTE] 
><span data-ttu-id="0d197-110">Microsoft は、ユーザーや組織のアプリ テンプレートから作成されたアプリのライセンスを取得してサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0d197-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="0d197-111">**&#9734; 新たにリリースされたアプリ テンプレートを示します。**</span><span class="sxs-lookup"><span data-stu-id="0d197-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="0d197-112">主な利点</span><span class="sxs-lookup"><span data-stu-id="0d197-112">Key benefits</span></span>

* <span data-ttu-id="0d197-113">**クラウドに直接展開します。** すべてのアプリ テンプレートには、Microsoft Azure または Power Platform で必要なすべてのサービスをホストできる展開スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0d197-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="0d197-114">**推奨されるサンプル コード:** アプリ テンプレートは、セキュリティとインフラストラクチャに関する推奨ベスト プラクティスに準拠しています。</span><span class="sxs-lookup"><span data-stu-id="0d197-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="0d197-115">アプリ テンプレートに対して提出されたコミュニティの変更はすべて、準拠を確認するためにレビューされます。</span><span class="sxs-lookup"><span data-stu-id="0d197-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="0d197-116">**カスタマイズ可能で拡張可能:** すべてのアプリ テンプレートは最小限の構成で展開することができますが、独自のニーズに合わせて簡単にカスタマイズまたは拡張できるよう、コード ベースと展開スクリプト全体が提供されています。</span><span class="sxs-lookup"><span data-stu-id="0d197-116">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="0d197-117">**詳細なドキュメント:** すべてのアプリ テンプレートには、ソリューションのアーキテクチャ、展開、および構成の手順に関するエンドツーエンドのドキュメントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="0d197-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot-9734"></a><span data-ttu-id="0d197-118">導入ボット &#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-118">Adoption Bot &#9734;</span></span>

<span data-ttu-id="0d197-119">導入ボットは、Power Virtual Agent for Teams (PVA) を使用して構築されたユーザー の管理チャット ボットです。</span><span class="sxs-lookup"><span data-stu-id="0d197-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="0d197-120">これは、PVA バージョンの FAQPlus と見なされます。</span><span class="sxs-lookup"><span data-stu-id="0d197-120">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="0d197-121">導入ボットは、Microsoft 365 と Teams に関する 100 以上の一般的な質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="0d197-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="0d197-122">含まれるトピックの編集、独自のトピックの追加、および既存の FAQ の取り込み。</span><span class="sxs-lookup"><span data-stu-id="0d197-122">You can edit the included topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="0d197-123">ユーザーが追加のサポートを必要とする場合、導入ボットは専門家に接続したり、プレミアム フロー コネクタを使用してサービス チケットを開くまで拡張することができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span>

[<span data-ttu-id="0d197-124">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-124">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a><span data-ttu-id="0d197-125">Appointment Manager &#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-125">Appointment Manager &#9734;</span></span>

<span data-ttu-id="0d197-126">予定マネージャーは、企業が Teams を通じてコンシューマーとの仮想予定を作成、管理、および実施するのに役立つ Teams アプリ テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="0d197-126">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="0d197-127">コンシューマーからの新しい予定の要求は Teams チャネルに表示され、チーム内のスタッフにすばやく割り当て、再割り当てできます。</span><span class="sxs-lookup"><span data-stu-id="0d197-127">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="0d197-128">予定の依頼は、カスタム タブを使用して、チーム レベルまたは個人レベルで表示できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-128">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="0d197-129">すべての予定は Teams オンライン会議に関連付けられているため、スタッフとコンシューマーはスケジュールされた時間に簡単に会議に参加できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-129">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="0d197-130">アプリ テンプレートは、Microsoft Bookings と統合して、予定を簡単に管理できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-130">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="0d197-131">スケジュールされた予定は割り当てられたスタッフの予定表に自動的に表示され、コンシューマーは会議リンクが埋め込まれたカスタマイズ可能な電子メール通知と事前通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="0d197-131">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="0d197-132">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-132">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="0d197-133">![Appointment Manager Overview ](../assets/images/appointment-manager-overview.png)
 ![ Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="0d197-133">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="0d197-134">Ask Away</span><span class="sxs-lookup"><span data-stu-id="0d197-134">Ask Away</span></span>

<span data-ttu-id="0d197-135">Ask Away は、ユーザーが Teams 内で Q&A (質問と回答) セッションを実行できるようにする [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-135">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="0d197-136">チーム メンバーは、Ask Away ボットを使用して、同僚が共有する質問を送信して賛成票を投じることができます。これにより、Q&A ホストは、チャネルまたはチャット内で最も重要な質問を簡単に収集できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-136">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="0d197-137">ボットを使用して、Teams 会議でリアルタイムの Q&A セッションを実行でき、出席者はチャットを介してライブで質問を送信できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-137">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="0d197-138">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![ユーザーが質問に投票するためのランキング ポップアップ ダイアログの表示](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="0d197-140">アソシエイト インサイト</span><span class="sxs-lookup"><span data-stu-id="0d197-140">Associate Insights</span></span>

<span data-ttu-id="0d197-141">アソシエイト インサイトは、現場担当者が顧客の意見、感情、認識を直接キャプチャして送信できるようにする [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="0d197-141">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="0d197-142">多くの場合、現場担当者は、一対一の連絡窓口で顧客と関わりを持つ最初の会社の代表者です。</span><span class="sxs-lookup"><span data-stu-id="0d197-142">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="0d197-143">収集されたデータは、製品の改善とカスタマー エクスペリエンスの向上のために、たとえば Power BI Teams タブを介して、ビジネスチームが共同で共有および使用できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-143">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="0d197-144">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-144">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![アプリが生成した分析情報のフィードバック ビュー](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![アプリが生成した分析情報の Power BI ビュー](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="0d197-147">勤怠</span><span class="sxs-lookup"><span data-stu-id="0d197-147">Attendance</span></span>

<span data-ttu-id="0d197-148">勤怠アプリは、チームにピン留めすることができる [[Power Apps]](/powerapps/maker/canvas-apps/embed-teams-app) タブです。</span><span class="sxs-lookup"><span data-stu-id="0d197-148">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="0d197-149">これは、通常、学習環境やトレーニング環境などの設定で出欠を記録するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="0d197-149">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="0d197-150">ユーザーは、過去 30 日間までの出席をマークまたは編集し、グループ全体または個々の出席者の要約された出席レポートを表示できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-150">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="0d197-151">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-151">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![勤怠アプリのデモ](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="0d197-153">会議室予約</span><span class="sxs-lookup"><span data-stu-id="0d197-153">Book-a-room</span></span>

<span data-ttu-id="0d197-154">会議室予約は、会議室をすばやく検索して、現在時刻から 30 分間 (既定)、60 分間、90 分間予約できる [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-154">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="0d197-155">会議室予約ボットは、個人の会話または一対一の会話を対象としています。</span><span class="sxs-lookup"><span data-stu-id="0d197-155">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="0d197-156">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-156">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![会議室予約のデモ](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="0d197-158">アクセスを構築する</span><span class="sxs-lookup"><span data-stu-id="0d197-158">Building Access</span></span>

<span data-ttu-id="0d197-159">Building Access は、施設の管理者が従業員が施設に滞在しているかどうかを管理、追跡、報告できるようにして、建物の占有しきい値と社会的距離の基準の管理をサポートする Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-159">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="0d197-160">Microsoft [Power Apps](/powerapps/powerapps-overview)、[Power Automate](/power-automate/getting-started)を使用して構築されたこのアプリは、Microsoft Teams と緊密に統合されており、組織が建物の準備状況を判断し、現場アクセスの適格基準を確立し、将来の計画のための分析情報を収集できるようにします。</span><span class="sxs-lookup"><span data-stu-id="0d197-160">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="0d197-161">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Building Access の予約カード](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Building Access の主なビュー](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="0d197-164">Celebrations</span><span class="sxs-lookup"><span data-stu-id="0d197-164">Celebrations</span></span>

<span data-ttu-id="0d197-165">Celebrations は、チームメンバーがお互いの誕生日、記念日、その他の定期的なイベントを祝うのに役立つ Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-165">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="0d197-166">チーム メンバー全員の特別な日を思い出し、イベント作成時に選択されたすべてのチームに友好的なメッセージを送信して、チーム メンバーがその日に特別な気分になるようにします。</span><span class="sxs-lookup"><span data-stu-id="0d197-166">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="0d197-167">このアプリでは、チームメンバー全員が簡単にイベントを追加および表示できるようにするためのインターフェイスが用意されています。また、イベントを共有するチームをユーザーが選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="0d197-167">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="0d197-168">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-168">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="0d197-169">チェックリスト</span><span class="sxs-lookup"><span data-stu-id="0d197-169">Checklist</span></span>

<span data-ttu-id="0d197-170">Checklist は、チャットやチャネルで共有チェックリストを作成することで、チームと共同作業を行うことができる、Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-170">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="0d197-171">このアプリは、デスクトップ、ブラウザー、iOS、Android のすべての Teams プラットフォーム クライアントでサポートされており、Microsoft365 サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="0d197-171">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="0d197-172">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-172">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Teams ビューにチェックリストを作成する](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a><span data-ttu-id="0d197-174">Classroom Drop-in &#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-174">Classroom Drop-in &#9734;</span></span>

<span data-ttu-id="0d197-175">Classroom Drop-in は、システム リーダーがクラス チーム (仮想教室) を見つけて、必要に応じて指定したドロップイン期間に自分自身または他のユーザーをこれらのクラス チームに追加できる Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-175">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="0d197-176">Microsoft [Power Apps](/powerapps/powerapps-overview) と [Power Automate](/power-automate/getting-started)を使用して構築されたアプリは、Microsoft Teams と深く統合され、教育機関がビジネス要件ごとにクラス チームの関連関係者にアクセスを提供することで、ハイブリッド学習環境での運用を最適化できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-176">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="0d197-177">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-177">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![クラスルームのドロップイン要求](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="0d197-179">社内コミュニケーター</span><span class="sxs-lookup"><span data-stu-id="0d197-179">Company Communicator</span></span>

<span data-ttu-id="0d197-180">社内コミュニケーター アプリを使用すると、企業チームはチャットを介して複数のチームまたは多数の従業員向けのメッセージを作成および送信できます。これにより、組織は共同作業を行う場所で従業員に連絡できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-180">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="0d197-181">このテンプレートは、新しいイニシアチブの発表、従業員のオンボーディング、最新の学習と能力開発、組織全体のブロードキャストなど、複数のシナリオに利用できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-181">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="0d197-182">このアプリは、指定されたユーザーがメッセージを作成、プレビュー、共同作業、送信するための簡単なインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="0d197-182">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="0d197-183">これは、メッセージを確認または操作したユーザーの数に関するカスタム テレメトリなどのカスタム ターゲット通信機能を構築するための基盤を提供します。</span><span class="sxs-lookup"><span data-stu-id="0d197-183">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="0d197-184">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-184">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![社内コミュニケーターの作成ボックス ビュー](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="0d197-186">連絡先グループの参照</span><span class="sxs-lookup"><span data-stu-id="0d197-186">Contact Group Lookup</span></span>

<span data-ttu-id="0d197-187">Contact Group Lookup アプリは、組織の連絡先グループ (以前は、「配布リストまたはコミュニケーション グループ」と呼ばれていました) を作成、アクセス、および管理するための便利で有用なアプローチを提供します。</span><span class="sxs-lookup"><span data-stu-id="0d197-187">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="0d197-188">ユーザーは、すべての Teams 環境内で、グループ メンバーの表示とチャット、メンバー ステータスの表示、連絡先グループの選択したメンバーとのグループ チャットの作成をすばやく行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-188">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="0d197-189">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-189">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![Contact Group Lookup のピン留めされたお気に入りビュー](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Contact Group Lookup のチャット開始のデモ](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation-9734"></a><span data-ttu-id="0d197-192">同僚の働き&#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-192">Co-worker Appreciation &#9734;</span></span>

<span data-ttu-id="0d197-193">Microsoft Teams の同僚の仕事仲間テンプレートを使用すると、ユーザーは Teams のコンテキスト内で同僚の実績を認識できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-193">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="0d197-194">同僚が仕事仲間に報酬を与える場合、受信者と他のチーム メンバーはチャネルの会話でタグ付けされ、チャネルの特典の詳細に関する通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="0d197-194">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="0d197-195">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span><span class="sxs-lookup"><span data-stu-id="0d197-195">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="0d197-196">これは、ランキング付き、PowerApps ベースのバージョンの Open Badges アプリ テンプレートと見なされます。</span><span class="sxs-lookup"><span data-stu-id="0d197-196">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="0d197-197">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-197">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![全体](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="0d197-199">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="0d197-199">CrowdSourcer</span></span>

<span data-ttu-id="0d197-200">CrowdSourcer は、グループ メンバーから共同で調達された情報をチームに照会する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-200">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="0d197-201">これは、参加者が楽しく役立つ情報リソースに積極的に参加して貢献できるようにしながら、よく寄せられる質問に回答するための優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="0d197-201">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="0d197-202">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-202">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Crowdsource のエンドユーザーの操作](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="0d197-204">カスタム ステッカー</span><span class="sxs-lookup"><span data-stu-id="0d197-204">Custom Stickers</span></span>

<span data-ttu-id="0d197-205">自己表現は健全なチーム文化の中核です。</span><span class="sxs-lookup"><span data-stu-id="0d197-205">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="0d197-206">このアプリ テンプレートは、ユーザーが Microsoft Teams 内で、カスタム ステッカーや GIF を使用できるようにする[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-206">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="0d197-207">このテンプレートは、簡単な Web ベースの構成エクスペリエンスを提供し、構成アクセス権を持つユーザーがエンド ユーザーに持たせたい GIF/ステッカー/画像をアップロードできるため、チーム全体で選択したステッカーのセットを使用できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-207">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="0d197-208">このアプリでは、ストレージや共有メカニズムとして SharePoint サイトや個々のチャネルにアクセスしなくても、チーム間で画像/GIF/ステッカーを簡単に共有できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-208">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="0d197-209">たとえば、製品チームは、製品の画像や GIF をソーシャル メディア、マーケティング、販売チームとプログラムで簡単に共有できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-209">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="0d197-210">新しい画像/GIF が利用可能になったときに、特定のチーム/個人への通知フローをトリガーすることで、このアプリを拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="0d197-210">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="0d197-211">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-211">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![ステッカー アプリ](../assets/images/stickers.png)

## <a name="employee-ideas-9734"></a><span data-ttu-id="0d197-213">Employee Ideas &#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-213">Employee Ideas &#9734;</span></span>

<span data-ttu-id="0d197-214">Employee Ideas アプリは、Azure ベースの Great Ideas アプリ テンプレートの PowerApps バージョンです。</span><span class="sxs-lookup"><span data-stu-id="0d197-214">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="0d197-215">このアプリを使用すると、Teams ユーザーはアイデア キャンペーンを設定および構成できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-215">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="0d197-216">アイデア キャンペーンは、一般的なテーマに関するアイデアをグループ化するカテゴリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-216">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="0d197-217">Teams ユーザーは、次のアクティビティを実行できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-217">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="0d197-218">アイデアごとに従業員が提出する必要がある標準的な提出フォームを構成します。</span><span class="sxs-lookup"><span data-stu-id="0d197-218">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="0d197-219">キャンペーンのアイデアとリストを確認して管理します。</span><span class="sxs-lookup"><span data-stu-id="0d197-219">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="0d197-220">キャンペーンを変更および削除します。</span><span class="sxs-lookup"><span data-stu-id="0d197-220">Modify and delete campaigns.</span></span>
* <span data-ttu-id="0d197-221">リーダーのアイデア掲示板を確認します。</span><span class="sxs-lookup"><span data-stu-id="0d197-221">Review leader boards of ideas.</span></span>
* <span data-ttu-id="0d197-222">優先するアイデアに投票して共有します。</span><span class="sxs-lookup"><span data-stu-id="0d197-222">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="0d197-223">キャンペーンのアイデアを提出します。</span><span class="sxs-lookup"><span data-stu-id="0d197-223">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="0d197-224">他のチーム メンバーのアイデアを表示します。</span><span class="sxs-lookup"><span data-stu-id="0d197-224">View other team member's idea.</span></span>
* <span data-ttu-id="0d197-225">最もいいね! アイデアに投票します。</span><span class="sxs-lookup"><span data-stu-id="0d197-225">Vote on most liked ideas.</span></span>
* <span data-ttu-id="0d197-226">キャンペーン内の他のユーザーと比較して、アイデアのパフォーマンスを確認します。</span><span class="sxs-lookup"><span data-stu-id="0d197-226">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="0d197-227">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-227">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![キャンペーン ビューの管理](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="0d197-229">E-しがち</span><span class="sxs-lookup"><span data-stu-id="0d197-229">E-Prescriptions</span></span> 

<span data-ttu-id="0d197-230">E-Prescriptions は、患者に電子処方箋を発行するプロセスを自動化することにより、遠隔医療と仮想ケアを強化する [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-230">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="0d197-231">医療専門家は、Teams プラットフォーム内で直接、予定をすばやく確認し、電子処方箋を生成し、電子処方箋を添付した電子メールを患者に送信できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-231">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="0d197-232">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-232">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![E-Prescriptions アプリのスクリーンショット。](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![E-Prescriptions アプリのスクリーンショット。](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="0d197-237">従業員トレーニング</span><span class="sxs-lookup"><span data-stu-id="0d197-237">Employee Training</span></span> 

<span data-ttu-id="0d197-238">従業員トレーニングは、主催者が組織の学習およびトレーニング イベントを簡単に公開、追跡、促進できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-238">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="0d197-239">このアプリを使用すると、イベント プランナーはイベント登録者にリマインダーと通知を送信できます。従業員は今後のイベントへの関心を示し、現在のイベントの最新情報を入手し、Teams メッセージング拡張機能を介して同僚とイベントの詳細を共有できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-239">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="0d197-240">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-240">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="0d197-241">**従業員トレーニング イベントの表示** ![従業員トレーニング タブの画像](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="0d197-241">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="0d197-242">**従業員トレーニング イベントの作成** ![従業員トレーニング作成イベント フォーム](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="0d197-242">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="0d197-243">専門家検索</span><span class="sxs-lookup"><span data-stu-id="0d197-243">Expert Finder</span></span>

<span data-ttu-id="0d197-244">専門家検索は、スキル、興味、教育属性に基づいて特定の組織メンバーを識別する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-244">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="0d197-245">メンバーは、Azure Active Directory ユーザー プロファイルのキーワード検索と一致する組織内のエキスパートを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0d197-245">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="0d197-246">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-246">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![専門家検索の検索結果のデモ](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="0d197-248">FAQ プラス</span><span class="sxs-lookup"><span data-stu-id="0d197-248">FAQ Plus</span></span>

<span data-ttu-id="0d197-249">会話型 Q&A ボットは、ユーザーからよく寄せられる質問に回答する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="0d197-249">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="0d197-250">ただし、ほとんどのボットは、ボットに障害が発生したときにループ内に人間がいないため、意味のある方法でユーザーとやり取りできません。</span><span class="sxs-lookup"><span data-stu-id="0d197-250">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="0d197-251">FAQ ボットは フレンドリーな Q&A ボットですが、ボットが役立たないときには人間が介在するようにします。</span><span class="sxs-lookup"><span data-stu-id="0d197-251">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="0d197-252">ボットに質問をすることができ、知識ベースに含まれている場合、ボットは回答を返します。</span><span class="sxs-lookup"><span data-stu-id="0d197-252">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="0d197-253">そうでない場合、ボットはユーザーがクエリを送信できるようにします。クエリは、チーム内からの通知に基づいて行動することでサポートを提供するのに役立つ、事前に構成された専門家チームに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="0d197-253">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="0d197-254">**FAQ プラス** の最新リリースは、専門家チームが以下を完了できるようにすることにより、改善された Q&A 解決をサポートします。</span><span class="sxs-lookup"><span data-stu-id="0d197-254">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="0d197-255">&#x2714; メッセージ拡張機能を使用して、ナレッジベースに新しい Q&A を直接追加します。</span><span class="sxs-lookup"><span data-stu-id="0d197-255">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="0d197-256">&#x2714; ボットによって追加された Q&A ペアを編集および削除します。</span><span class="sxs-lookup"><span data-stu-id="0d197-256">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="0d197-257">&#x2714; Q&A の改訂履歴を追跡します。</span><span class="sxs-lookup"><span data-stu-id="0d197-257">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="0d197-258">&#x2714; [アダプティブ カード](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)として表示する追加の詳細を含む回答を構成します。</span><span class="sxs-lookup"><span data-stu-id="0d197-258">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="0d197-259">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-259">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ プラス GIF](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a><span data-ttu-id="0d197-261">サポート アプリの&#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-261">Get Support App &#9734;</span></span>

<span data-ttu-id="0d197-262">Get Support アプリは、Microsoft Teams を使用している組織が使用して、一連のユーザーが監督者に支援を要求できるようすることができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-262">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="0d197-263">このアプリには、次のようなさまざまな機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0d197-263">This app includes various features, such as:</span></span>
-   <span data-ttu-id="0d197-264">Power App からさまざまなカテゴリのサポートを要求する</span><span class="sxs-lookup"><span data-stu-id="0d197-264">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="0d197-265">誰が割り当てられているか通知を要求者に送信する</span><span class="sxs-lookup"><span data-stu-id="0d197-265">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="0d197-266">割り当てられた監督者に、サポートが必要なユーザーを通知する通知</span><span class="sxs-lookup"><span data-stu-id="0d197-266">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="0d197-267">SharePoint および PowerBI でのエスカレーションとパターンの分析</span><span class="sxs-lookup"><span data-stu-id="0d197-267">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="0d197-268">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-268">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![サポート Gif を取得する](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="0d197-270">Goal Tracker</span><span class="sxs-lookup"><span data-stu-id="0d197-270">Goal Tracker</span></span>

<span data-ttu-id="0d197-271">Goal Tracker アプリは、Microsoft Teams内で、組織の目標の設定、進捗状況の観察、成功の確認をサポートする包括的なソリューションです。</span><span class="sxs-lookup"><span data-stu-id="0d197-271">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="0d197-272">このアプリを使用すると、ユーザーは、専門家、個人、チーム レベルで目標を設定、追跡、更新できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-272">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="0d197-273">また、チーム メンバーは、集中力を維持し、順調に進めるために、タイムリーなリマインダーと状態の更新情報を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="0d197-273">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="0d197-274">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![目標の設定](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![設定した目標の表示](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="0d197-277">Great Ideas</span><span class="sxs-lookup"><span data-stu-id="0d197-277">Great Ideas</span></span>

<span data-ttu-id="0d197-278">Great Ideas アプリは、組織内のイノベーションと創造性をサポートし、力を与えます。</span><span class="sxs-lookup"><span data-stu-id="0d197-278">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="0d197-279">このアプリを使用すると、Microsoft Teams 内で、従業員は同僚やリーダーシップとアイデアを共有し、新しい報告を検索し、同僚の検討のために貢献にスポットライトを当て、最良の提案に投票することができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-279">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="0d197-280">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-280">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![提出されたアイデアの表示](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![アイデアの表示](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a><span data-ttu-id="0d197-283">グループ アクティビティ</span><span class="sxs-lookup"><span data-stu-id="0d197-283">Group Activities</span></span>

<span data-ttu-id="0d197-284">グループ アクティビティは、チームの所有者が Microsoft Teamsの コンテキスト内でアクティビティ グループをすばやく作成し、コラボレーション ワークフローを管理するのを容易にする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-284">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="0d197-285">アクティビティ作成者は、アクティビティを作成し、チーム メンバーをグループにランダムに配布し、オプションで、アクティビティが完了するまでボットにリマインダーを送信させることができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-285">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="0d197-286">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-286">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Teams 内のグループ アクティビティのリスト](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![チャネル内のグループ アクティビティ通知メッセージ](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="0d197-289">Grow Your Skills</span><span class="sxs-lookup"><span data-stu-id="0d197-289">Grow Your Skills</span></span>

<span data-ttu-id="0d197-290">Grow Your Skills アプリは、従業員が組織の補助的なプロジェクトに貢献し、新しいスキルを同時に学習できるようにして、プロフェッショナルな成長と開発をサポートします。</span><span class="sxs-lookup"><span data-stu-id="0d197-290">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="0d197-291">すべての Teams 環境内で、従業員はこのアプリを使用して、自分の興味に合った機会を見つけ、同僚との有意義な共同作業を行い、新しいレベルの専門知識と能力を取得できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-291">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="0d197-292">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![使用可能なプロジェクト ビュー](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![閲覧者の取得したスキル ビュー](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="0d197-295">HR サポート</span><span class="sxs-lookup"><span data-stu-id="0d197-295">HR Support</span></span>

<span data-ttu-id="0d197-296">HR サポート ボットはフレンドリーな Q&A ボットであり、サポートができない場合に HR チームのサポート プロフェッショナル/エキスパートをループに入れます。</span><span class="sxs-lookup"><span data-stu-id="0d197-296">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="0d197-297">ボットに質問をすることができ、知識ベースに含まれている場合、ボットは回答を返します。</span><span class="sxs-lookup"><span data-stu-id="0d197-297">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="0d197-298">そうでない場合、ボットはユーザーがクエリを送信できるようにします。クエリは、チーム内からの通知に基づいて行動することでサポートを提供するのに役立つ、事前に構成された専門家チームに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="0d197-298">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="0d197-299">さらに、ボットは、質問で事前に構成されたタグを検索することにより、推奨される HR ポリシー/質問へのリンクを提案します。</span><span class="sxs-lookup"><span data-stu-id="0d197-299">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="0d197-300">これらのタイルは、クイックリファレンスとして関連するタブにもあります。</span><span class="sxs-lookup"><span data-stu-id="0d197-300">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="0d197-301">HR サポートは、軽量の QnA に適しています。また、組織内で新しいプロジェクトやイニシアチブを立ち上げるときに迅速なサポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="0d197-301">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="0d197-302">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-302">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR サポート](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="0d197-304">アイスブレーカー</span><span class="sxs-lookup"><span data-stu-id="0d197-304">Icebreaker</span></span>

<span data-ttu-id="0d197-305">アイスブレーカーは、[Microsoft Teams ボット](../bots/what-are-bots.md)で、毎週 2 人のランダムなチーム メンバーをペアにして、チームを近づけることができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-305">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="0d197-306">ボットは、両方のメンバーに有効な空き時間を自動的に提案することで、スケジュール設定を簡単にします。</span><span class="sxs-lookup"><span data-stu-id="0d197-306">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="0d197-307">このアプリで個人的なつながりを強化し、緊密に結びついたコミュニティを構築します。</span><span class="sxs-lookup"><span data-stu-id="0d197-307">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="0d197-308">アイスブレーカー アプリは、チーム全体で個人的なつながりを促進するだけでなく、組織内で関心に基づいたコミュニティを育成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0d197-308">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="0d197-309">たとえば、このアプリを DevOps の共同作業グループに使用して、アイデアやベストプラクティスを組織全体に有機的に広めることができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-309">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="0d197-310">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-310">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![アイスブレーカー アプリ](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="0d197-312">Incentives</span><span class="sxs-lookup"><span data-stu-id="0d197-312">Incentives</span></span>

<span data-ttu-id="0d197-313">Incentives は、トレーニングや変更管理イニシアチブなどの指定されたアクティビティへのインセンティブ付き従業員の参加を管理および追跡する [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="0d197-313">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="0d197-314">管理者は、アプリを使用して、指定されたアクティビティを確立し、完了のためにポイントを割り当て、報酬に必要な適格ポイント レベルを指定します。</span><span class="sxs-lookup"><span data-stu-id="0d197-314">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="0d197-315">従業員は、アプリを使用して蓄積されたポイントを表示し、資格に達したら、償還可能な報酬を要求して請求します。</span><span class="sxs-lookup"><span data-stu-id="0d197-315">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="0d197-316">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-316">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Incentives アプリのデモ](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="0d197-318">Incident Reporter</span><span class="sxs-lookup"><span data-stu-id="0d197-318">Incident Reporter</span></span>

<span data-ttu-id="0d197-319">Incident Reporter は、組織内のインシデントの管理を最適化する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-319">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="0d197-320">ボットは、自動化されたインシデント データ収集、カスタマイズされたインシデント レポート、関連する利害関係者への通知、エンドツーエンドのインシデント追跡を容易にします。</span><span class="sxs-lookup"><span data-stu-id="0d197-320">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="0d197-321">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-321">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Incident Reporter グループ範囲ビュー](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Incident Reporter 個人範囲ビュー](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection-9734"></a><span data-ttu-id="0d197-324">検査&#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-324">Inspection &#9734;</span></span>

 <span data-ttu-id="0d197-325">検査は、フロント ライン ワーカーが場所から資産や機器までを検査できる Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-325">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="0d197-326">たとえば、小売店、製造工場、自動車やコンピューターなどです。</span><span class="sxs-lookup"><span data-stu-id="0d197-326">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="0d197-327">このソリューションには、それぞれ異なる種類のユーザーを対象とした 2 つのアプリがあります。</span><span class="sxs-lookup"><span data-stu-id="0d197-327">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="0d197-328">このアプリは、フロント ラインの作業者が資産やエリアを検査したり、製品やサービスの品質を管理したり、職場で安全を維持したりできる機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="0d197-328">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="0d197-329">検査中に見つかった問題に対処するために、チーム メンバー間のコミュニケーションが容易です。</span><span class="sxs-lookup"><span data-stu-id="0d197-329">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="0d197-330">このアプリは、マネージャーが問題の解決を迅速に行い、傾向を強調する簡単なレポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="0d197-330">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="0d197-331">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![検査の概要](../assets/images/inspection-app.png)  


## <a name="issue-reporting-9734"></a><span data-ttu-id="0d197-333">問題の報告&#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-333">Issue Reporting &#9734;</span></span>

<span data-ttu-id="0d197-334">問題報告アプリは、従業員とマネージャーが問題の発生と管理を支援します。</span><span class="sxs-lookup"><span data-stu-id="0d197-334">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="0d197-335">これは、問題を報告するための問題報告アプリと、問題を管理するための問題の管理アプリの 2 つのアプリで構成されています。</span><span class="sxs-lookup"><span data-stu-id="0d197-335">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="0d197-336">チーム マネージャーは、問題の管理アプリを使用して、Microsoft Teams メッセージと Planner タスクがアプリによって作成されるチャネルを含むアプリ エクスペリエンスを構成します。</span><span class="sxs-lookup"><span data-stu-id="0d197-336">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="0d197-337">マネージャーは、ユーザーが問題を報告するときに詳細を収集するテンプレート フォームを作成するためにもアプリを使用します。</span><span class="sxs-lookup"><span data-stu-id="0d197-337">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="0d197-338">たとえば、問題テンプレート フォームを確認、編集、または削除します。</span><span class="sxs-lookup"><span data-stu-id="0d197-338">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="0d197-339">また、アプリを使用して、チームの問題を確認し、問題履歴を報告し、問題の解決を効率的に管理することもできます。</span><span class="sxs-lookup"><span data-stu-id="0d197-339">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="0d197-340">従業員は、問題報告アプリを使用して、問題の解決に必要な問題と詳細を記録します。</span><span class="sxs-lookup"><span data-stu-id="0d197-340">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="0d197-341">アプリは、既存の問題を変更および解決し、個人またはチームの問題の大きなビューを取得するためにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="0d197-341">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="0d197-342">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-342">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Issue reporting team view](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="0d197-344">新入社員オンボーディング</span><span class="sxs-lookup"><span data-stu-id="0d197-344">New Employee Onboarding</span></span> 

<span data-ttu-id="0d197-345">New Employee Onboarding は、組織が新入社員教育で、従業員に一貫した高品質のオンボーディング エクスペリエンスを提供できるようにする Microsoft Teams と [SharePoint New Employee Onboarding が統合されたソリューション](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-345">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="0d197-346">このアプリは、人事チームと採用マネージャーがオリエンテーションと導入プロセス全体で関連情報を提供するために使用でき、新入社員がフィードバックを共有し、紹介を提供し、オンボーディング タスクを完了するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-346">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="0d197-347">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-347">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="0d197-348">**新入社員のウェルカム カード** ![新入社員のウェルカムカードの画像](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="0d197-348">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="0d197-349">**新入社員のチェックリスト** ![新入社員のチェックリストの画像](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="0d197-349">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="0d197-350">オープン バッジ</span><span class="sxs-lookup"><span data-stu-id="0d197-350">Open Badges</span></span>

<span data-ttu-id="0d197-351">オープン バッジは、個人が Teams コンテキスト内でデジタル学習資格情報バッジを取得して、どこでも共有できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-351">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="0d197-352">第三者デジタル バッジ発行機関である [Badgr](https://badgr.org/) の機能を使用して、授与されたバッジは受信者の Badgr プロファイルに記録され、生涯学習の豊富な画像を作成して共有するために利用できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-352">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="0d197-353">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![使用可能なバッジの画像](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![授与されたバッジ ビュー](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="0d197-356">ポーリング</span><span class="sxs-lookup"><span data-stu-id="0d197-356">Poll</span></span> 

<span data-ttu-id="0d197-357">Poll は、チャットまたはチャネルで投票をすばやく作成して送信し、チームの意見や好みを収集できるようにする Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-357">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="0d197-358">このアプリは、デスクトップ、ブラウザー、iOS、Android のすべての Teams プラットフォーム クライアントでサポートされており、Microsoft365 サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="0d197-358">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="0d197-359">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-359">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Teams ビューで投票を作成する](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="0d197-361">クイック応答</span><span class="sxs-lookup"><span data-stu-id="0d197-361">Quick Responses</span></span>

<span data-ttu-id="0d197-362">クイック応答は、ユーザーのよくある質問 (FAQ) に効果的に回答するための堅牢なソリューションを提供する Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-362">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="0d197-363">各クエリに手動で継続的に情報を繰り返す代わりに、アプリは、Teams [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)を介してインタラクティブなユーザー エクスペリエンスのための応答のライブラリを構築します。</span><span class="sxs-lookup"><span data-stu-id="0d197-363">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="0d197-364">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![応答のサンプル ビュー](../assets/images/quick-responses.png)

## <a name="rapid-assist-9734"></a><span data-ttu-id="0d197-366">迅速なアシスト&#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-366">Rapid Assist &#9734;</span></span>

<span data-ttu-id="0d197-367">Rapid Assist は、Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) ベースのアプリです。お客様に対する関係者は、迅速な回答の取得、情報の検索、オープンな要求のフォローアップを行い、専門家が質問に答えるのに役立つ通話を迅速に受け取る通知を受信できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-367">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="0d197-368">Microsoft [Power Apps](/powerapps/powerapps-overview) と [Power Automate](/power-automate/getting-started)を使用して構築されたアプリは、Microsoft Teams と深く統合され、組織はフロントライン ワーカーを企業の連絡員と簡単に接続して、顧客のクエリを解決し、優れたカスタマー エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-368">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="0d197-369">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![エンド ユーザー要求インターフェイス](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![エキスパート 要求ビュー](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="0d197-372">反映</span><span class="sxs-lookup"><span data-stu-id="0d197-372">Reflect</span></span> 

<span data-ttu-id="0d197-373">Reflect は、チーム メンバーがチーム内の同僚やグループリーダーと感情的に幸福な状態を直接共有するための安全かつ包括的なリソースを提供する Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-373">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="0d197-374">このアプリは、チャネル、グループ、会議、一対一チャットで利用でき、チェックイン応答は、パブリック、プライベートから送信者、または完全に匿名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-374">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="0d197-375">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="0d197-376">**ウェルビーイング投票**</span><span class="sxs-lookup"><span data-stu-id="0d197-376">**Well-being poll**</span></span>
    
    ![Reflect アプリのユーザー投票](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="0d197-378">リモート サポート</span><span class="sxs-lookup"><span data-stu-id="0d197-378">Remote Support</span></span>

<span data-ttu-id="0d197-379">リモート サポートは、組織全体のサポート要求者と内部サポート チームの間に焦点を絞ったインターフェイスを提供する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="0d197-379">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="0d197-380">エンド ユーザーは、サポートの要求を送信、編集、取り消すことができ、サポート チームはすべての Teams プラットフォーム内で要求に応答、管理、更新できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-380">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="0d197-381">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![サポート要求フォーム](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![サポート要求の詳細](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="0d197-384">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="0d197-384">Request-a-team</span></span>

<span data-ttu-id="0d197-385">Request-a-team は、企業組織の新しいチーム作成を最適化する Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-385">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="0d197-386">このアプリは、ウィザードでガイドされたリクエスト フォーム、組み込み承認プロセス、要求状態ダッシュボード、自動化されたチーム ビルドの統合を通じて、新しいチーム インスタンスを作成する際の標準化とベスト プラクティスをサポートします。</span><span class="sxs-lookup"><span data-stu-id="0d197-386">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="0d197-387">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-387">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![Request-a-team のスタート ページ ビュー](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Request-a-team のウィザード ページ ビュー](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="0d197-390">Scrums for Channels</span><span class="sxs-lookup"><span data-stu-id="0d197-390">Scrums for Channels</span></span>

<span data-ttu-id="0d197-391">Scrums for Channels は、ユーザーが Microsoft Teams 内のチャネルでスクラムをスケジュールして実行できるようにするスクラム アシスタント アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-391">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="0d197-392">このアプリは、リモート チームや、地理的に異なる場所やタイムゾーンのメンバーで構成されるチームが毎日の更新情報を共有し、スクラム スタンドアップ ミーティングに確実に参加できるようにするのに最適です。</span><span class="sxs-lookup"><span data-stu-id="0d197-392">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="0d197-393">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="0d197-394">グループ チャットでスクラム ミーティングを実施するには、[Scrums for Group Chat](#scrums-for-group-chat) アプリ テンプレートを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0d197-394">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrums for Channels の設定ビュー](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums for Channels のチーム メンバー ステータス ビュー](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="0d197-397">Scrums for Group Chat</span><span class="sxs-lookup"><span data-stu-id="0d197-397">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="0d197-398">Scrums Status アプリ テンプレートは更新され、Scrums for Group Chat になりました。</span><span class="sxs-lookup"><span data-stu-id="0d197-398">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="0d197-399">Scrums for Group Chat は、グループ チャットのメンバーが非同期スタンドアップ ミーティングを実行し、毎日の更新情報を簡単に共有できるようにする、サポート的なスクラム アシスタントです。</span><span class="sxs-lookup"><span data-stu-id="0d197-399">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="0d197-400">これにより、グループ チャットのすべてのメンバーがスクラムに貢献し、実行中のスクラムで他のメンバーが行った更新情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-400">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="0d197-401">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-401">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums for Group Chat のデモ](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="0d197-403">今すぐ共有</span><span class="sxs-lookup"><span data-stu-id="0d197-403">Share Now</span></span> 

<span data-ttu-id="0d197-404">Share Now アプリは、ユーザーがチーム環境内でコンテンツを簡単に共有できるようにすることで、同僚間の積極的な情報交換を促進します。</span><span class="sxs-lookup"><span data-stu-id="0d197-404">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="0d197-405">ユーザーはアプリを使用して、関心のあるアイテムをチーム メンバーと共有し、新しい共有コンテンツを見つけ、環境設定を設定し、後で読むためにお気に入りをブックマークします。</span><span class="sxs-lookup"><span data-stu-id="0d197-405">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="0d197-406">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-406">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![コンテンツの選択ビュー](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="0d197-408">SharePoint リスト検索</span><span class="sxs-lookup"><span data-stu-id="0d197-408">SharePoint List Search</span></span>

<span data-ttu-id="0d197-409">Microsoft Teams でのコラボレーションでは、SharePoint リストのアイテム内に含まれる情報を参照することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="0d197-409">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="0d197-410">問題のアイテムへのリンクを貼り付けるだけで、全員が会話からコンテキストを切り替え、必要な情報を見つけてから、会話を続けるために Teams に戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-410">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="0d197-411">会話が続くと、通常、ユーザーは参照アイテムに何度も戻って新しいコメントを確認し、アイテムに含まれる情報の記憶を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0d197-411">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="0d197-412">このコンテキストの切り替えは、スムーズなコラボレーションへの障壁を生み出し、亀裂を通り抜ける物事のレシピです。</span><span class="sxs-lookup"><span data-stu-id="0d197-412">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="0d197-413">このような問題を軽減するために、リスト検索アプリ テンプレートをお届けします。</span><span class="sxs-lookup"><span data-stu-id="0d197-413">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="0d197-414">何百万人ものユーザーが SharePoint を使用して、組織のコアワークフローの一部を強化しています。</span><span class="sxs-lookup"><span data-stu-id="0d197-414">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="0d197-415">ただし、リストを中心に共同作業を行うのは特に面倒です。</span><span class="sxs-lookup"><span data-stu-id="0d197-415">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="0d197-416">Microsoft Teams のリスト検索アプリ テンプレートを使用すると、ユーザーは SharePoint リスト アイテムの情報をチャットの会話内に直接挿入して、チャットにリンクを挿入するだけで発生するコンテキストの切り替えを軽減できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-416">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="0d197-417">情報は読みやすい自動書式カードとして挿入され、ユーザーが会話に参加し続けるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0d197-417">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="0d197-418">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-418">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![リスト検索アプリ](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="0d197-420">Staff Check-ins</span><span class="sxs-lookup"><span data-stu-id="0d197-420">Staff Check-ins</span></span>

<span data-ttu-id="0d197-421">Staff Check-ins は、[Power Apps](/powerapps/powerapps-overview) ベースのアプリであり、ビジネス担当者と現場担当者の間の監視コミュニケーションを可能にします。</span><span class="sxs-lookup"><span data-stu-id="0d197-421">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="0d197-422">スタッフは、タイムクリティカルな情報とステータスの更新情報を、スケジュール ベースまたはアドホック ベースで、Teams から直接簡単に提供できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-422">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="0d197-423">このアプリは、リアルタイムの位置情報、写真、メモのほか、リマインダー通知と自動ワークフローをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="0d197-423">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="0d197-424">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-424">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![チェックインの作成ビュー](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="0d197-426">アンケート</span><span class="sxs-lookup"><span data-stu-id="0d197-426">Survey</span></span>

<span data-ttu-id="0d197-427">Survey は、チャットまたはチャネルで調査を作成してデータを収集し、実用的な洞察を得ることができる Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="0d197-427">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="0d197-428">このアプリは、デスクトップ、ブラウザー、iOS、Android のすべての Teams プラットフォーム クライアントでサポートされており、Microsoft365 サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="0d197-428">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="0d197-429">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-429">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Teams ビューでアンケートを作成する](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="virtual-rounding-9734"></a><span data-ttu-id="0d197-431">仮想丸め&#9734;</span><span class="sxs-lookup"><span data-stu-id="0d197-431">Virtual Rounding &#9734;</span></span>

<span data-ttu-id="0d197-432">病院や緊急電話のプロバイダーは、1 日に数十回、多くの場合何百回もの "ラウンド" を行います。</span><span class="sxs-lookup"><span data-stu-id="0d197-432">Hospital and emergency room providers make dozens, and often hundreds of “rounds” per day.</span></span> <span data-ttu-id="0d197-433">患者に対するこれらの迅速なチェックインは、患者がどのように行っているのかの状態チェックを提供し、患者の懸念に対処することを目的とします。</span><span class="sxs-lookup"><span data-stu-id="0d197-433">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="0d197-434">丸めは、患者が複数の種類のプロバイダーによって監視されるのを確実にするための不可欠な方法ですが、各プロバイダーから、新しいマスク、および新しい一連のテープを使用する必要がある各訪問について、PPE の大きなドレインを表します。</span><span class="sxs-lookup"><span data-stu-id="0d197-434">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="0d197-435">このアプリ テンプレートを使用すると、医療労働者は、プロバイダーと患者の間の Microsoft Teams 会議を通じて、事実上簡単にラウンドを実施できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-435">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="0d197-436">仮想丸めソリューションは、Microsoft Health and Life Sciences ブログの投稿 [でも参照されています](https://aka.ms/teamsvirtualrounding)。</span><span class="sxs-lookup"><span data-stu-id="0d197-436">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="0d197-437">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-437">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![仮想丸め](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="0d197-439">訪問者の管理</span><span class="sxs-lookup"><span data-stu-id="0d197-439">Visitor Management</span></span>

<span data-ttu-id="0d197-440">Visitor Management アプリを使用すると、組織と従業員は、Microsoft Teams から直接、オンサイトの訪問者プロセスを簡単かつ効率的に管理できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-440">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="0d197-441">このアプリを使用すると、従業員は訪問者の要求を作成し、訪問者のダッシュボードを介して要求状態を一元的に追跡し、訪問者が到着したときにリアルタイムの通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="0d197-441">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="0d197-442">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-442">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![要求の作成ビュー](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![訪問者到着通知](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a><span data-ttu-id="0d197-445">Workplace の特典</span><span class="sxs-lookup"><span data-stu-id="0d197-445">Workplace Awards</span></span>

<span data-ttu-id="0d197-446">Workplace Awards は、現代の職場での認識を促進し、従業員の感謝の文化を促進するための前向きなフレームワークを提供する Teams アプリ テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="0d197-446">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="0d197-447">このアプリを使用すると、従業員の報酬と表彰 (R&R) プログラムを設定および管理できます。このプログラムでは、従業員が同僚を簡単に指名して承認し、 R&R リーダーが提出された指名を表示し、賞を授与し、受領者を発表できます。</span><span class="sxs-lookup"><span data-stu-id="0d197-447">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="0d197-448">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="0d197-448">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="0d197-449">Workplace Awards の推薦カード</span><span class="sxs-lookup"><span data-stu-id="0d197-449">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Workplace Awards のリスト タブ](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="0d197-451">見たいアプリ テンプレートのアイデアがありますか?</span><span class="sxs-lookup"><span data-stu-id="0d197-451">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="0d197-452">[ある場合はご連絡ください](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。</span><span class="sxs-lookup"><span data-stu-id="0d197-452">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
