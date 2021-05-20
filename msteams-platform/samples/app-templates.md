---
title: Microsoft Teams アプリ テンプレート
description: Microsoft Teams プラットフォーム用のアプリ テンプレートのリンクと説明
ms.topic: reference
keywords: Microsoft Teams テンプレートのサンプル デモ
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 8cfb066ee3c202fb8611a61bbde3058207a62a35
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566343"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="abb98-104">Microsoft Teams 用のアプリ テンプレート</span><span class="sxs-lookup"><span data-stu-id="abb98-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="abb98-105">アプリ テンプレートは、オープン ソースで、GitHub で利用できる Microsoft Teams 用の完全なアプリの例です。</span><span class="sxs-lookup"><span data-stu-id="abb98-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="abb98-106">各アプリ テンプレートには、組織用に展開してインストールするための詳細な手順が記載されています。</span><span class="sxs-lookup"><span data-stu-id="abb98-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="abb98-107">また、すぐにインストールして使用を開始できるサンプルアプリも提供します。</span><span class="sxs-lookup"><span data-stu-id="abb98-107">It also provides a sample app that you can install and start using immediately.</span></span> <span data-ttu-id="abb98-108">完全なソースコードも利用可能で、詳細に調べるか、コードをフォークして、特定の要件を満たすように変更することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-108">The complete source code is also available, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="abb98-109">すべてのアプリテンプレートは [MIT ライセンス](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE)の条件下で提供されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>

> [!NOTE] 
> <span data-ttu-id="abb98-110">ユーザーおよび組織向けに、アプリ テンプレートから作成されたアプリのライセンスとサポートを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="abb98-110">You must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="abb98-111">**&#9734; 新たにリリースされたアプリ テンプレートを示します。**</span><span class="sxs-lookup"><span data-stu-id="abb98-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="abb98-112">主な利点</span><span class="sxs-lookup"><span data-stu-id="abb98-112">Key benefits</span></span>

* <span data-ttu-id="abb98-113">**クラウドに直接展開:** すべてのアプリ テンプレートには展開スクリプトが含まれており、必要なサービスをすべて Microsoft Azure または Power Platform にホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="abb98-114">**推奨サンプルコード:** アプリ テンプレートは、セキュリティとインフラストラクチャに関して推奨されるベスト プラクティスに準拠しています。</span><span class="sxs-lookup"><span data-stu-id="abb98-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="abb98-115">コミュニティから提出されたアプリ テンプレートの変更はすべて、適合性を確認するためにレビューされます。</span><span class="sxs-lookup"><span data-stu-id="abb98-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="abb98-116">**カスタマイズ可能で拡張可能:** すべてのアプリ テンプレートは最小限の構成で展開されますが、コード ベーススクリプトと配置スクリプト全体が用意されているので、独自のニーズに合わせて簡単にカスタマイズまたは拡張できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-116">**Customizable and extensible:** While all app templates are deployed with minimal configuration, the entire code base and deployment scripts are provided, so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="abb98-117">**詳細なドキュメント:** すべてのアプリ テンプレートには、ソリューション アーキテクチャ、展開、構成の手順に関するエンドツーエンドのドキュメントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="abb98-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="abb98-118">導入ボット</span><span class="sxs-lookup"><span data-stu-id="abb98-118">Adoption Bot</span></span> 

<span data-ttu-id="abb98-119">導入ボットは、PVA用のパワー仮想エージェントで構築されたユーザーケアチャットボットTeams。</span><span class="sxs-lookup"><span data-stu-id="abb98-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams PVA.</span></span> <span data-ttu-id="abb98-120">これは、FAQプラスのPVAバージョンとして考えられています。</span><span class="sxs-lookup"><span data-stu-id="abb98-120">It is considered as the PVA version of FAQ Plus.</span></span> <span data-ttu-id="abb98-121">Adoption Bot は、Microsoft 365 と Teams に関する 100 以上の一般的な質問に回答しています。</span><span class="sxs-lookup"><span data-stu-id="abb98-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="abb98-122">既存のトピックを編集したり、独自のトピックを追加したり、既存の FAQ を取り込むことができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="abb98-123">ユーザーが追加のヘルプを必要とする場合、Adoption Bot は専門家への接続や、プレミアム フロー コネクタを使用して拡張し、サービス チケットを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span> <span data-ttu-id="abb98-124">このボットは、自己インストールされているか、導入 [ハブ](https://github.com/akporzondek/adoption_hub)などのカスタム アプリに組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="abb98-124">This bot is self-installed or built into a custom app, such as the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="abb98-125">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="abb98-126">導入ツール- チャンピオン管理プラットフォーム &#9734;</span><span class="sxs-lookup"><span data-stu-id="abb98-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="abb98-127">チャンピオン管理プラットフォーム (CMP) アプリ テンプレートを使用すると、チームワークのチャンピオンを管理、拡張、インスパイアして、より多くのことを達成できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="abb98-128">このアプリ テンプレートは、SharePoint Framework上に構築され、チーム内のタブに読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="abb98-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="abb98-129">グループはこのツールを活用して、プログラムのメンバーシップを管理したり、ログ記録用のスコアボードとイベントタイプを提供したり、デジタルバッジをプログラム参加者にオーバーレイするツールを提供したりできます。</span><span class="sxs-lookup"><span data-stu-id="abb98-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="abb98-130">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="abb98-131">導入ツール- Microsoft 365学習経路 (はじめに) &#9734;</span><span class="sxs-lookup"><span data-stu-id="abb98-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="abb98-132">はじめにアプリテンプレートを使用すると、Microsoft Teams内の学習経路Microsoft 365力を持って来ることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="abb98-133">このアプリテンプレートを使用すると、特定のトレーニングページや他のイントラネット資産への簡単なアクセスを許可し、コンテンツをTeams内に直接読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="abb98-134">また、会社のブランドに合わせてアプリ名やロゴを変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="abb98-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="abb98-135">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="abb98-136">予定マネージャ</span><span class="sxs-lookup"><span data-stu-id="abb98-136">Appointment Manager</span></span> 

<span data-ttu-id="abb98-137">Appointment Manager は、企業が Teams を経由して消費者とのバーチャルの予定を作成、管理、実施するための Teams アプリ テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="abb98-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="abb98-138">コンシューマーからの新しい予定要求は、Teams チャネルで表示され、チーム内のスタッフにすばやく割り当てられ、再割り当てされます。</span><span class="sxs-lookup"><span data-stu-id="abb98-138">New appointment requests from consumers are visible in Teams channels, where they are quickly assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="abb98-139">予定のリクエストは、チーム レベルまたは個人レベルでカスタム タブを使用して表示されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-139">Appointment requests are viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="abb98-140">すべての予定は Teams のオンライン会議に関連付けられているため、スタッフと消費者は簡単に予定された時間に会議に参加することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="abb98-141">アプリ テンプレートは Microsoft Bookings と統合されており、簡単に予約管理ができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="abb98-142">スケジュールされた予定は、自動的に割り当てられたスタッフのカレンダーに表示され、消費者は会議のリンクが埋め込まれたカスタマイズ可能なメール通知とアラームを受信することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="abb98-143">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="abb98-144">![予定管理の概要](../assets/images/appointment-manager-overview.png)
![ Teams での予定管理](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="abb98-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="abb98-145">Ask Away</span><span class="sxs-lookup"><span data-stu-id="abb98-145">Ask Away</span></span>

<span data-ttu-id="abb98-146">Ask Away は、q&A セッションと呼ばれる質問と回答をTeamsで実行できる[Microsoft Teamsボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Question and Answer, called Q&A sessions within Teams.</span></span> <span data-ttu-id="abb98-147">チーム メンバーは、Ask Away ボットを使用して、同僚が共有する質問を送信して賛成票を投じることができます。これにより、Q&A ホストは、チャネルまたはチャット内で最も重要な質問を簡単に収集できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="abb98-148">ボットは、Teams会議でリアルタイムの Q&A セッションを実施するために使用され、参加者はチャットを通じて質問をライブで送信できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-148">The bot is used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live through chat.</span></span>

[<span data-ttu-id="abb98-149">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![ユーザーが質問に投票するためのランキング ポップアップ ダイアログの表示](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="abb98-151">アソシエイト インサイト</span><span class="sxs-lookup"><span data-stu-id="abb98-151">Associate Insights</span></span>

<span data-ttu-id="abb98-152">アソシエイト インサイトは、現場担当者が顧客の意見、感情、認識を直接キャプチャして送信できるようにする [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="abb98-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="abb98-153">多くの場合、現場担当者は、一対一の連絡窓口で顧客と関わりを持つ最初の会社の代表者です。</span><span class="sxs-lookup"><span data-stu-id="abb98-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="abb98-154">収集されたデータは、製品の改善や顧客体験の向上のために、Power BI Teamsタブなどでビジネスチームによって共有され、共同で使用されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-154">The collected data are shared and used collaboratively by business teams, such as through a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="abb98-155">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

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

## <a name="attendance"></a><span data-ttu-id="abb98-158">勤怠</span><span class="sxs-lookup"><span data-stu-id="abb98-158">Attendance</span></span>

<span data-ttu-id="abb98-159">参加時アプリは、チームに固定されている[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)タブです。</span><span class="sxs-lookup"><span data-stu-id="abb98-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that are pinned in a team.</span></span> <span data-ttu-id="abb98-160">学習環境やトレーニング環境などの設定でのプレゼンスを記録するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="abb98-160">It is designed to record presence in settings, such as learning and training environments.</span></span> <span data-ttu-id="abb98-161">ユーザーは、過去 30 日間までの出席をマークまたは編集し、グループ全体または個々の出席者の要約された出席レポートを表示できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span> <span data-ttu-id="abb98-162">チームの出席の詳細については[、「GitHubで取得する](https://github.com/OfficeDev/microsoft-teams-apps-attendance)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="abb98-162">For more information on teams attendance, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span></span>

<span data-ttu-id="abb98-163">次の図は、出席アプリのデモを示しています。</span><span class="sxs-lookup"><span data-stu-id="abb98-163">The following image displays the attendance app demo:</span></span>  

![勤怠アプリのデモ](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="abb98-165">会議室予約</span><span class="sxs-lookup"><span data-stu-id="abb98-165">Book-a-room</span></span>

<span data-ttu-id="abb98-166">ブックルームは、ユーザーが現在の時刻から30分、60分、または90分の会議室をすばやく見つけて予約できる[Microsoft Teamsボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-166">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="abb98-167">デフォルトの時間は 30 分です。</span><span class="sxs-lookup"><span data-stu-id="abb98-167">The default time is 30 minutes.</span></span> <span data-ttu-id="abb98-168">会議室予約ボットは、個人の会話または一対一の会話を対象としています。</span><span class="sxs-lookup"><span data-stu-id="abb98-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="abb98-169">Book-a-room アプリの詳細については[、「GitHubで入手する](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="abb98-169">For more information on Book-a-room app, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span></span>  
<span data-ttu-id="abb98-170">次の図は、部屋のブックのデモを示しています。</span><span class="sxs-lookup"><span data-stu-id="abb98-170">The following image displays the Book-a-room demo:</span></span>

![会議室予約のデモ](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="abb98-172">Building Access</span><span class="sxs-lookup"><span data-stu-id="abb98-172">Building Access</span></span>

<span data-ttu-id="abb98-173">Access の構築は、施設のディレクターが管理、追跡、および従業員のオンサイトプレゼンスを報告できるようにすることで、占有しきい値と社会的な混乱の規範を構築する管理をサポートする Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-173">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="abb98-174">Microsoft [Power Apps](/powerapps/powerapps-overview)、[Power Automate](/power-automate/getting-started)を使用して構築されたこのアプリは、Microsoft Teams と緊密に統合されており、組織が建物の準備状況を判断し、現場アクセスの適格基準を確立し、将来の計画のための分析情報を収集できるようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-174">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="abb98-175">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Building Access の予約カード](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![Building Access の主なビュー](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="abb98-178">Celebrations</span><span class="sxs-lookup"><span data-stu-id="abb98-178">Celebrations</span></span>

<span data-ttu-id="abb98-179">お祝いは、チームメンバーがお互いの誕生日、記念日、およびその他の定期的なイベントを祝うために役立つTeamsアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-179">Celebrations is a Teams app that helps team members to celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="abb98-180">チーム メンバー全員の特別な日を思い出し、イベント作成時に選択されたすべてのチームに友好的なメッセージを送信して、チーム メンバーがその日に特別な気分になるようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-180">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="abb98-181">このアプリでは、チームメンバー全員が簡単にイベントを追加および表示できるようにするためのインターフェイスが用意されています。また、イベントを共有するチームをユーザーが選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-181">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="abb98-182">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-182">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="abb98-183">Checklist</span><span class="sxs-lookup"><span data-stu-id="abb98-183">Checklist</span></span>

<span data-ttu-id="abb98-184">Checklist は、チャットやチャネルで共有チェックリストを作成することで、チームと共同作業を行うことができる、Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-184">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="abb98-185">アプリは、デスクトップ ブラウザー、iOS、Android など、すべての Teamsプラットフォーム クライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="abb98-185">The app is supported across all Teams platform clients, such as desktop browser, iOS, and Android.</span></span> <span data-ttu-id="abb98-186">アプリは、Microsoft 365 サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="abb98-186">The app is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="abb98-187">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-187">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![Teams ビューにチェックリストを作成する](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="abb98-189">教室ドロップイン</span><span class="sxs-lookup"><span data-stu-id="abb98-189">Classroom Drop-in</span></span> 

<span data-ttu-id="abb98-190">Classroom Drop-in は、システム リーダーがクラス チームを見つけ、仮想教室を意味し、必要に応じて指定したドロップイン期間に、これらのクラス チームに自分自身または他のユーザーを追加できるようにする Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-190">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams, means virtual classrooms and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="abb98-191">Microsoft [Power Apps](/powerapps/powerapps-overview) と [Power Automate](/power-automate/getting-started) を使用して構築されたアプリは、Microsoft Teams と深く統合されており、教育機関は、ビジネス要件に応じてクラスチームに関連する関係者へのアクセスを提供することで、ハイブリッドな学習環境での運用を最適化することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-191">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="abb98-192">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-192">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![Classroom Drop-in リクエスト](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="abb98-194">社内コミュニケーター</span><span class="sxs-lookup"><span data-stu-id="abb98-194">Company Communicator</span></span>

<span data-ttu-id="abb98-195">社内コミュニケーター アプリを使用すると、企業チームはチャットを介して複数のチームまたは多数の従業員向けのメッセージを作成および送信できます。これにより、組織は共同作業を行う場所で従業員に連絡できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-195">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="abb98-196">このテンプレートは、新しいイニシアチブの発表、従業員のオンボーディング、最新の学習、開発や組織全体のブロードキャストなど、複数のシナリオに利用できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-196">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning, and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="abb98-197">このアプリは、指定されたユーザーがメッセージを作成、プレビュー、共同作業、送信するための簡単なインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="abb98-197">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="abb98-198">これは、メッセージを確認または操作したユーザーの数に関するカスタム テレメトリなどのカスタム ターゲット通信機能を構築するための基盤を提供します。</span><span class="sxs-lookup"><span data-stu-id="abb98-198">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="abb98-199">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-199">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![社内コミュニケーターの作成ボックス ビュー](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="abb98-201">Contact Group Lookup</span><span class="sxs-lookup"><span data-stu-id="abb98-201">Contact Group Lookup</span></span>

<span data-ttu-id="abb98-202">連絡先グループ検索アプリは、組織の連絡先グループ (以前は配布リストまたは通信グループと呼ばれていた) を作成、アクセス、および管理するための便利で便利な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="abb98-202">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups, formerly known as distribution lists or communication groups.</span></span> <span data-ttu-id="abb98-203">ユーザーは、すべての Teams 環境内で、グループ メンバーの表示とチャット、メンバー ステータスの表示、連絡先グループの選択したメンバーとのグループ チャットの作成をすばやく行うことができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-203">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="abb98-204">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-204">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

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

## <a name="co-worker-appreciation"></a><span data-ttu-id="abb98-207">同僚の感謝</span><span class="sxs-lookup"><span data-stu-id="abb98-207">Co-worker Appreciation</span></span> 

<span data-ttu-id="abb98-208">Microsoft Teams の Co-worker Appreciation テンプレートを使用すると、ユーザーは Teams のコンテキストで同僚の業績を認識することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-208">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="abb98-209">共同作業者が同僚へのリワードを選択すると、受信者や他のチーム メンバーがチャネルの会話でタグ付けされ、チャネルのリワードの詳細についての通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-209">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="abb98-210">アワードは Teams アプリに記録され、安全で携帯性に優れ、簡単に共有することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-210">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="abb98-211">これは、PowerApps ベースのバージョンのオープン バッジ アプリ テンプレートと見なされ、スコア ボードが付きます。</span><span class="sxs-lookup"><span data-stu-id="abb98-211">This is considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="abb98-212">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-212">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![全体](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="abb98-214">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="abb98-214">CrowdSourcer</span></span>

<span data-ttu-id="abb98-215">CrowdSourcer は、グループ メンバーから共同で調達された情報をチームに照会する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-215">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="abb98-216">よく寄せられる質問に答え、参加者が楽しく役立つ情報リソースに積極的に参加し、貢献できるようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-216">It helps to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="abb98-217">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-217">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Crowdsource のエンドユーザーの操作](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="abb98-219">カスタム ステッカー</span><span class="sxs-lookup"><span data-stu-id="abb98-219">Custom Stickers</span></span>

<span data-ttu-id="abb98-220">自己表現は健全なチーム文化の中核です。</span><span class="sxs-lookup"><span data-stu-id="abb98-220">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="abb98-221">このアプリ テンプレートは、ユーザーが Microsoft Teams 内で、カスタム ステッカーや GIF を使用できるようにする[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-221">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="abb98-222">このテンプレートは、構成アクセス権を持つ誰もがGIF、ステッカー、および画像をアップロードできる簡単なWebベースの設定体験を提供し、チーム全体が選択したステッカーのセットを使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-222">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs, stickers, and images they want their users to have, allowing your entire team to use any set of stickers you choose.</span></span>

<span data-ttu-id="abb98-223">このアプリはまた、ストレージや共有メカニズムとしてSharePointサイトや個々のチャネルへのアクセスを必要とせずに、チーム間で画像、GIF、ステッカーの共有を容易にできます。</span><span class="sxs-lookup"><span data-stu-id="abb98-223">This app also enables easy sharing of images, GIFs, stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="abb98-224">たとえば、製品チームは、製品イメージや GIF ファイルを、プログラムでソーシャル メディア、マーケティング、営業チームと簡単に共有できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-224">For example, product teams can easily share product images and GIFs to social media, marketing, and sales teams programmatically.</span></span> <span data-ttu-id="abb98-225">また、新しい画像、およびGIFが利用可能になったときに、特定のチームや個人に通知フローをトリガーすることによって、このアプリを拡張することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-225">One can also extend this app by triggering a notification flow to specific teams or individuals when new images, and GIFs are made available.</span></span>

[<span data-ttu-id="abb98-226">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![ステッカー アプリ](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="abb98-228">従業員のアイデア</span><span class="sxs-lookup"><span data-stu-id="abb98-228">Employee Ideas</span></span>

<span data-ttu-id="abb98-229">Employee Ideas アプリは、Azure ベースの Great Ideas アプリ テンプレートの PowerApps 版です。</span><span class="sxs-lookup"><span data-stu-id="abb98-229">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="abb98-230">このアプリでは、Teams ユーザーがアイデア キャンペーンの設定や構成を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-230">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="abb98-231">アイデア キャンペーンとは、共通のテーマを中心にアイデアをグループ化するためのカテゴリーです。</span><span class="sxs-lookup"><span data-stu-id="abb98-231">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="abb98-232">Teamsユーザーは、以下のアクティビティを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="abb98-232">Teams users can also perform the following activities:</span></span>

* <span data-ttu-id="abb98-233">従業員が各アイデアに対して提出する必要がある標準の提出フォームを構成します。</span><span class="sxs-lookup"><span data-stu-id="abb98-233">Configure a standard submission form that employees must submit for each idea.</span></span> 
* <span data-ttu-id="abb98-234">キャンペーンのアイデアやリストを見直して管理します。</span><span class="sxs-lookup"><span data-stu-id="abb98-234">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="abb98-235">キャンペーンを変更、削除します。</span><span class="sxs-lookup"><span data-stu-id="abb98-235">Modify and delete campaigns.</span></span>
* <span data-ttu-id="abb98-236">アイデアのランキングをレビューします。</span><span class="sxs-lookup"><span data-stu-id="abb98-236">Review leader boards of ideas.</span></span>
* <span data-ttu-id="abb98-237">優先順位の高いアイデアに投票し、共有します。</span><span class="sxs-lookup"><span data-stu-id="abb98-237">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="abb98-238">キャンペーンのアイデアを送信します。</span><span class="sxs-lookup"><span data-stu-id="abb98-238">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="abb98-239">他のチーム メンバーのアイデアを表示します。</span><span class="sxs-lookup"><span data-stu-id="abb98-239">View other team member's idea.</span></span>
* <span data-ttu-id="abb98-240">最も気に入ったアイデアに投票します。</span><span class="sxs-lookup"><span data-stu-id="abb98-240">Vote on most liked ideas.</span></span>
* <span data-ttu-id="abb98-241">キャンペーンの他のユーザーと比較して、自分のアイデアのパフォーマンスをレビューします。</span><span class="sxs-lookup"><span data-stu-id="abb98-241">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="abb98-242">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-242">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![キャンペーン ビューを管理](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="abb98-244">E-Prescriptions</span><span class="sxs-lookup"><span data-stu-id="abb98-244">E-Prescriptions</span></span> 

<span data-ttu-id="abb98-245">E-処方箋は、患者に電子処方箋を発行するプロセスを自動化することにより、遠隔医療と仮想ケアを強化する[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-245">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="abb98-246">医療専門家は、Teams プラットフォーム内で直接、予定をすばやく確認し、電子処方箋を生成し、電子処方箋を添付した電子メールを患者に送信できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-246">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="abb98-247">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

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

## <a name="employee-training"></a><span data-ttu-id="abb98-252">Employee Training</span><span class="sxs-lookup"><span data-stu-id="abb98-252">Employee Training</span></span> 

<span data-ttu-id="abb98-253">従業員トレーニングは、組織の学習イベントやトレーニング イベントを開催者が簡単に公開、追跡、促進できるMicrosoft Teamsアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-253">Employee training is a Microsoft Teams app that enables organizers to easily publish, track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="abb98-254">このアプリを使用すると、イベントプランナーはイベント登録者にリマインダーや通知を送信することができ、従業員は今後のイベントへの関心を示し、現在のイベントを最新の状態に保ち、Teamsメッセージング拡張機能を通じて同僚とイベントの詳細を共有することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-254">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues through the Teams messaging extension.</span></span>

[<span data-ttu-id="abb98-255">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="abb98-256">**従業員トレーニング イベントの表示** ![従業員トレーニング タブの画像](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="abb98-256">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="abb98-257">**従業員トレーニング イベントの作成** ![従業員トレーニング作成イベント フォーム](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="abb98-257">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="abb98-258">専門家検索</span><span class="sxs-lookup"><span data-stu-id="abb98-258">Expert Finder</span></span>

<span data-ttu-id="abb98-259">専門家検索は、スキル、興味、教育属性に基づいて特定の組織メンバーを識別する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-259">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="abb98-260">メンバーは、組織内で、Azure Active Directoryユーザー プロファイルのキーワード検索に一致する専門家を検索します。</span><span class="sxs-lookup"><span data-stu-id="abb98-260">Members find experts within an organization that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="abb98-261">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![専門家検索の検索結果のデモ](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="abb98-263">FAQ プラス</span><span class="sxs-lookup"><span data-stu-id="abb98-263">FAQ Plus</span></span>

<span data-ttu-id="abb98-264">会話型 Q&A ボットは、ユーザーからよく寄せられる質問に回答する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="abb98-264">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="abb98-265">しかし、ボットが失敗したときにループに人間がいないため、ほとんどのボットはユーザーと有意義な方法で関与しません。</span><span class="sxs-lookup"><span data-stu-id="abb98-265">But, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="abb98-266">FAQ ボットは フレンドリーな Q&A ボットですが、ボットが役立たないときには人間が介在するようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-266">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="abb98-267">ボットに質問をすることができ、知識ベースに含まれている場合、ボットは回答を返します。</span><span class="sxs-lookup"><span data-stu-id="abb98-267">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="abb98-268">そうでない場合、ボットはユーザーがクエリを送信できるようにします。クエリは、チーム内からの通知に基づいて行動することでサポートを提供するのに役立つ、事前に構成された専門家チームに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-268">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="abb98-269">**FAQ プラス** の最新リリースは、専門家チームが以下を完了できるようにすることにより、改善された Q&A 解決をサポートします。</span><span class="sxs-lookup"><span data-stu-id="abb98-269">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="abb98-270">&#x2714; メッセージ拡張機能を使用して、ナレッジベースに新しい Q&A を直接追加します。</span><span class="sxs-lookup"><span data-stu-id="abb98-270">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="abb98-271">&#x2714; ボットによって追加された Q&A ペアを編集および削除します。</span><span class="sxs-lookup"><span data-stu-id="abb98-271">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="abb98-272">&#x2714; Q&A の改訂履歴を追跡します。</span><span class="sxs-lookup"><span data-stu-id="abb98-272">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="abb98-273">&#x2714; [アダプティブ カード](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)として表示する追加の詳細を含む回答を構成します。</span><span class="sxs-lookup"><span data-stu-id="abb98-273">&#x2714; Configure an answer with additional details to display as an [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="abb98-274">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ プラス GIF](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="abb98-276">サポート アプリを入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-276">Get Support App</span></span>

<span data-ttu-id="abb98-277">サポートの取得アプリは、Microsoft Teamsを使用している組織によって使用され、すべてのユーザーがスーパーバイザーに支援を要求できるようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-277">The Get Support app is used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="abb98-278">このアプリには、次の機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="abb98-278">This app includes the following features:</span></span>
* <span data-ttu-id="abb98-279">パワーアプリから異なるカテゴリに関する支援を要求します。</span><span class="sxs-lookup"><span data-stu-id="abb98-279">Requesting assistance on different categories from a Power App.</span></span>
* <span data-ttu-id="abb98-280">誰が割り当てられたか知らせる要求者に送信される通知。</span><span class="sxs-lookup"><span data-stu-id="abb98-280">Notifications sent to requestors informing them of who hare assigned.</span></span>
* <span data-ttu-id="abb98-281">割り当てられたスーパーバイザーに、誰が支援を必要とするか知らせる通知。</span><span class="sxs-lookup"><span data-stu-id="abb98-281">Notifications sent to assigned supervisors informing them of who needs assistance.</span></span> 
* <span data-ttu-id="abb98-282">SharePointと PowerBI.S のエスカレーションとパターンの分析</span><span class="sxs-lookup"><span data-stu-id="abb98-282">Analyzing escalations and patterns in SharePoint and PowerBI.S.</span></span>

[<span data-ttu-id="abb98-283">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-283">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![Get Support Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="abb98-285">Goal Tracker</span><span class="sxs-lookup"><span data-stu-id="abb98-285">Goal Tracker</span></span>

<span data-ttu-id="abb98-286">Goal Tracker アプリは、Microsoft Teams内で、組織の目標の設定、進捗状況の観察、成功の確認をサポートする包括的なソリューションです。</span><span class="sxs-lookup"><span data-stu-id="abb98-286">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="abb98-287">このアプリを使用すると、ユーザーは、専門家、個人、チーム レベルで目標を設定、追跡、更新できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-287">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="abb98-288">また、チーム メンバーは、集中力を維持し、順調に進めるために、タイムリーなリマインダーと状態の更新情報を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="abb98-288">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="abb98-289">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

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

## <a name="great-ideas"></a><span data-ttu-id="abb98-292">Great Ideas</span><span class="sxs-lookup"><span data-stu-id="abb98-292">Great Ideas</span></span>

<span data-ttu-id="abb98-293">Great Ideas アプリは、組織内のイノベーションと創造性をサポートし、力を与えます。</span><span class="sxs-lookup"><span data-stu-id="abb98-293">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="abb98-294">このアプリを使用すると、Microsoft Teams 内で、従業員は同僚やリーダーシップとアイデアを共有し、新しい報告を検索し、同僚の検討のために貢献にスポットライトを当て、最良の提案に投票することができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-294">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="abb98-295">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-295">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="abb98-298">グループ アクティビティ</span><span class="sxs-lookup"><span data-stu-id="abb98-298">Group Activities</span></span>

<span data-ttu-id="abb98-299">グループ アクティビティは、チームの所有者が Microsoft Teamsの コンテキスト内でアクティビティ グループをすばやく作成し、コラボレーション ワークフローを管理するのを容易にする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-299">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="abb98-300">アクティビティ作成者は、アクティビティを作成し、チーム メンバーをグループにランダムに配布し、オプションで、アクティビティが完了するまでボットにリマインダーを送信させることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-300">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="abb98-301">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-301">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

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

## <a name="group-connect-9734"></a><span data-ttu-id="abb98-304">グループConnect &#9734;</span><span class="sxs-lookup"><span data-stu-id="abb98-304">Group Connect &#9734;</span></span>

<span data-ttu-id="abb98-305">グループConnectは、組織のメンバーが従業員グループを見つけ、従業員グループに関連する情報を見つけるのに役立つMicrosoft Teamsアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-305">Group Connect is a Microsoft Teams app that helps organization members discover employee groups and find information relevant to employee groups.</span></span> <span data-ttu-id="abb98-306">このアプリには、組織のリーダーがグループ、イベント、リソースに関して従業員とコミュニケーションを取るための豊富な機能が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="abb98-306">The app comes built-in with rich capabilities for organization leaders to communicate with their employees regarding groups, events, and resources.</span></span> <span data-ttu-id="abb98-307">グループConnectアプリは、グループ内のネットワーキングと結束を促進するために、グループメンバー同士を希望する頻度でマッチングします。</span><span class="sxs-lookup"><span data-stu-id="abb98-307">The Group Connect app also matches group members with each other at their desired frequency to encourage networking and cohesion within a group.</span></span> <span data-ttu-id="abb98-308">グループ Connect アプリを活用して、組織内で従業員グループを育成する方法の詳細については、GitHubのアプリを参照してください。</span><span class="sxs-lookup"><span data-stu-id="abb98-308">For more information on how you can leverage the Group Connect app to help employee groups foster within your organization, see the app on GitHub.</span></span>

[<span data-ttu-id="abb98-309">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-309">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect)

![D&I グループを発見する](https://github.com/OfficeDev/microsoft-teams-apps-diversityandinclusion/wiki/Images/temp_group_connect_landing.png)

## <a name="grow-your-skills"></a><span data-ttu-id="abb98-311">Grow Your Skills</span><span class="sxs-lookup"><span data-stu-id="abb98-311">Grow Your Skills</span></span>

<span data-ttu-id="abb98-312">Grow Your Skills アプリは、従業員が組織の補助的なプロジェクトに貢献し、新しいスキルを同時に学習できるようにして、プロフェッショナルな成長と開発をサポートします。</span><span class="sxs-lookup"><span data-stu-id="abb98-312">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="abb98-313">すべての Teams 環境内で、従業員はこのアプリを使用して、自分の興味に合った機会を見つけ、同僚との有意義な共同作業を行い、新しいレベルの専門知識と能力を取得できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-313">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="abb98-314">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-314">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a><span data-ttu-id="abb98-317">HR サポート</span><span class="sxs-lookup"><span data-stu-id="abb98-317">HR Support</span></span>

<span data-ttu-id="abb98-318">HR サポート ボットは、サポート担当者やサポート担当者がサポートできない場合に、サポート担当者または専門家をループに入れて使用するボット&フレンドリーな Q です。</span><span class="sxs-lookup"><span data-stu-id="abb98-318">HR Support bot is a friendly Q&A bot that brings a support professional or expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="abb98-319">ボットに質問をすることができ、知識ベースに含まれている場合、ボットは回答を返します。</span><span class="sxs-lookup"><span data-stu-id="abb98-319">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="abb98-320">そうでない場合、ボットはユーザーがクエリを送信できるようにします。クエリは、チーム内からの通知に基づいて行動することでサポートを提供するのに役立つ、事前に構成された専門家チームに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-320">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="abb98-321">さらに、ボットは、質問に事前に設定されたタグを検索することで、推奨される HR ポリシーまたは質問へのリンクを提案します。</span><span class="sxs-lookup"><span data-stu-id="abb98-321">Additionally, the bot suggests links to recommended HR policies or questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="abb98-322">これらのタイルは、クイック リファレンスとして関連付けられたタブにあります。</span><span class="sxs-lookup"><span data-stu-id="abb98-322">These tiles are found in the associated tab as a quick reference.</span></span> <span data-ttu-id="abb98-323">HR サポートは、軽量 Q&A に適しており、組織で新しいプロジェクトやイニシアチブを立ち上げる際に迅速なサポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="abb98-323">HR Support works well for light weight Q&A and to provide quick support when launching new projects or initiatives in the organization.</span></span>

[<span data-ttu-id="abb98-324">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-324">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR サポート](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="abb98-326">アイスブレーカー</span><span class="sxs-lookup"><span data-stu-id="abb98-326">Icebreaker</span></span>

<span data-ttu-id="abb98-327">アイスブレーカーは、[Microsoft Teams ボット](../bots/what-are-bots.md)で、毎週 2 人のランダムなチーム メンバーをペアにして、チームを近づけることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-327">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="abb98-328">ボットは、両方のメンバーに有効な空き時間を自動的に提案することで、スケジュール設定を簡単にします。</span><span class="sxs-lookup"><span data-stu-id="abb98-328">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="abb98-329">このアプリで個人的なつながりを強化し、緊密に結びついたコミュニティを構築します。</span><span class="sxs-lookup"><span data-stu-id="abb98-329">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="abb98-330">アイスブレーカー アプリは、チーム全体で個人的なつながりを促進するだけでなく、組織内で関心に基づいたコミュニティを育成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="abb98-330">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="abb98-331">たとえば、このアプリを DevOps の共同作業グループに使用して、アイデアやベストプラクティスを組織全体に有機的に広めることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-331">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="abb98-332">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-332">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![アイスブレーカー アプリ](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="abb98-334">Incentives</span><span class="sxs-lookup"><span data-stu-id="abb98-334">Incentives</span></span>

<span data-ttu-id="abb98-335">インセンティブは、トレーニングや変更管理イニシアチブなど、指定された活動への従業員のインセンティブ付け参加を管理および追跡する[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="abb98-335">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities, such as trainings and change management initiatives.</span></span> <span data-ttu-id="abb98-336">管理者は、アプリを使用して、指定されたアクティビティを確立し、完了のためにポイントを割り当て、報酬に必要な適格ポイント レベルを指定します。</span><span class="sxs-lookup"><span data-stu-id="abb98-336">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="abb98-337">従業員は、アプリを使用して蓄積されたポイントを表示し、資格に達したら、償還可能な報酬を要求して請求します。</span><span class="sxs-lookup"><span data-stu-id="abb98-337">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="abb98-338">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-338">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![Incentives アプリのデモ](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="abb98-340">Incident Reporter</span><span class="sxs-lookup"><span data-stu-id="abb98-340">Incident Reporter</span></span>

<span data-ttu-id="abb98-341">Incident Reporter は、組織内のインシデントの管理を最適化する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-341">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="abb98-342">ボットは、自動化されたインシデント データ収集、カスタマイズされたインシデント レポート、関連する利害関係者への通知、エンドツーエンドのインシデント追跡を容易にします。</span><span class="sxs-lookup"><span data-stu-id="abb98-342">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="abb98-343">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-343">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection"></a><span data-ttu-id="abb98-346">特殊評価</span><span class="sxs-lookup"><span data-stu-id="abb98-346">Inspection</span></span> 

 <span data-ttu-id="abb98-347">Inspection は、現場の最前線にいる従業員が位置情報から資産、備品まで何でも検査できる Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-347">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="abb98-348">たとえば、小売店、製造工場、車両、または機械などがあります。</span><span class="sxs-lookup"><span data-stu-id="abb98-348">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="abb98-349">このソリューションには 2 つのアプリがあり、それぞれ異なるタイプのユーザーを対象としています。</span><span class="sxs-lookup"><span data-stu-id="abb98-349">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="abb98-350">このアプリは、第一線で働く人たちが資産や領域を検査したり、製品やサービスの品質を管理したり、職場の安全を維持したりすることができるようにするためのものです。</span><span class="sxs-lookup"><span data-stu-id="abb98-350">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="abb98-351">検査中に発見された問題に対処するために、チーム メンバー間のコミュニケーションを促進します。</span><span class="sxs-lookup"><span data-stu-id="abb98-351">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="abb98-352">このアプリでは管理者向けのシンプルなレポートを提供して、問題解決を迅速化し、傾向を強調します。</span><span class="sxs-lookup"><span data-stu-id="abb98-352">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="abb98-353">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![Inspection の概要](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="abb98-355">問題報告</span><span class="sxs-lookup"><span data-stu-id="abb98-355">Issue Reporting</span></span>

<span data-ttu-id="abb98-356">Issue Reporting アプリは、従業員や管理者が課題を提起し、管理するための権限を付与するためのものです。</span><span class="sxs-lookup"><span data-stu-id="abb98-356">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="abb98-357">これは、問題を報告するための「問題報告アプリ」と、問題を管理するための「問題管理アプリ」の 2 つのアプリで構成されています。</span><span class="sxs-lookup"><span data-stu-id="abb98-357">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="abb98-358">チーム管理者は、問題管理アプリを使用して、Microsoft Teams のメッセージやアプリで作成される Planner のタスク内のチャネルを含む、アプリのエクスペリエンスを構成します。</span><span class="sxs-lookup"><span data-stu-id="abb98-358">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="abb98-359">管理者は、このアプリを使用してテンプレート フォームを作成し、ユーザーが問題を報告した場合に詳細を収集します。</span><span class="sxs-lookup"><span data-stu-id="abb98-359">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="abb98-360">たとえば、問題テンプレート フォームのレビュー、編集、削除などがあります。</span><span class="sxs-lookup"><span data-stu-id="abb98-360">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="abb98-361">このアプリは、チームの問題のレビュー、問題の履歴のレポート、問題解決の効率的な管理にも使用されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-361">The app is also used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="abb98-362">従業員は、問題報告アプリを使用して、問題とその解決に必要な詳細を記録します。</span><span class="sxs-lookup"><span data-stu-id="abb98-362">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="abb98-363">このアプリは、既存の問題を修正して解決し、個人やチームの問題を大局的に俯瞰するためにも使用されています。</span><span class="sxs-lookup"><span data-stu-id="abb98-363">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="abb98-364">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![Issue Reporting チーム ビュー](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="abb98-366">New Employee Onboarding</span><span class="sxs-lookup"><span data-stu-id="abb98-366">New Employee Onboarding</span></span> 

<span data-ttu-id="abb98-367">New Employee Onboarding は、組織が新入社員教育で、従業員に一貫した高品質のオンボーディング エクスペリエンスを提供できるようにする Microsoft Teams と [SharePoint New Employee Onboarding が統合されたソリューション](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-367">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="abb98-368">このアプリは、人事チームと採用マネージャーが、オリエンテーションと誘導プロセスを通じて関連情報を提供するために使用され、新入社員はフィードバックを共有し、紹介を提供し、完全なオンボーディングタスクを行います。</span><span class="sxs-lookup"><span data-stu-id="abb98-368">The app is used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="abb98-369">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="abb98-370">**新入社員のウェルカム カード** ![新入社員のウェルカムカードの画像](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="abb98-370">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="abb98-371">**新入社員のチェックリスト** ![新入社員のチェックリストの画像](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="abb98-371">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="abb98-372">オープン バッジ</span><span class="sxs-lookup"><span data-stu-id="abb98-372">Open Badges</span></span>

<span data-ttu-id="abb98-373">オープン バッジは、個人が Teams コンテキスト内でデジタル学習資格情報バッジを取得して、どこでも共有できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-373">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="abb98-374">第三者デジタル バッジ発行機関である [Badgr](https://badgr.org/) の機能を使用して、授与されたバッジは受信者の Badgr プロファイルに記録され、生涯学習の豊富な画像を作成して共有するために利用できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-374">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="abb98-375">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a><span data-ttu-id="abb98-378">Poll</span><span class="sxs-lookup"><span data-stu-id="abb98-378">Poll</span></span> 

<span data-ttu-id="abb98-379">Poll は、チャットまたはチャネルで投票をすばやく作成して送信し、チームの意見や好みを収集できるようにする Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-379">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="abb98-380">アプリは、デスクトップ、ブラウザー、iOS、Android などのすべてのTeamsプラットフォームクライアントでサポートされ、Microsoft 365サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="abb98-380">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="abb98-381">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Teams ビューで投票を作成する](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="abb98-383">クイック応答</span><span class="sxs-lookup"><span data-stu-id="abb98-383">Quick Responses</span></span>

<span data-ttu-id="abb98-384">クイックレスポンスは、ユーザーのよくある質問に関するFAQに効果的に答える堅牢なソリューションを提供するMicrosoft Teamsアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-384">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions FAQs.</span></span> <span data-ttu-id="abb98-385">各クエリに手動で連続して繰り返し表示される情報に応答する代わりに、アプリは[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)を使用して対話型ユーザー エクスペリエンスの応答ライブラリTeams構築します。</span><span class="sxs-lookup"><span data-stu-id="abb98-385">Instead of answering each query manually and continuously repeating information, the app builds a library of responses for an interactive user experience through Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="abb98-386">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![応答のサンプル ビュー](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a><span data-ttu-id="abb98-388">クイズ&#9734;</span><span class="sxs-lookup"><span data-stu-id="abb98-388">Quiz  &#9734;</span></span>

<span data-ttu-id="abb98-389">クイズは、あなたが知識チェックと瞬時に結果のためのチャットやチャネル内のクイズを作成することを可能にするカスタム[Teamsメッセージング拡張](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-389">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="abb98-390">クイズは、クラス内試験とオフライン試験、チーム内の知識チェック、チーム内の楽しいクイズに使用できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-390">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="abb98-391">クイズ アプリは、デスクトップ、ブラウザー、iOS、Android クライアントなど、複数のプラットフォームでサポートTeams。</span><span class="sxs-lookup"><span data-stu-id="abb98-391">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="abb98-392">このアプリは、既存のMicrosoft 365サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="abb98-392">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="abb98-393">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![Teamsビューでクイズを作成](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="abb98-395">ラピッドアシスト</span><span class="sxs-lookup"><span data-stu-id="abb98-395">Rapid Assist</span></span>

<span data-ttu-id="abb98-396">Rapid Assist は、Microsof t[Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) ベースのアプリで、顧客対応担当者が専門家と素早く接続して迅速な回答を得たり、情報を検索したり、オープンな要求をフォローしたりして、専門家が通知を受信して素早く応答し、質問に答えるためのサポートを行います。</span><span class="sxs-lookup"><span data-stu-id="abb98-396">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="abb98-397">Microsoft [Power Apps](/powerapps/powerapps-overview) と [Power Automate](/power-automate/getting-started) を使用して構築されたアプリは、Microsoft Teams と深く統合されており、組織は現場の従業員と企業のリエゾンを簡単に接続して、顧客の問い合わせを解決し、優れた顧客エクスペリエンスを提供できるようにします。</span><span class="sxs-lookup"><span data-stu-id="abb98-397">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="abb98-398">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-398">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![エンド ユーザー要求インターフェイス](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![専門家要求ビュー](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="abb98-401">Reflect</span><span class="sxs-lookup"><span data-stu-id="abb98-401">Reflect</span></span> 

<span data-ttu-id="abb98-402">Reflect は、チーム メンバーが感情的な幸福の状態を同僚やグループ リーダーと直接Teams内で共有するための安全で包括的なリソースを提供するカスタム Microsoft Teams[メッセージング拡張](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-402">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues or group leaders directly within Teams.</span></span> <span data-ttu-id="abb98-403">アプリは、チャネル、グループ、会議、および 1:1 のチャットで利用でき、チェックイン応答はパブリック、プライベートから送信者、または完全に匿名に設定されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-403">The app is available in channel, group, meeting, and 1:1 chats and the check-in response is set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="abb98-404">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-404">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="abb98-405">**ウェルビーイング投票**</span><span class="sxs-lookup"><span data-stu-id="abb98-405">**Well-being poll**</span></span>
    
    ![Reflect アプリのユーザー投票](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="abb98-407">リモート サポート</span><span class="sxs-lookup"><span data-stu-id="abb98-407">Remote Support</span></span>

<span data-ttu-id="abb98-408">リモート サポートは、組織全体のサポート要求者と内部サポート チームの間に焦点を絞ったインターフェイスを提供する [Microsoft Teams ボット](../bots/what-are-bots.md)です。</span><span class="sxs-lookup"><span data-stu-id="abb98-408">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="abb98-409">エンド ユーザーは、サポートの要求を送信、編集、取り消すことができ、サポート チームはすべての Teams プラットフォーム内で要求に応答、管理、更新できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-409">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="abb98-410">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-410">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a><span data-ttu-id="abb98-413">Request-a-team</span><span class="sxs-lookup"><span data-stu-id="abb98-413">Request-a-team</span></span>

<span data-ttu-id="abb98-414">Request-a-team は、企業組織の新しいチーム作成を最適化する Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-414">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="abb98-415">このアプリは、ウィザードでガイドされたリクエスト フォーム、組み込み承認プロセス、要求状態ダッシュボード、自動化されたチーム ビルドの統合を通じて、新しいチーム インスタンスを作成する際の標準化とベスト プラクティスをサポートします。</span><span class="sxs-lookup"><span data-stu-id="abb98-415">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="abb98-416">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-416">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a><span data-ttu-id="abb98-419">Scrums for Channels</span><span class="sxs-lookup"><span data-stu-id="abb98-419">Scrums for Channels</span></span>

<span data-ttu-id="abb98-420">Scrums for Channels は、ユーザーが Microsoft Teams 内のチャネルでスクラムをスケジュールして実行できるようにするスクラム アシスタント アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-420">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="abb98-421">このアプリは、リモート チームや、地理的に異なる場所やタイムゾーンのメンバーで構成されるチームが毎日の更新情報を共有し、スクラム スタンドアップ ミーティングに確実に参加できるようにするのに最適です。</span><span class="sxs-lookup"><span data-stu-id="abb98-421">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="abb98-422">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-422">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="abb98-423">グループ チャットでスクラム会議を実施するには、「グループ チャット アプリ テンプレート [のスクラム](#scrums-for-group-chat) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="abb98-423">To conduct scrum meetings in a group chat, see [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

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

## <a name="scrums-for-group-chat"></a><span data-ttu-id="abb98-426">Scrums for Group Chat</span><span class="sxs-lookup"><span data-stu-id="abb98-426">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="abb98-427">スクラムステータスアプリテンプレートが更新され、グループチャットのスクラムになりました。</span><span class="sxs-lookup"><span data-stu-id="abb98-427">The Scrums Status app template is updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="abb98-428">Scrums for Group Chat は、グループ チャットのメンバーが非同期スタンドアップ ミーティングを実行し、毎日の更新情報を簡単に共有できるようにする、サポート的なスクラム アシスタントです。</span><span class="sxs-lookup"><span data-stu-id="abb98-428">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="abb98-429">これにより、グループ チャットのすべてのメンバーがスクラムに貢献し、実行中のスクラムで他のメンバーが行った更新情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-429">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="abb98-430">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-430">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![Scrums for Group Chat のデモ](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="abb98-432">Share Now</span><span class="sxs-lookup"><span data-stu-id="abb98-432">Share Now</span></span> 

<span data-ttu-id="abb98-433">Share Now アプリは、ユーザーがチーム環境内でコンテンツを簡単に共有できるようにすることで、同僚間の積極的な情報交換を促進します。</span><span class="sxs-lookup"><span data-stu-id="abb98-433">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="abb98-434">ユーザーはアプリを使用して、関心のあるアイテムをチーム メンバーと共有し、新しい共有コンテンツを見つけ、環境設定を設定し、後で読むためにお気に入りをブックマークします。</span><span class="sxs-lookup"><span data-stu-id="abb98-434">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="abb98-435">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-435">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![コンテンツの選択ビュー](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="abb98-437">SharePoint リスト検索</span><span class="sxs-lookup"><span data-stu-id="abb98-437">SharePoint List Search</span></span>

<span data-ttu-id="abb98-438">Microsoft Teams でのコラボレーションでは、SharePoint リストのアイテム内に含まれる情報を参照することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="abb98-438">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="abb98-439">質問のアイテムへのリンクを貼り付けると、すべてのユーザーが会話からコンテキストを切り替え、必要な情報を見つけ、Teamsに戻って会話を続けます。</span><span class="sxs-lookup"><span data-stu-id="abb98-439">Paste a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="abb98-440">会話が続くにつれて、ユーザーは参照アイテムに何度も切り替えて新しいコメントを確認し、アイテムに含まれる情報の記憶を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="abb98-440">As the conversation continues  people have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="abb98-441">このコンテキスト切り替えは、円滑なコラボレーションの障壁となります。</span><span class="sxs-lookup"><span data-stu-id="abb98-441">This context switching creates a barrier to smooth collaboration.</span></span>
<span data-ttu-id="abb98-442">この問題を解決するには、リスト検索アプリ テンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="abb98-442">To resolve this problem, the List Search app template is used.</span></span> <span data-ttu-id="abb98-443">多くのユーザーは、SharePointを使用して、組織内の主要なワークフローの一部に電力を供給しています。</span><span class="sxs-lookup"><span data-stu-id="abb98-443">Many users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="abb98-444">ただし、リストの周りの共同作業は困難です。</span><span class="sxs-lookup"><span data-stu-id="abb98-444">However, collaborating around lists is difficult.</span></span> <span data-ttu-id="abb98-445">Microsoft Teams のリスト検索アプリ テンプレートを使用すると、ユーザーは SharePoint リスト アイテムの情報をチャットの会話内に直接挿入して、チャットにリンクを挿入するだけで発生するコンテキストの切り替えを軽減できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-445">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="abb98-446">この情報は読みやすい自動フォーマットカードとして挿入され、ユーザーが会話に従事し続けるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="abb98-446">The information is inserted as an easy-to-read auto-formatted card, helping the users stay engaged in the conversation.</span></span>

[<span data-ttu-id="abb98-447">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-447">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![リスト検索アプリ](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="abb98-449">Staff Check-ins</span><span class="sxs-lookup"><span data-stu-id="abb98-449">Staff Check-ins</span></span>

<span data-ttu-id="abb98-450">スタッフチェックインは、あなたのビジネスとフィールドの担当者間の監督通信を可能にする[Power Apps](/powerapps/powerapps-overview)ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-450">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview) based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="abb98-451">スタッフは、タイムクリティカルな情報とステータスの更新情報を、スケジュール ベースまたはアドホック ベースで、Teams から直接簡単に提供できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-451">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="abb98-452">アプリは、リアルタイムの場所、写真、メモ、リマインダー通知、および自動化されたワークフローをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="abb98-452">The app supports real-time location, photos, notes, reminder notifications, and automated workflows.</span></span>

[<span data-ttu-id="abb98-453">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-453">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![チェックインの作成ビュー](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="abb98-455">Survey</span><span class="sxs-lookup"><span data-stu-id="abb98-455">Survey</span></span>

<span data-ttu-id="abb98-456">Survey は、チャットまたはチャネルで調査を作成してデータを収集し、実用的な洞察を得ることができる Microsoft Teams のカスタム [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-456">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span> <span data-ttu-id="abb98-457">アプリは、デスクトップ、ブラウザー、iOS、Android などのすべてのTeamsプラットフォームクライアントでサポートされ、Microsoft 365サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="abb98-457">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="abb98-458">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-458">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Teams ビューでアンケートを作成する](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="abb98-460">タイムタリー</span><span class="sxs-lookup"><span data-stu-id="abb98-460">Time Tally</span></span> 

<span data-ttu-id="abb98-461">プロジェクトには複数のタスクを含めることができ、さまざまなプロジェクトを従業員に割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-461">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="abb98-462">マネージャは、これらのタスクに費やした時間を通じてプロジェクトの進捗状況を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="abb98-462">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="abb98-463">これは、従業員がタイムシートを記入する必要があるため、面倒な活動になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="abb98-463">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="abb98-464">Time Tally アプリを使用すると、従業員はモバイル デバイスを使用してタイムシートをすばやく入力でき、管理者はタイムシート エントリで従業員をフォローアップする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="abb98-464">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="abb98-465">マネージャは、リソースに基づいてプロジェクトの稼働率を表示し、エントリを承認または却下できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-465">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="abb98-466">タイムシートのコンプライアンスを確保するために、事前通知が送信されます。</span><span class="sxs-lookup"><span data-stu-id="abb98-466">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="abb98-467">また、履歴データと使用状況を分析に使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="abb98-467">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="abb98-468">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-468">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![タイムタリー](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a><span data-ttu-id="abb98-470">トレーニング&#9734;</span><span class="sxs-lookup"><span data-stu-id="abb98-470">Training  &#9734;</span></span>

<span data-ttu-id="abb98-471">トレーニングは、ユーザーがオフラインの知識共有とアップスキルのためのチャットまたはチャネル内のトレーニングを公開することを可能にするカスタムTeams[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)アプリです。</span><span class="sxs-lookup"><span data-stu-id="abb98-471">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="abb98-472">アプリは、デスクトップ、ブラウザー、iOS、Android などの複数のTeamsプラットフォーム クライアントでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="abb98-472">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="abb98-473">このアプリは、Microsoft 365サブスクリプションの一部として展開する準備ができています。</span><span class="sxs-lookup"><span data-stu-id="abb98-473">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="abb98-474">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-474">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Teams ビューでトレーニングを作成する](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="abb98-476">Virtual Rounding</span><span class="sxs-lookup"><span data-stu-id="abb98-476">Virtual Rounding</span></span>

<span data-ttu-id="abb98-477">病院や救急外来の提供者は、1日に多くの **ラウンド** を行います。</span><span class="sxs-lookup"><span data-stu-id="abb98-477">Hospital and emergency room providers make many **rounds** per day.</span></span> <span data-ttu-id="abb98-478">患者に対するこれらの迅速なチェックは、患者がどのように行動しているかの状態チェックを行い、患者の懸念に確実な対処を行うことを目的としています。</span><span class="sxs-lookup"><span data-stu-id="abb98-478">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="abb98-479">丸めは、患者が複数のタイプのプロバイダーによって監視されていることを確認するための不可欠な慣行ですが、訪問ごとに、各プロバイダから、新しいマスク、および新しい手袋のセットが使用されるため、PPEの巨大な排水管を表します。</span><span class="sxs-lookup"><span data-stu-id="abb98-479">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves are used.</span></span> <span data-ttu-id="abb98-480">このアプリのテンプレートを使用すると、医療従事者は、プロバイダーと患者の間で Microsoft Teams の会議を介して、仮想的に簡単な回診を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-480">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="abb98-481">Virtual Rounding のソリューションは、Microsoft Health とライフ サイエンスの[ブログ記事](https://aka.ms/teamsvirtualrounding)でも参照できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-481">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="abb98-482">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-482">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![Virtual Rounding](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="abb98-484">Visitor Management</span><span class="sxs-lookup"><span data-stu-id="abb98-484">Visitor Management</span></span>

<span data-ttu-id="abb98-485">Visitor Management アプリを使用すると、組織と従業員は、Microsoft Teams から直接、オンサイトの訪問者プロセスを簡単かつ効率的に管理できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-485">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="abb98-486">このアプリを使用すると、従業員は訪問者の要求を作成し、訪問者のダッシュボードを介して要求状態を一元的に追跡し、訪問者が到着したときにリアルタイムの通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="abb98-486">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="abb98-487">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-487">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="abb98-490">Workplace Awards</span><span class="sxs-lookup"><span data-stu-id="abb98-490">Workplace Awards</span></span>

<span data-ttu-id="abb98-491">Workplace Awards は、現代の職場での認識を促進し、従業員の感謝の文化を促進するための前向きなフレームワークを提供する Teams アプリ テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="abb98-491">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="abb98-492">このアプリでは、R&R プログラムと呼ばれる従業員の報酬と認識を設定および管理することができ、従業員は同僚を簡単に指名して支持し、R&R リーダーは、提出されたノミネートを表示し、賞を付与し、受信者を発表できます。</span><span class="sxs-lookup"><span data-stu-id="abb98-492">The app enables you to setup and manage an employee rewards and recognition, called R&R program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="abb98-493">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="abb98-493">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="abb98-494">Workplace Awards の推薦カード</span><span class="sxs-lookup"><span data-stu-id="abb98-494">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Workplace Awards のリスト タブ](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="abb98-496">アプリ テンプレートの詳細については、「 [アプリ テンプレート](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="abb98-496">For more information on app template, see [App template](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>

## <a name="see-also"></a><span data-ttu-id="abb98-497">関連項目</span><span class="sxs-lookup"><span data-stu-id="abb98-497">See also</span></span>

[<span data-ttu-id="abb98-498">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="abb98-498">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
