---
title: Microsoft Teams アプリ テンプレート
description: Microsoft Teams プラットフォーム用のアプリ テンプレートのリンクと説明
ms.topic: reference
keywords: Microsoft Teams テンプレートのサンプル デモ
ms.author: lajanuar
author: laujan
ms.openlocfilehash: ac2062e8f62ee52a53c6e129301e2a5615110789
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475964"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="ccd89-104">Microsoft Teams 用のアプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="ccd89-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="ccd89-105">アプリ テンプレートは、オープン ソースで、GitHub で利用できる Microsoft Teams 用の完全なアプリの例です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="ccd89-106">各アプリ テンプレートには、組織用に展開してインストールするための詳細な手順が記載されています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="ccd89-107">サンプル アプリも提供されているため、すぐにインストールして使用を開始できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="ccd89-108">完全なソースコードも利用できるので、詳細を調べたり、コードをフォークして特定のニーズに合わせて変更したりできます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="ccd89-109">すべてのアプリテンプレートは [MIT ライセンス](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)の条件下で提供されます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
>[!NOTE] 
><span data-ttu-id="ccd89-110">Microsoft ではなく、ユーザーや組織のために、アプリ テンプレートで作成したアプリをライセンスしてサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="ccd89-111">**&#9734; 新たにリリースされたアプリ テンプレートを示します。**</span><span class="sxs-lookup"><span data-stu-id="ccd89-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="ccd89-112">主な利点</span><span class="sxs-lookup"><span data-stu-id="ccd89-112">Key benefits</span></span>

* <span data-ttu-id="ccd89-113">**クラウドに直接展開:** すべてのアプリ テンプレートには展開スクリプトが含まれており、必要なサービスをすべて Microsoft Azure または Power Platform にホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="ccd89-114">**推奨サンプルコード:** アプリ テンプレートは、セキュリティとインフラストラクチャに関して推奨されるベスト プラクティスに準拠しています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="ccd89-115">コミュニティから提出されたアプリ テンプレートの変更はすべて、適合性を確認するためにレビューされます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="ccd89-116">**カスタマイズ可能かつ拡張可能:** すべてのアプリ テンプレートは最小限の構成で展開する準備ができていますが、コード ベース全体と展開スクリプトを提供しているため、独自のニーズに合わせて簡単にカスタマイズまたは拡張できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-116">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="ccd89-117">**詳細なドキュメント:** すべてのアプリ テンプレートには、ソリューション アーキテクチャ、展開、構成の手順に関するエンドツーエンドのドキュメントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot-9734"></a><span data-ttu-id="ccd89-118">Adoption Bot &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-118">Adoption Bot &#9734;</span></span>

<span data-ttu-id="ccd89-119">Adoption Bot は Power Virtual Agent for Teams (PVA) で構築されたユーザーケア チャット ボットです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="ccd89-120">FAQPlus の PVA 版と考えることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-120">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="ccd89-121">Adoption Bot は、Microsoft 365 と Teams に関する 100 以上の一般的な質問に回答しています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="ccd89-122">既存のトピックの編集、独自のトピックの追加、および既存の FAQ の取り込みが可能です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="ccd89-123">ユーザーが追加のヘルプを必要とする場合、導入ボットはそれらを専門家に接続したり、プレミアム フロー コネクタを使用してサービス チケットを開くまで拡張することができます。このボットは、独自のボットにインストールするか、導入ハブのようなカスタム アプリに [組み込む場合があります](https://github.com/akporzondek/adoption_hub)。</span><span class="sxs-lookup"><span data-stu-id="ccd89-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.This bot can be installed on it's own or built into a custom app like the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="ccd89-124">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-124">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a><span data-ttu-id="ccd89-125">Appointment Manager &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-125">Appointment Manager &#9734;</span></span>

<span data-ttu-id="ccd89-126">Appointment Manager は、企業が Teams を経由して消費者とのバーチャルの予定を作成、管理、実施するための Teams アプリ テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-126">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="ccd89-127">消費者からの新規予定リクエストは Teams チャネルに表示され、チームのスタッフに素早く割り当てたり、割り当てし直したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-127">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="ccd89-128">予定リクエストは、カスタム タブを使用してチーム レベルまたは個人レベルで確認することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-128">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="ccd89-129">すべての予定は Teams のオンライン会議に関連付けられているため、スタッフと消費者は簡単に予定された時間に会議に参加することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-129">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="ccd89-130">アプリ テンプレートは Microsoft Bookings と統合されており、簡単に予約管理ができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-130">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="ccd89-131">スケジュールされた予定は、自動的に割り当てられたスタッフのカレンダーに表示され、消費者は会議のリンクが埋め込まれたカスタマイズ可能なメール通知とアラームを受信することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-131">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="ccd89-132">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-132">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="ccd89-133">![予定管理の概要](../assets/images/appointment-manager-overview.png)
![ Teams での予定管理](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="ccd89-133">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="ccd89-134">Ask Away</span><span class="sxs-lookup"><span data-stu-id="ccd89-134">Ask Away</span></span>

<span data-ttu-id="ccd89-135">Ask Away は、ユーザーが Teams 内で Q&A (質問と回答) セッションを実行できるようにする [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-135">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="ccd89-136">チーム メンバーは、Ask Away ボットを使用して、同僚が共有する質問を送信して賛成票を投じることができます。これにより、Q&A ホストは、チャネルまたはチャット内で最も重要な質問を簡単に収集できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-136">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="ccd89-137">ボットを使用して、Teams 会議でリアルタイムの Q&A セッションを実行でき、出席者はチャットを介してライブで質問を送信できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-137">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="ccd89-138">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![ユーザーが質問に投票するためのランキング ポップアップ ダイアログの表示](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="ccd89-140">アソシエイト インサイト</span><span class="sxs-lookup"><span data-stu-id="ccd89-140">Associate Insights</span></span>

<span data-ttu-id="ccd89-141">アソシエイト インサイトは、現場担当者が顧客の意見、感情、認識を直接キャプチャして送信できるようにする [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-141">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="ccd89-142">多くの場合、現場担当者は、一対一の連絡窓口で顧客と関わりを持つ最初の会社の代表者です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-142">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="ccd89-143">収集されたデータは、製品の改善とカスタマー エクスペリエンスの向上のために、たとえば Power BI Teams タブを介して、ビジネスチームが共同で共有および使用できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-143">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="ccd89-144">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-144">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

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

## <a name="attendance"></a><span data-ttu-id="ccd89-147">勤怠</span><span class="sxs-lookup"><span data-stu-id="ccd89-147">Attendance</span></span>

<span data-ttu-id="ccd89-148">勤怠アプリは、チームにピン留めすることができる [[Power Apps]](/powerapps/maker/canvas-apps/embed-teams-app) タブです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-148">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="ccd89-149">これは、通常、学習環境やトレーニング環境などの設定で出欠を記録するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-149">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="ccd89-150">ユーザーは、過去 30 日間までの出席をマークまたは編集し、グループ全体または個々の出席者の要約された出席レポートを表示できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-150">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="ccd89-151">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-151">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![勤怠アプリのデモ](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="ccd89-153">会議室予約</span><span class="sxs-lookup"><span data-stu-id="ccd89-153">Book-a-room</span></span>

<span data-ttu-id="ccd89-154">会議室予約は、会議室をすばやく検索して、現在時刻から 30 分間 (既定)、60 分間、90 分間予約できる [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-154">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="ccd89-155">会議室予約ボットは、個人の会話または一対一の会話を対象としています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-155">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="ccd89-156">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-156">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![会議室予約のデモ](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="ccd89-158">Building Access</span><span class="sxs-lookup"><span data-stu-id="ccd89-158">Building Access</span></span>

<span data-ttu-id="ccd89-159">Building Access は、施設の管理者が従業員が施設に滞在しているかどうかを管理、追跡、報告できるようにして、建物の占有しきい値と社会的距離の基準の管理をサポートする Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-159">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="ccd89-160">Microsoft [Power Apps](/powerapps/powerapps-overview)、[Power Automate](/power-automate/getting-started)を使用して構築されたこのアプリは、Microsoft Teams と緊密に統合されており、組織が建物の準備状況を判断し、現場アクセスの適格基準を確立し、将来の計画のための分析情報を収集できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-160">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="ccd89-161">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Building Access の予約カード](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Building Access の主なビュー](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="ccd89-164">Celebrations</span><span class="sxs-lookup"><span data-stu-id="ccd89-164">Celebrations</span></span>

<span data-ttu-id="ccd89-165">Celebrations は、チームメンバーがお互いの誕生日、記念日、その他の定期的なイベントを祝うのに役立つ Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-165">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="ccd89-166">チーム メンバー全員の特別な日を思い出し、イベント作成時に選択されたすべてのチームに友好的なメッセージを送信して、チーム メンバーがその日に特別な気分になるようにします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-166">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="ccd89-167">このアプリでは、チームメンバー全員が簡単にイベントを追加および表示できるようにするためのインターフェイスが用意されています。また、イベントを共有するチームをユーザーが選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-167">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="ccd89-168">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-168">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="ccd89-169">Checklist</span><span class="sxs-lookup"><span data-stu-id="ccd89-169">Checklist</span></span>

<span data-ttu-id="ccd89-170">Checklist は、チャットやチャネルで共有チェックリストを作成することで、チームと共同作業を行うことができる、Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-170">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="ccd89-171">このアプリは、デスクトップ、ブラウザー、iOS、Android のすべての Teams プラットフォーム クライアントでサポートされており、Microsoft365 サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-171">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="ccd89-172">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-172">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Teams ビューにチェックリストを作成する](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a><span data-ttu-id="ccd89-174">Classroom Drop-in &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-174">Classroom Drop-in &#9734;</span></span>

<span data-ttu-id="ccd89-175">Classroom Drop-in は、Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) ベースのアプリで、システム リーダーがクラスチーム (仮想教室) を見つけて、必要に応じて指定されたドロップイン期間に自分自身や他のユーザーをそのクラスチームに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-175">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="ccd89-176">Microsoft [Power Apps](/powerapps/powerapps-overview) と [Power Automate](/power-automate/getting-started) を使用して構築されたアプリは、Microsoft Teams と深く統合されており、教育機関は、ビジネス要件に応じてクラスチームに関連する関係者へのアクセスを提供することで、ハイブリッドな学習環境での運用を最適化することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-176">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="ccd89-177">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-177">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Classroom Drop-in リクエスト](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="ccd89-179">社内コミュニケーター</span><span class="sxs-lookup"><span data-stu-id="ccd89-179">Company Communicator</span></span>

<span data-ttu-id="ccd89-180">社内コミュニケーター アプリを使用すると、企業チームはチャットを介して複数のチームまたは多数の従業員向けのメッセージを作成および送信できます。これにより、組織は共同作業を行う場所で従業員に連絡できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-180">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="ccd89-181">このテンプレートは、新しいイニシアチブの発表、従業員のオンボーディング、最新の学習と能力開発、組織全体のブロードキャストなど、複数のシナリオに利用できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-181">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="ccd89-182">このアプリは、指定されたユーザーがメッセージを作成、プレビュー、共同作業、送信するための簡単なインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-182">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="ccd89-183">これは、メッセージを確認または操作したユーザーの数に関するカスタム テレメトリなどのカスタム ターゲット通信機能を構築するための基盤を提供します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-183">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="ccd89-184">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-184">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![社内コミュニケーターの作成ボックス ビュー](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="ccd89-186">Contact Group Lookup</span><span class="sxs-lookup"><span data-stu-id="ccd89-186">Contact Group Lookup</span></span>

<span data-ttu-id="ccd89-187">Contact Group Lookup アプリは、組織の連絡先グループ (以前は、「配布リストまたはコミュニケーション グループ」と呼ばれていました) を作成、アクセス、および管理するための便利で有用なアプローチを提供します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-187">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="ccd89-188">ユーザーは、すべての Teams 環境内で、グループ メンバーの表示とチャット、メンバー ステータスの表示、連絡先グループの選択したメンバーとのグループ チャットの作成をすばやく行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-188">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="ccd89-189">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-189">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation-9734"></a><span data-ttu-id="ccd89-192">Co-worker Appreciation &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-192">Co-worker Appreciation &#9734;</span></span>

<span data-ttu-id="ccd89-193">Microsoft Teams の Co-worker Appreciation テンプレートを使用すると、ユーザーは Teams のコンテキストで同僚の業績を認識することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-193">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="ccd89-194">共同作業者が同僚へのリワードを選択すると、受信者や他のチーム メンバーがチャネルの会話でタグ付けされ、チャネルのリワードの詳細についての通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-194">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="ccd89-195">アワードは Teams アプリに記録され、安全で携帯性に優れ、簡単に共有することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-195">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="ccd89-196">これは、ランキングを備えた Open Badges アプリ テンプレートの PowerApps ベースのバージョンと考えることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-196">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="ccd89-197">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-197">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![全体](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="ccd89-199">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="ccd89-199">CrowdSourcer</span></span>

<span data-ttu-id="ccd89-200">CrowdSourcer は、グループ メンバーから共同で調達された情報をチームに照会する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-200">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="ccd89-201">これは、参加者が楽しく役立つ情報リソースに積極的に参加して貢献できるようにしながら、よく寄せられる質問に回答するための優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-201">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="ccd89-202">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-202">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Crowdsource のエンドユーザーの操作](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="ccd89-204">カスタム ステッカー</span><span class="sxs-lookup"><span data-stu-id="ccd89-204">Custom Stickers</span></span>

<span data-ttu-id="ccd89-205">自己表現は健全なチーム文化の中核です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-205">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="ccd89-206">このアプリ テンプレートは、ユーザーが Microsoft Teams 内で、カスタム ステッカーや GIF を使用できるようにする[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-206">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="ccd89-207">このテンプレートは、簡単な Web ベースの構成エクスペリエンスを提供し、構成アクセス権を持つユーザーがエンド ユーザーに持たせたい GIF/ステッカー/画像をアップロードできるため、チーム全体で選択したステッカーのセットを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-207">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="ccd89-208">このアプリでは、ストレージや共有メカニズムとして SharePoint サイトや個々のチャネルにアクセスしなくても、チーム間で画像/GIF/ステッカーを簡単に共有できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-208">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="ccd89-209">たとえば、製品チームは、製品の画像や GIF をソーシャル メディア、マーケティング、販売チームとプログラムで簡単に共有できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-209">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="ccd89-210">新しい画像/GIF が利用可能になったときに、特定のチーム/個人への通知フローをトリガーすることで、このアプリを拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-210">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="ccd89-211">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-211">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![ステッカー アプリ](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="ccd89-213">従業員のアイデア</span><span class="sxs-lookup"><span data-stu-id="ccd89-213">Employee Ideas</span></span>

<span data-ttu-id="ccd89-214">Employee Ideas アプリは、Azure ベースの Great Ideas アプリ テンプレートの PowerApps 版です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-214">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="ccd89-215">このアプリでは、Teams ユーザーがアイデア キャンペーンの設定や構成を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-215">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="ccd89-216">アイデア キャンペーンとは、共通のテーマを中心にアイデアをグループ化するためのカテゴリーです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-216">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="ccd89-217">また、Teams ユーザーは次のようなアクティビティを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-217">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="ccd89-218">従業員がアイデアごとに送信する必要がある標準的な送信フォームを設定します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-218">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="ccd89-219">キャンペーンのアイデアやリストを見直して管理します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-219">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="ccd89-220">キャンペーンを変更、削除します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-220">Modify and delete campaigns.</span></span>
* <span data-ttu-id="ccd89-221">アイデアのランキングをレビューします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-221">Review leader boards of ideas.</span></span>
* <span data-ttu-id="ccd89-222">優先順位の高いアイデアに投票し、共有します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-222">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="ccd89-223">キャンペーンのアイデアを送信します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-223">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="ccd89-224">他のチーム メンバーのアイデアを表示します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-224">View other team member's idea.</span></span>
* <span data-ttu-id="ccd89-225">最も気に入ったアイデアに投票します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-225">Vote on most liked ideas.</span></span>
* <span data-ttu-id="ccd89-226">キャンペーンの他のユーザーと比較して、自分のアイデアのパフォーマンスをレビューします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-226">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="ccd89-227">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-227">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![キャンペーン ビューを管理](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="ccd89-229">E-Prescriptions</span><span class="sxs-lookup"><span data-stu-id="ccd89-229">E-Prescriptions</span></span> 

<span data-ttu-id="ccd89-230">E-Prescriptions は、患者に電子処方箋を発行するプロセスを自動化することにより、遠隔医療と仮想ケアを強化する [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-230">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="ccd89-231">医療専門家は、Teams プラットフォーム内で直接、予定をすばやく確認し、電子処方箋を生成し、電子処方箋を添付した電子メールを患者に送信できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-231">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="ccd89-232">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-232">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="ccd89-237">Employee Training</span><span class="sxs-lookup"><span data-stu-id="ccd89-237">Employee Training</span></span> 

<span data-ttu-id="ccd89-238">従業員トレーニングは、主催者が組織の学習およびトレーニング イベントを簡単に公開、追跡、促進できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-238">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="ccd89-239">このアプリを使用すると、イベント プランナーはイベント登録者にリマインダーと通知を送信できます。従業員は今後のイベントへの関心を示し、現在のイベントの最新情報を入手し、Teams メッセージング拡張機能を介して同僚とイベントの詳細を共有できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-239">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="ccd89-240">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-240">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="ccd89-241">**従業員トレーニング イベントの表示** ![従業員トレーニング タブの画像](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="ccd89-241">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="ccd89-242">**従業員トレーニング イベントの作成** ![従業員トレーニング作成イベント フォーム](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="ccd89-242">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="ccd89-243">専門家検索</span><span class="sxs-lookup"><span data-stu-id="ccd89-243">Expert Finder</span></span>

<span data-ttu-id="ccd89-244">専門家検索は、スキル、興味、教育属性に基づいて特定の組織メンバーを識別する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-244">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="ccd89-245">メンバーは、Azure Active Directory ユーザー プロファイルのキーワード検索と一致する組織内のエキスパートを見つけます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-245">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="ccd89-246">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-246">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![専門家検索の検索結果のデモ](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="ccd89-248">FAQ プラス</span><span class="sxs-lookup"><span data-stu-id="ccd89-248">FAQ Plus</span></span>

<span data-ttu-id="ccd89-249">会話型 Q&A ボットは、ユーザーからよく寄せられる質問に回答する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-249">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="ccd89-250">ただし、ほとんどのボットは、ボットに障害が発生したときにループ内に人間がいないため、意味のある方法でユーザーとやり取りできません。</span><span class="sxs-lookup"><span data-stu-id="ccd89-250">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="ccd89-251">FAQ ボットは フレンドリーな Q&A ボットですが、ボットが役立たないときには人間が介在するようにします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-251">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="ccd89-252">ボットに質問をすることができ、知識ベースに含まれている場合、ボットは回答を返します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-252">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="ccd89-253">そうでない場合、ボットはユーザーがクエリを送信できるようにします。クエリは、チーム内からの通知に基づいて行動することでサポートを提供するのに役立つ、事前に構成された専門家チームに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-253">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd89-254">**FAQ プラス** の最新リリースは、専門家チームが以下を完了できるようにすることにより、改善された Q&A 解決をサポートします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-254">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="ccd89-255">&#x2714; メッセージ拡張機能を使用して、ナレッジベースに新しい Q&A を直接追加します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-255">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="ccd89-256">&#x2714; ボットによって追加された Q&A ペアを編集および削除します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-256">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="ccd89-257">&#x2714; Q&A の改訂履歴を追跡します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-257">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="ccd89-258">&#x2714; [アダプティブ カード](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)として表示する追加の詳細を含む回答を構成します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-258">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="ccd89-259">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-259">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ プラス GIF](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a><span data-ttu-id="ccd89-261">Get Support App &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-261">Get Support App &#9734;</span></span>

<span data-ttu-id="ccd89-262">Microsoft Teams を使用している組織では、Get Support App を使用することで、任意のユーザーセットが上司にサポートを要求できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-262">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="ccd89-263">このアプリには、次のようなさまざまな機能が搭載されています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-263">This app includes various features, such as:</span></span>
-   <span data-ttu-id="ccd89-264">Power App とは異なるカテゴリのサポートを要求する</span><span class="sxs-lookup"><span data-stu-id="ccd89-264">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="ccd89-265">どのユーザーが割り当てられたかを要求者に知らせるために送信される通知</span><span class="sxs-lookup"><span data-stu-id="ccd89-265">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="ccd89-266">割り当てられた上司に、どのユーザーがサポートを必要としているか知らせるために送信される通知</span><span class="sxs-lookup"><span data-stu-id="ccd89-266">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="ccd89-267">SharePoint と PowerBI での昇格とパターンの分析</span><span class="sxs-lookup"><span data-stu-id="ccd89-267">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="ccd89-268">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-268">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Get Support Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="ccd89-270">Goal Tracker</span><span class="sxs-lookup"><span data-stu-id="ccd89-270">Goal Tracker</span></span>

<span data-ttu-id="ccd89-271">Goal Tracker アプリは、Microsoft Teams内で、組織の目標の設定、進捗状況の観察、成功の確認をサポートする包括的なソリューションです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-271">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="ccd89-272">このアプリを使用すると、ユーザーは、専門家、個人、チーム レベルで目標を設定、追跡、更新できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-272">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="ccd89-273">また、チーム メンバーは、集中力を維持し、順調に進めるために、タイムリーなリマインダーと状態の更新情報を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-273">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="ccd89-274">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a><span data-ttu-id="ccd89-277">Great Ideas</span><span class="sxs-lookup"><span data-stu-id="ccd89-277">Great Ideas</span></span>

<span data-ttu-id="ccd89-278">Great Ideas アプリは、組織内のイノベーションと創造性をサポートし、力を与えます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-278">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="ccd89-279">このアプリを使用すると、Microsoft Teams 内で、従業員は同僚やリーダーシップとアイデアを共有し、新しい報告を検索し、同僚の検討のために貢献にスポットライトを当て、最良の提案に投票することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-279">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="ccd89-280">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-280">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="ccd89-283">グループ アクティビティ</span><span class="sxs-lookup"><span data-stu-id="ccd89-283">Group Activities</span></span>

<span data-ttu-id="ccd89-284">グループ アクティビティは、チームの所有者が Microsoft Teamsの コンテキスト内でアクティビティ グループをすばやく作成し、コラボレーション ワークフローを管理するのを容易にする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-284">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="ccd89-285">アクティビティ作成者は、アクティビティを作成し、チーム メンバーをグループにランダムに配布し、オプションで、アクティビティが完了するまでボットにリマインダーを送信させることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-285">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="ccd89-286">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-286">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="grow-your-skills"></a><span data-ttu-id="ccd89-289">Grow Your Skills</span><span class="sxs-lookup"><span data-stu-id="ccd89-289">Grow Your Skills</span></span>

<span data-ttu-id="ccd89-290">Grow Your Skills アプリは、従業員が組織の補助的なプロジェクトに貢献し、新しいスキルを同時に学習できるようにして、プロフェッショナルな成長と開発をサポートします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-290">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="ccd89-291">すべての Teams 環境内で、従業員はこのアプリを使用して、自分の興味に合った機会を見つけ、同僚との有意義な共同作業を行い、新しいレベルの専門知識と能力を取得できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-291">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="ccd89-292">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a><span data-ttu-id="ccd89-295">HR サポート</span><span class="sxs-lookup"><span data-stu-id="ccd89-295">HR Support</span></span>

<span data-ttu-id="ccd89-296">HR サポート ボットはフレンドリーな Q&A ボットであり、サポートができない場合に HR チームのサポート プロフェッショナル/エキスパートをループに入れます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-296">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="ccd89-297">ボットに質問をすることができ、知識ベースに含まれている場合、ボットは回答を返します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-297">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="ccd89-298">そうでない場合、ボットはユーザーがクエリを送信できるようにします。クエリは、チーム内からの通知に基づいて行動することでサポートを提供するのに役立つ、事前に構成された専門家チームに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-298">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="ccd89-299">さらに、ボットは、質問で事前に構成されたタグを検索することにより、推奨される HR ポリシー/質問へのリンクを提案します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-299">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="ccd89-300">これらのタイルは、クイックリファレンスとして関連するタブにもあります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-300">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="ccd89-301">HR サポートは、軽量の QnA に適しています。また、組織内で新しいプロジェクトやイニシアチブを立ち上げるときに迅速なサポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-301">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="ccd89-302">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-302">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR サポート](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="ccd89-304">アイスブレーカー</span><span class="sxs-lookup"><span data-stu-id="ccd89-304">Icebreaker</span></span>

<span data-ttu-id="ccd89-305">アイスブレーカーは、[Microsoft Teams ボット](../bots/what-are-bots.md)で、毎週 2 人のランダムなチーム メンバーをペアにして、チームを近づけることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-305">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="ccd89-306">ボットは、両方のメンバーに有効な空き時間を自動的に提案することで、スケジュール設定を簡単にします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-306">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="ccd89-307">このアプリで個人的なつながりを強化し、緊密に結びついたコミュニティを構築します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-307">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="ccd89-308">アイスブレーカー アプリは、チーム全体で個人的なつながりを促進するだけでなく、組織内で関心に基づいたコミュニティを育成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-308">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="ccd89-309">たとえば、このアプリを DevOps の共同作業グループに使用して、アイデアやベストプラクティスを組織全体に有機的に広めることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-309">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="ccd89-310">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-310">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![アイスブレーカー アプリ](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="ccd89-312">Incentives</span><span class="sxs-lookup"><span data-stu-id="ccd89-312">Incentives</span></span>

<span data-ttu-id="ccd89-313">Incentives は、トレーニングや変更管理イニシアチブなどの指定されたアクティビティへのインセンティブ付き従業員の参加を管理および追跡する [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-313">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="ccd89-314">管理者は、アプリを使用して、指定されたアクティビティを確立し、完了のためにポイントを割り当て、報酬に必要な適格ポイント レベルを指定します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-314">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="ccd89-315">従業員は、アプリを使用して蓄積されたポイントを表示し、資格に達したら、償還可能な報酬を要求して請求します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-315">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="ccd89-316">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-316">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Incentives アプリのデモ](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="ccd89-318">Incident Reporter</span><span class="sxs-lookup"><span data-stu-id="ccd89-318">Incident Reporter</span></span>

<span data-ttu-id="ccd89-319">Incident Reporter は、組織内のインシデントの管理を最適化する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-319">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="ccd89-320">ボットは、自動化されたインシデント データ収集、カスタマイズされたインシデント レポート、関連する利害関係者への通知、エンドツーエンドのインシデント追跡を容易にします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-320">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="ccd89-321">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-321">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection-9734"></a><span data-ttu-id="ccd89-324">Inspection &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-324">Inspection &#9734;</span></span>

 <span data-ttu-id="ccd89-325">Inspection は、現場の最前線にいる従業員が位置情報から資産、備品まで何でも検査できる Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-325">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="ccd89-326">たとえば、小売店、製造工場、車両、または機械などがあります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-326">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="ccd89-327">このソリューションには 2 つのアプリがあり、それぞれ異なるタイプのユーザーを対象としています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-327">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="ccd89-328">このアプリは、第一線で働く人たちが資産や領域を検査したり、製品やサービスの品質を管理したり、職場の安全を維持したりすることができるようにするためのものです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-328">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="ccd89-329">検査中に発見された問題に対処するために、チーム メンバー間のコミュニケーションを促進します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-329">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="ccd89-330">このアプリでは管理者向けのシンプルなレポートを提供して、問題解決を迅速化し、傾向を強調します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-330">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="ccd89-331">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Inspection の概要](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="ccd89-333">問題レポート</span><span class="sxs-lookup"><span data-stu-id="ccd89-333">Issue Reporting</span></span>

<span data-ttu-id="ccd89-334">Issue Reporting アプリは、従業員や管理者が課題を提起し、管理するための権限を付与するためのものです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-334">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="ccd89-335">これは、問題を報告するための「問題報告アプリ」と、問題を管理するための「問題管理アプリ」の 2 つのアプリで構成されています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-335">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="ccd89-336">チーム管理者は、問題管理アプリを使用して、Microsoft Teams のメッセージやアプリで作成される Planner のタスク内のチャネルを含む、アプリのエクスペリエンスを構成します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-336">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="ccd89-337">管理者は、このアプリを使用してテンプレート フォームを作成し、ユーザーが問題を報告した場合に詳細を収集します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-337">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="ccd89-338">たとえば、問題テンプレート フォームのレビュー、編集、削除などがあります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-338">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="ccd89-339">また、アプリを使ってチームの問題をレビューしたり、問題の履歴を報告したり、問題の解決方法を効率的に管理することができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-339">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="ccd89-340">従業員は、問題報告アプリを使用して、問題とその解決に必要な詳細を記録します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-340">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="ccd89-341">このアプリは、既存の問題を修正して解決し、個人やチームの問題を大局的に俯瞰するためにも使用されています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-341">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="ccd89-342">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-342">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Issue Reporting チーム ビュー](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="ccd89-344">New Employee Onboarding</span><span class="sxs-lookup"><span data-stu-id="ccd89-344">New Employee Onboarding</span></span> 

<span data-ttu-id="ccd89-345">New Employee Onboarding は、組織が新入社員教育で、従業員に一貫した高品質のオンボーディング エクスペリエンスを提供できるようにする Microsoft Teams と [SharePoint New Employee Onboarding が統合されたソリューション](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-345">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="ccd89-346">このアプリは、人事チームと採用マネージャーがオリエンテーションと導入プロセス全体で関連情報を提供するために使用でき、新入社員がフィードバックを共有し、紹介を提供し、オンボーディング タスクを完了するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-346">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="ccd89-347">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-347">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="ccd89-348">**新入社員のウェルカム カード** ![新入社員のウェルカムカードの画像](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="ccd89-348">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="ccd89-349">**新入社員のチェックリスト** ![新入社員のチェックリストの画像](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="ccd89-349">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="ccd89-350">オープン バッジ</span><span class="sxs-lookup"><span data-stu-id="ccd89-350">Open Badges</span></span>

<span data-ttu-id="ccd89-351">オープン バッジは、個人が Teams コンテキスト内でデジタル学習資格情報バッジを取得して、どこでも共有できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-351">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="ccd89-352">第三者デジタル バッジ発行機関である [Badgr](https://badgr.org/) の機能を使用して、授与されたバッジは受信者の Badgr プロファイルに記録され、生涯学習の豊富な画像を作成して共有するために利用できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-352">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="ccd89-353">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a><span data-ttu-id="ccd89-356">Poll</span><span class="sxs-lookup"><span data-stu-id="ccd89-356">Poll</span></span> 

<span data-ttu-id="ccd89-357">Poll は、チャットまたはチャネルで投票をすばやく作成して送信し、チームの意見や好みを収集できるようにする Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-357">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="ccd89-358">このアプリは、デスクトップ、ブラウザー、iOS、Android のすべての Teams プラットフォーム クライアントでサポートされており、Microsoft365 サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-358">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="ccd89-359">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-359">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Teams ビューで投票を作成する](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="ccd89-361">クイック応答</span><span class="sxs-lookup"><span data-stu-id="ccd89-361">Quick Responses</span></span>

<span data-ttu-id="ccd89-362">クイック応答は、ユーザーのよくある質問 (FAQ) に効果的に回答するための堅牢なソリューションを提供する Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-362">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="ccd89-363">各クエリに手動で継続的に情報を繰り返す代わりに、アプリは、Teams [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)を介してインタラクティブなユーザー エクスペリエンスのための応答のライブラリを構築します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-363">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="ccd89-364">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![応答のサンプル ビュー](../assets/images/quick-responses.png)


## <a name="quiz--9734"></a><span data-ttu-id="ccd89-366">クイズ&#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-366">Quiz  &#9734;</span></span>

<span data-ttu-id="ccd89-367">Quiz はカスタム [Teams メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md) アプリで、チャットまたはチャネル内にクイズを作成し、知識チェックと瞬時の結果を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-367">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="ccd89-368">Quiz for, In-class and offline exams, Knowledge check in team, and for fun quizs in a team.</span><span class="sxs-lookup"><span data-stu-id="ccd89-368">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="ccd89-369">クイズ アプリは、Teams デスクトップ、ブラウザー、iOS、Android クライアントなど、複数のプラットフォームでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-369">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="ccd89-370">このアプリは、既存の Microsoft 365 サブスクリプションの一部として展開する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="ccd89-370">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="ccd89-371">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-371">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Teams ビューでクイズを作成する](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="ccd89-373">Rapid Assist</span><span class="sxs-lookup"><span data-stu-id="ccd89-373">Rapid Assist</span></span>

<span data-ttu-id="ccd89-374">Rapid Assist は、Microsof t[Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) ベースのアプリで、顧客対応担当者が専門家と素早く接続して迅速な回答を得たり、情報を検索したり、オープンな要求をフォローしたりして、専門家が通知を受信して素早く応答し、質問に答えるためのサポートを行います。</span><span class="sxs-lookup"><span data-stu-id="ccd89-374">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="ccd89-375">Microsoft [Power Apps](/powerapps/powerapps-overview) と [Power Automate](/power-automate/getting-started) を使用して構築されたアプリは、Microsoft Teams と深く統合されており、組織は現場の従業員と企業のリエゾンを簡単に接続して、顧客の問い合わせを解決し、優れた顧客エクスペリエンスを提供できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-375">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="ccd89-376">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-376">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![エンド ユーザー要求インターフェイス](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![専門家要求ビュー](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="ccd89-379">Reflect</span><span class="sxs-lookup"><span data-stu-id="ccd89-379">Reflect</span></span> 

<span data-ttu-id="ccd89-380">Reflect は、チーム メンバーがチーム内の同僚やグループリーダーと感情的に幸福な状態を直接共有するための安全かつ包括的なリソースを提供する Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-380">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="ccd89-381">このアプリは、チャネル、グループ、会議、一対一チャットで利用でき、チェックイン応答は、パブリック、プライベートから送信者、または完全に匿名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-381">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="ccd89-382">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-382">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="ccd89-383">**ウェルビーイング投票**</span><span class="sxs-lookup"><span data-stu-id="ccd89-383">**Well-being poll**</span></span>
    
    ![Reflect アプリのユーザー投票](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="ccd89-385">リモート サポート</span><span class="sxs-lookup"><span data-stu-id="ccd89-385">Remote Support</span></span>

<span data-ttu-id="ccd89-386">リモート サポートは、組織全体のサポート要求者と内部サポート チームの間に焦点を絞ったインターフェイスを提供する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-386">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="ccd89-387">エンド ユーザーは、サポートの要求を送信、編集、取り消すことができ、サポート チームはすべての Teams プラットフォーム内で要求に応答、管理、更新できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-387">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="ccd89-388">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-388">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a><span data-ttu-id="ccd89-391">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="ccd89-391">Request-a-team</span></span>

<span data-ttu-id="ccd89-392">Request-a-team は、企業組織の新しいチーム作成を最適化する Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-392">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="ccd89-393">このアプリは、ウィザードでガイドされたリクエスト フォーム、組み込み承認プロセス、要求状態ダッシュボード、自動化されたチーム ビルドの統合を通じて、新しいチーム インスタンスを作成する際の標準化とベスト プラクティスをサポートします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-393">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="ccd89-394">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-394">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a><span data-ttu-id="ccd89-397">Scrums for Channels</span><span class="sxs-lookup"><span data-stu-id="ccd89-397">Scrums for Channels</span></span>

<span data-ttu-id="ccd89-398">Scrums for Channels は、ユーザーが Microsoft Teams 内のチャネルでスクラムをスケジュールして実行できるようにするスクラム アシスタント アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-398">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="ccd89-399">このアプリは、リモート チームや、地理的に異なる場所やタイムゾーンのメンバーで構成されるチームが毎日の更新情報を共有し、スクラム スタンドアップ ミーティングに確実に参加できるようにするのに最適です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-399">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="ccd89-400">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-400">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="ccd89-401">グループ チャットでスクラム ミーティングを実施するには、[Scrums for Group Chat](#scrums-for-group-chat) アプリ テンプレートを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ccd89-401">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="ccd89-404">Scrums for Group Chat</span><span class="sxs-lookup"><span data-stu-id="ccd89-404">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="ccd89-405">Scrums Status アプリ テンプレートは更新され、Scrums for Group Chat になりました。</span><span class="sxs-lookup"><span data-stu-id="ccd89-405">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="ccd89-406">Scrums for Group Chat は、グループ チャットのメンバーが非同期スタンドアップ ミーティングを実行し、毎日の更新情報を簡単に共有できるようにする、サポート的なスクラム アシスタントです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-406">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="ccd89-407">これにより、グループ チャットのすべてのメンバーがスクラムに貢献し、実行中のスクラムで他のメンバーが行った更新情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-407">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="ccd89-408">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-408">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums for Group Chat のデモ](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="ccd89-410">Share Now</span><span class="sxs-lookup"><span data-stu-id="ccd89-410">Share Now</span></span> 

<span data-ttu-id="ccd89-411">Share Now アプリは、ユーザーがチーム環境内でコンテンツを簡単に共有できるようにすることで、同僚間の積極的な情報交換を促進します。</span><span class="sxs-lookup"><span data-stu-id="ccd89-411">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="ccd89-412">ユーザーはアプリを使用して、関心のあるアイテムをチーム メンバーと共有し、新しい共有コンテンツを見つけ、環境設定を設定し、後で読むためにお気に入りをブックマークします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-412">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="ccd89-413">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-413">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![コンテンツの選択ビュー](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="ccd89-415">SharePoint リスト検索</span><span class="sxs-lookup"><span data-stu-id="ccd89-415">SharePoint List Search</span></span>

<span data-ttu-id="ccd89-416">Microsoft Teams でのコラボレーションでは、SharePoint リストのアイテム内に含まれる情報を参照することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-416">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="ccd89-417">問題のアイテムへのリンクを貼り付けるだけで、全員が会話からコンテキストを切り替え、必要な情報を見つけてから、会話を続けるために Teams に戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-417">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="ccd89-418">会話が続くと、通常、ユーザーは参照アイテムに何度も戻って新しいコメントを確認し、アイテムに含まれる情報の記憶を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-418">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="ccd89-419">このコンテキストの切り替えは、スムーズなコラボレーションへの障壁を生み出し、亀裂を通り抜ける物事のレシピです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-419">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="ccd89-420">このような問題を軽減するために、リスト検索アプリ テンプレートをお届けします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-420">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="ccd89-421">何百万人ものユーザーが SharePoint を使用して、組織のコアワークフローの一部を強化しています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-421">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="ccd89-422">ただし、リストを中心に共同作業を行うのは特に面倒です。</span><span class="sxs-lookup"><span data-stu-id="ccd89-422">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="ccd89-423">Microsoft Teams のリスト検索アプリ テンプレートを使用すると、ユーザーは SharePoint リスト アイテムの情報をチャットの会話内に直接挿入して、チャットにリンクを挿入するだけで発生するコンテキストの切り替えを軽減できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-423">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="ccd89-424">情報は読みやすい自動書式カードとして挿入され、ユーザーが会話に参加し続けるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-424">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="ccd89-425">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-425">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![リスト検索アプリ](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="ccd89-427">Staff Check-ins</span><span class="sxs-lookup"><span data-stu-id="ccd89-427">Staff Check-ins</span></span>

<span data-ttu-id="ccd89-428">Staff Check-ins は、[Power Apps](/powerapps/powerapps-overview) ベースのアプリであり、ビジネス担当者と現場担当者の間の監視コミュニケーションを可能にします。</span><span class="sxs-lookup"><span data-stu-id="ccd89-428">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="ccd89-429">スタッフは、タイムクリティカルな情報とステータスの更新情報を、スケジュール ベースまたはアドホック ベースで、Teams から直接簡単に提供できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-429">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="ccd89-430">このアプリは、リアルタイムの位置情報、写真、メモのほか、リマインダー通知と自動ワークフローをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-430">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="ccd89-431">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-431">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![チェックインの作成ビュー](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="ccd89-433">Survey</span><span class="sxs-lookup"><span data-stu-id="ccd89-433">Survey</span></span>

<span data-ttu-id="ccd89-434">Survey は、チャットまたはチャネルで調査を作成してデータを収集し、実用的な洞察を得ることができる Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-434">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="ccd89-435">このアプリは、デスクトップ、ブラウザー、iOS、Android のすべての Teams プラットフォーム クライアントでサポートされており、Microsoft365 サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-435">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="ccd89-436">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-436">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Teams ビューでアンケートを作成する](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally-9734"></a><span data-ttu-id="ccd89-438">Time Tally &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-438">Time Tally &#9734;</span></span>

<span data-ttu-id="ccd89-439">プロジェクトには複数のタスクを含め、さまざまなプロジェクトを従業員に割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-439">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="ccd89-440">管理者は、従業員がこれらのタスクに費やした時間を通じてプロジェクトの進捗状況を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-440">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="ccd89-441">従業員がタイムシートを入力する必要がある場合、これは面倒な作業になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-441">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="ccd89-442">タイム 集計アプリを使用すると、従業員はモバイル デバイスを使用してタイムシートをすばやく入力し、管理者はタイムシートエントリで従業員をフォローアップする必要が生じない。</span><span class="sxs-lookup"><span data-stu-id="ccd89-442">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="ccd89-443">管理者はリソースに基づいてプロジェクトの使用率を表示し、エントリを承認または拒否できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-443">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="ccd89-444">タイムシートのコンプライアンスを確保するために、アラーム通知が送信されます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-444">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="ccd89-445">また、過去のデータと使用状況は分析に利用できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-445">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="ccd89-446">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-446">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Time Tally](../assets/images/11zon_gif.gif)


## <a name="training--9734"></a><span data-ttu-id="ccd89-448">トレーニング &#9734;</span><span class="sxs-lookup"><span data-stu-id="ccd89-448">Training  &#9734;</span></span>

<span data-ttu-id="ccd89-449">トレーニングは、 [ユーザー](../messaging-extensions/what-are-messaging-extensions.md) がチャットまたはチャネル内でトレーニングを公開し、オフラインでのナレッジ共有とスキルアップを行うカスタム Teams メッセージング拡張機能アプリです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-449">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="ccd89-450">アプリは、デスクトップ、ブラウザー、iOS、Android など、複数の Teams プラットフォーム クライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-450">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="ccd89-451">このアプリは、Microsoft 365 サブスクリプションの一部として展開する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="ccd89-451">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="ccd89-452">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-452">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Teams ビューでトレーニングを作成する](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="ccd89-454">Virtual Rounding</span><span class="sxs-lookup"><span data-stu-id="ccd89-454">Virtual Rounding</span></span>

<span data-ttu-id="ccd89-455">病院および緊急治療室のプロバイダーは、1 日に数十回、多くの場合数百 **ラウンドを** 行います。</span><span class="sxs-lookup"><span data-stu-id="ccd89-455">Hospital and emergency room providers make dozens, and often hundreds of **rounds** per day.</span></span> <span data-ttu-id="ccd89-456">患者に対するこれらの迅速なチェックは、患者がどのように行動しているかの状態チェックを行い、患者の懸念に確実な対処を行うことを目的としています。</span><span class="sxs-lookup"><span data-stu-id="ccd89-456">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="ccd89-457">回診は、患者が複数のタイプのプロバイダーによって監視されていることを確認するために必要不可欠な演習ですが、訪問のたびに、各プロバイダーで新しいマスクと新しい手袋のセットを使用しなければならないため、PPE の膨大な消耗につながります。</span><span class="sxs-lookup"><span data-stu-id="ccd89-457">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="ccd89-458">このアプリのテンプレートを使用すると、医療従事者は、プロバイダーと患者の間で Microsoft Teams の会議を介して、仮想的に簡単な回診を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-458">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="ccd89-459">Virtual Rounding のソリューションは、Microsoft Health とライフ サイエンスの[ブログ記事](https://aka.ms/teamsvirtualrounding)でも参照できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-459">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="ccd89-460">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-460">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Virtual Rounding](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="ccd89-462">Visitor Management</span><span class="sxs-lookup"><span data-stu-id="ccd89-462">Visitor Management</span></span>

<span data-ttu-id="ccd89-463">Visitor Management アプリを使用すると、組織と従業員は、Microsoft Teams から直接、オンサイトの訪問者プロセスを簡単かつ効率的に管理できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-463">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="ccd89-464">このアプリを使用すると、従業員は訪問者の要求を作成し、訪問者のダッシュボードを介して要求状態を一元的に追跡し、訪問者が到着したときにリアルタイムの通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-464">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="ccd89-465">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-465">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="ccd89-468">Workplace Awards</span><span class="sxs-lookup"><span data-stu-id="ccd89-468">Workplace Awards</span></span>

<span data-ttu-id="ccd89-469">Workplace Awards は、現代の職場での認識を促進し、従業員の感謝の文化を促進するための前向きなフレームワークを提供する Teams アプリ テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="ccd89-469">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="ccd89-470">このアプリを使用すると、従業員の報酬と表彰 (R&R) プログラムを設定および管理できます。このプログラムでは、従業員が同僚を簡単に指名して承認し、 R&R リーダーが提出された指名を表示し、賞を授与し、受領者を発表できます。</span><span class="sxs-lookup"><span data-stu-id="ccd89-470">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="ccd89-471">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="ccd89-471">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="ccd89-472">Workplace Awards の推薦カード</span><span class="sxs-lookup"><span data-stu-id="ccd89-472">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Workplace Awards のリスト タブ](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="ccd89-474">見たいアプリ テンプレートのアイデアがありますか?</span><span class="sxs-lookup"><span data-stu-id="ccd89-474">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="ccd89-475">[ある場合はご連絡ください](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。</span><span class="sxs-lookup"><span data-stu-id="ccd89-475">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
