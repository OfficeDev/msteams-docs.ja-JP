---
title: Microsoft Teams アプリテンプレート
description: Microsoft Teams プラットフォームのアプリテンプレートのリンクと説明
ms.topic: reference
keywords: Microsoft Teams テンプレートサンプルのデモ
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 87361e8c6be068b932400d97379db8f182afd499
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552578"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="d2359-104">Microsoft Teams のアプリテンプレート</span><span class="sxs-lookup"><span data-stu-id="d2359-104">App Templates for Microsoft Teams</span></span>

<span data-ttu-id="d2359-105">アプリテンプレートとは、コミュニティ主導で、オープンソースで、GitHub 上で利用可能な Microsoft Teams 用のプロダクション対応アプリのことです。</span><span class="sxs-lookup"><span data-stu-id="d2359-105">App templates are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="d2359-106">それぞれに、組織のためにアプリを展開してインストールするための詳細な手順が記載されており、すぐにインストールして使用を開始できるアプリを用意しています。</span><span class="sxs-lookup"><span data-stu-id="d2359-106">Each contains detailed instructions for deploying and installing that app for your organization, providing a ready-to-use app that you can install and begin using immediately.</span></span> <span data-ttu-id="d2359-107">完全なソースコードも利用できます。そのため、詳細について確認したり、コードをフォークして、特定のニーズを満たすように変更したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-107">The complete source code is available as well, so you can explore it in detail, or fork the code and alter it to meet your specific needs.</span></span>

<span data-ttu-id="d2359-108">**&#9734; は、新しくリリースされたアプリテンプレートを示しています。**</span><span class="sxs-lookup"><span data-stu-id="d2359-108">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="d2359-109">主な利点</span><span class="sxs-lookup"><span data-stu-id="d2359-109">Key benefits</span></span>

* <span data-ttu-id="d2359-110">**プラグアンドプレイの操作:** すべてのアプリテンプレートには、Microsoft Azure で必要なすべてのサービスをホストできる展開スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d2359-110">**Plug and play experience:** All app templates include deployments scripts that will allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="d2359-111">アプリを展開するためのコーディングは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="d2359-111">No coding is required to deploy the apps.</span></span>
* <span data-ttu-id="d2359-112">**運用可能なコード:** アプリテンプレートは、セキュリティとインフラストラクチャの推奨されるベストプラクティスに準拠しており、それらに加えられたすべてのコミュニティの変更をレビューして、引き続き準拠していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d2359-112">**Production-ready code:** The app templates conform to recommended best practices around security and infrastructure, and all community submitted changes to them are reviewed to ensure continued conformance.</span></span>
* <span data-ttu-id="d2359-113">**カスタマイズと拡張:** すべてのアプリテンプレートを展開する準備ができましたが、コードベースと展開スクリプト全体が提供されるので、独自のニーズに合わせてカスタマイズまたは拡張することが容易になります。</span><span class="sxs-lookup"><span data-stu-id="d2359-113">**Customizable and extensible:** While all app templates are ready to deploy as they are, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="d2359-114">**サポート & 詳細なドキュメント:** すべてのアプリテンプレートには、ソリューションのアーキテクチャ、展開、および構成手順に関するエンドツーエンドのドキュメントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="d2359-114">**Detailed documentation & support:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="d2359-115">リポジトリも監視されるので、GitHub で問題を発生させることで、発生した問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="d2359-115">The repositories are monitored as well, so please report any issues you encounter by raising an Issue on GitHub.</span></span>

## <a name="ask-away-9734"></a><span data-ttu-id="d2359-116">他の &#9734; を確認する</span><span class="sxs-lookup"><span data-stu-id="d2359-116">Ask Away &#9734;</span></span>

<span data-ttu-id="d2359-117">この質問は、ユーザーが Teams 内で Q&A (質問と回答) セッションを実施できるようにする [Microsoft Teams の bot](../bots/what-are-bots.md) です。</span><span class="sxs-lookup"><span data-stu-id="d2359-117">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="d2359-118">不在時のボットを使用すると、チームメンバーは仕事仲間によって共有されている質問を提出したり、&して、ホストが、チャネルまたはチャット内の重要な質問を簡単に収集できるようになります。</span><span class="sxs-lookup"><span data-stu-id="d2359-118">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="d2359-119">この bot を使用して、Teams 会議のセッションをリアルタイムで Q&し、参加者がチャットで実際に質問を送信できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-119">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="d2359-120">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-120">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![ユーザーが質問に投票できるようにするためのスコアボードポップアップダイアログの表示](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="d2359-122">アソシエイト インサイト</span><span class="sxs-lookup"><span data-stu-id="d2359-122">Associate Insights</span></span>

<span data-ttu-id="d2359-123">アソシエイト Insights は、顧客の意見、心理、認識を直接取得して送信するための、第一線ワーカーを支援する [パワーアプリ](/powerapps/maker/canvas-apps/embed-teams-app) テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="d2359-123">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="d2359-124">Firstline ワーカーは、多くの場合、一対一の取引先担当者として顧客と協力することになります。</span><span class="sxs-lookup"><span data-stu-id="d2359-124">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="d2359-125">収集されたデータは、ビジネスチーム (たとえば、Power BI Teams タブを介して) によって共有および使用して、製品の改善や顧客のエクスペリエンスの向上に利用できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-125">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="d2359-126">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-126">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![アプリケーションによって生成された分析情報のフィードバックビュー](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![App が生成した application insights の Power BI ビュー](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="d2359-129">出席</span><span class="sxs-lookup"><span data-stu-id="d2359-129">Attendance</span></span>

<span data-ttu-id="d2359-130">出席アプリは、チーム内でピン留めできる [ [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) ] タブです。</span><span class="sxs-lookup"><span data-stu-id="d2359-130">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="d2359-131">これは、通常、学習およびトレーニング環境などの設定で、プレゼンスを記録するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="d2359-131">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="d2359-132">ユーザーは、過去30日間の参加をマークまたは編集したり、グループ全体または個々の出席者のレポートをまとめて表示したりできます。</span><span class="sxs-lookup"><span data-stu-id="d2359-132">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="d2359-133">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-133">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![出勤アプリデモ](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="d2359-135">書籍-a ルーム</span><span class="sxs-lookup"><span data-stu-id="d2359-135">Book-a-room</span></span>

<span data-ttu-id="d2359-136">書籍-a room は [Microsoft Teams の bot](../bots/what-are-bots.md) で、現在の時刻から 30 (既定)、60、または90分間、ユーザーが会議室をすばやく検索して予約することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-136">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="d2359-137">個人または1:1 の会話に対して、会議中の bot の範囲を示します。</span><span class="sxs-lookup"><span data-stu-id="d2359-137">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="d2359-138">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![書籍-a ルームのデモ](../assets/images/book-a-room.png)

## <a name="building-access-9734"></a><span data-ttu-id="d2359-140">Access &#9734; を作成する</span><span class="sxs-lookup"><span data-stu-id="d2359-140">Building Access &#9734;</span></span>

<span data-ttu-id="d2359-141">Access の作成は、施設ディレクターが従業員のオンサイトプレゼンスを管理、追跡、および報告することにより、占有しきい値と社会的 distancing 基準を構築するための管理をサポートする Microsoft の [電源プラットフォーム](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-141">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="d2359-142">Microsoft [Power Apps](/powerapps/powerapps-overview)を使用して構築されたアプリ、および [強力な機能](/power-automate/getting-started)を備えた microsoft Teams との緊密な統合により、組織は、建物の準備状況を判断し、オンサイトアクセスのための資格情報を設定して、今後の計画のために洞察を集めることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-142">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="d2359-143">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![アクセス予約カードの作成](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![アクセスキービューを作成する](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="d2359-146">お祝い</span><span class="sxs-lookup"><span data-stu-id="d2359-146">Celebrations</span></span>

<span data-ttu-id="d2359-147">[記念] は Teams アプリであり、チームメンバーは、他の誕生日、記念日、その他の定期的なイベントを担当することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-147">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="d2359-148">すべてのチームメンバーの特別な状況を記録して、イベントの作成時に選択されたすべてのチームでフレンドリメッセージを送信し、チームメンバーが自分の一日に特別な印象を感じられるようにします。</span><span class="sxs-lookup"><span data-stu-id="d2359-148">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="d2359-149">アプリは、すべてのチームメンバーが自分のイベントを個人的に追加および表示し、ユーザーがイベントを共有するチームを選択できるようにするための簡単なインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="d2359-149">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="d2359-150">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-150">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist-9734"></a><span data-ttu-id="d2359-151">チェックリスト &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-151">Checklist &#9734;</span></span>

<span data-ttu-id="d2359-152">チェックリストは、チャットまたはチャネルで共有チェックリストを作成することで、チームと共同作業を行えるようにするカスタム Microsoft Teams [メッセージング拡張](../messaging-extensions/what-are-messaging-extensions.md) アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-152">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="d2359-153">このアプリは、すべての Teams プラットフォームクライアント (デスクトップ、ブラウザー、iOS、および Android) でサポートされており、Microsoft 365 サブスクリプションの一部として展開の準備ができています。</span><span class="sxs-lookup"><span data-stu-id="d2359-153">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="d2359-154">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-154">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![Teams ビューでチェックリストを作成する](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="company-communicator"></a><span data-ttu-id="d2359-156">社内コミュニケーター</span><span class="sxs-lookup"><span data-stu-id="d2359-156">Company Communicator</span></span>

<span data-ttu-id="d2359-157">会社の Communicator アプリを使用すると、企業チームはチャットを介して複数のチームまたは多数の従業員宛てのメッセージを作成して送信することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-157">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="d2359-158">このテンプレートを、新しいイニシアチブのアナウンス、従業員のオンボード、モダンラーニング、開発、組織全体のブロードキャストなど、複数のシナリオで利用できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-158">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="d2359-159">アプリは、指定されたユーザーがメッセージを作成、プレビュー、共同作業、および送信するための簡単なインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="d2359-159">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="d2359-160">これにより、メッセージを確認したり操作したりしたユーザー数について、カスタムテレメトリなどのカスタムの対象化通信機能を構築するための基盤が提供されます。</span><span class="sxs-lookup"><span data-stu-id="d2359-160">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="d2359-161">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator 新規作成ボックスビュー](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup-9734"></a><span data-ttu-id="d2359-163">連絡先グループ参照 &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-163">Contact Group Lookup &#9734;</span></span>

<span data-ttu-id="d2359-164">連絡先グループの参照アプリは、組織の連絡先グループ (以前の配布リストまたは通信グループ) を作成、アクセス、および管理するための便利で便利な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="d2359-164">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="d2359-165">ユーザーは、グループメンバーの表示とチャット、メンバーの状態の表示、連絡先グループ内の選択されたメンバーとのグループチャットの作成をすばやく行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-165">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="d2359-166">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-166">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![連絡先グループ参照のピン留めされたお気に入りの表示](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![連絡先グループ参照の開始チャットのデモ](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="crowdsourcer"></a><span data-ttu-id="d2359-169">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="d2359-169">CrowdSourcer</span></span>

<span data-ttu-id="d2359-170">CrowdSourcer は、チームが照会した情報をグループメンバーから共同で提供する [Microsoft teams bot](../bots/what-are-bots.md) です。</span><span class="sxs-lookup"><span data-stu-id="d2359-170">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="d2359-171">これは、よく寄せられる質問に回答するための最適な方法であり、参加者が積極的に協力して、楽しくて役に立つ情報リソースに投稿することを可能にします。</span><span class="sxs-lookup"><span data-stu-id="d2359-171">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="d2359-172">Github で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-172">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Crowdsource エンドユーザーの操作](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="d2359-174">カスタム ステッカー</span><span class="sxs-lookup"><span data-stu-id="d2359-174">Custom Stickers</span></span>

<span data-ttu-id="d2359-175">自己表現は、正常なチームのカルチャにとって中心的なものです。</span><span class="sxs-lookup"><span data-stu-id="d2359-175">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="d2359-176">このアプリテンプレートは、ユーザーが Microsoft Teams 内でカスタムステッカーと Gif を使用できるようにする [メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md) です。</span><span class="sxs-lookup"><span data-stu-id="d2359-176">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="d2359-177">このテンプレートを使用すると、web ベースの構成を簡単に行うことができます。これにより、エンドユーザーが使用する Gif/ステッカー/画像を構成アクセス権を持つすべてのユーザーがアップロードできるようになります。</span><span class="sxs-lookup"><span data-stu-id="d2359-177">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="d2359-178">このアプリでは、ストレージと共有のメカニズムとして、SharePoint サイトや個々のチャネルへのアクセスを必要とせずに、teams 間で画像、Gif、ステッカーを簡単に共有することもできます。</span><span class="sxs-lookup"><span data-stu-id="d2359-178">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="d2359-179">たとえば、製品チームは、プログラムを使用して、製品の画像や Gif をソーシャルメディア、マーケティング、営業チームに簡単に共有できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-179">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="d2359-180">新しい画像/Gif が利用可能になったときに、特定の teams/個人に通知フローをトリガーすることによって、このアプリを拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="d2359-180">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="d2359-181">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-181">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![ステッカーアプリ](../assets/images/stickers.png)

## <a name="e-prescriptions-9734"></a><span data-ttu-id="d2359-183">電子処方箋 &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-183">E-Prescriptions &#9734;</span></span> 

<span data-ttu-id="d2359-184">電子処方箋は、電子処方箋を患者に発行するプロセスを自動化することによって、telemedicine と仮想の治療を強化する [パワーアプリ](/powerapps/maker/canvas-apps/embed-teams-app)ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-184">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="d2359-185">医療担当者は、予定をすばやくレビューし、電子処方箋を生成し、電子処方箋に添付された電子メールを Teams プラットフォーム内で直接患者に送信することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-185">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="d2359-186">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-186">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![電子処方箋アプリのスクリーンショット。](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![電子処方箋アプリのスクリーンショット。](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training-9734"></a><span data-ttu-id="d2359-191">従業員トレーニング &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-191">Employee Training &#9734;</span></span>

<span data-ttu-id="d2359-192">従業員トレーニングは、開催者が組織のために学習およびトレーニングイベントを簡単に発行、追跡、促進できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-192">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="d2359-193">アプリを使用すると、イベントプランナーはイベント登録者に通知と通知を送信でき、従業員は、今後のイベントに関する関心を示し、現在のイベントに関する更新を続行し、Teams メッセージング拡張機能を使用してイベントの詳細を同僚と共有できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-193">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="d2359-194">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-194">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="d2359-195">**従業員のトレーニングイベント** ![ を表示する[従業員トレーニング] タブの画像](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="d2359-195">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="d2359-196">**従業員のトレーニングイベント** ![ を作成する従業員トレーニング作成イベントフォーム](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="d2359-196">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="d2359-197">エキスパート検索</span><span class="sxs-lookup"><span data-stu-id="d2359-197">Expert Finder</span></span>

<span data-ttu-id="d2359-198">専門家の Finder は、スキル、関心事、教育の属性に基づいて特定の組織のメンバーを識別する [Microsoft Teams の bot](../bots/what-are-bots.md) です。</span><span class="sxs-lookup"><span data-stu-id="d2359-198">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="d2359-199">メンバーは、Azure Active Directory ユーザープロファイルのキーワード検索に一致する組織内の専門家を検索します。</span><span class="sxs-lookup"><span data-stu-id="d2359-199">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="d2359-200">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-200">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![エキスパートファインダー検索結果のデモ](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="d2359-202">FAQ プラス</span><span class="sxs-lookup"><span data-stu-id="d2359-202">FAQ Plus</span></span>

<span data-ttu-id="d2359-203">話し言葉 Q&ボットは、ユーザーからよく寄せられる質問に対する回答を簡単に提供する方法です。</span><span class="sxs-lookup"><span data-stu-id="d2359-203">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="d2359-204">ただし、bot が失敗したときにループに人間が存在しないため、ほとんどのボットはユーザーとの通信に失敗することがあります。</span><span class="sxs-lookup"><span data-stu-id="d2359-204">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="d2359-205">FAQ bot は、問題が解決できないときにループを処理する bot&ボットです。</span><span class="sxs-lookup"><span data-stu-id="d2359-205">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="d2359-206">この場合は、bot がサポート技術情報に含まれている場合、ボットに質問をして応答を求めることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-206">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="d2359-207">できない場合は、ユーザーはクエリを送信することができます。これにより、チーム内から通知を受け取ることによってサポートを提供できる専門家チームに投稿されます。</span><span class="sxs-lookup"><span data-stu-id="d2359-207">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="d2359-208">**FAQ** の最新リリースでは、専門家のチームが次のことを実行できるようにすることで、改善された質疑&サポートしています。</span><span class="sxs-lookup"><span data-stu-id="d2359-208">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="d2359-209">&#x2714; メッセージ拡張機能を使用して、新しい Q&をナレッジベースに直接追加します。</span><span class="sxs-lookup"><span data-stu-id="d2359-209">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="d2359-210">&#x2714; を編集および削除するには、bot によって追加されたペア&Q を追加します。</span><span class="sxs-lookup"><span data-stu-id="d2359-210">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="d2359-211">&#x2714; Q&のリビジョン履歴を追跡します。</span><span class="sxs-lookup"><span data-stu-id="d2359-211">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="d2359-212">&#x2714; [アダプティブカード](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)として表示するには、追加の詳細を含む回答を構成します。</span><span class="sxs-lookup"><span data-stu-id="d2359-212">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="d2359-213">**GitHub で取得する**</span><span class="sxs-lookup"><span data-stu-id="d2359-213">**Get it on GitHub**</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ プラス GIF](../assets/images/FAQPlusEndUser.gif)

## <a name="goal-tracker"></a><span data-ttu-id="d2359-215">目標追跡ツール</span><span class="sxs-lookup"><span data-stu-id="d2359-215">Goal Tracker</span></span>

<span data-ttu-id="d2359-216">目標追跡アプリは、組織にとって、Microsoft Teams 内での目標の確立、進捗状況の確認、成功の確認をサポートするための包括的なソリューションです。</span><span class="sxs-lookup"><span data-stu-id="d2359-216">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="d2359-217">アプリを使用すると、ユーザーは professional、personal、および team の各レベルで目標を設定、追跡、更新することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-217">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="d2359-218">チームメンバーは、タイムリーな事前通知や進捗状況の更新を受信して、常に順調に進めることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-218">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="d2359-219">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-219">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![目標を設定する](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![設定目標を表示する](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="d2359-222">魅力的なアイデア</span><span class="sxs-lookup"><span data-stu-id="d2359-222">Great Ideas</span></span>

<span data-ttu-id="d2359-223">魅力的なアイデアアプリは、組織内の革新と創造性をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d2359-223">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="d2359-224">アプリを使用すると、従業員は仕事仲間やリーダーシップを使用してアイデアを共有し、新しい提出物、ピアに関するスポットライトを見つけ、Microsoft Teams 内でのベスト提案に投票を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-224">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="d2359-225">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-225">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![提出されたアイデアの表示](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![アイデアを表示する](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a><span data-ttu-id="d2359-228">グループアクティビティ</span><span class="sxs-lookup"><span data-stu-id="d2359-228">Group Activities</span></span>

<span data-ttu-id="d2359-229">グループアクティビティは、チームの所有者が簡単にアクティビティグループを作成し、Microsoft Teams のコンテキスト内でコラボレーションワークフローを管理できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-229">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="d2359-230">アクティビティの作成者はアクティビティの作成を有効にし、チームメンバーをランダムにグループに展開し、必要に応じて、アクティビティが完了するまで、必要に応じて bot に通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="d2359-230">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="d2359-231">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-231">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Teams でのグループ活動のリスト](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![チャネル内のグループアクティビティ通知メッセージ](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="d2359-234">スキルを拡張する</span><span class="sxs-lookup"><span data-stu-id="d2359-234">Grow Your Skills</span></span>

<span data-ttu-id="d2359-235">It アプリの拡張は、従業員が新しいスキルを同時に習得しながら、従業員が組織の補助的なプロジェクトに貢献できるようにすることで、プロフェッショナルな成長と開発をサポートします。</span><span class="sxs-lookup"><span data-stu-id="d2359-235">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="d2359-236">従業員は、アプリを使用して、関心のある機会を見つけ、仲間との有意義なコラボレーションを楽しんで、新しいレベルの専門知識と機能を Teams 環境内で取得することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-236">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="d2359-237">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-237">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![利用可能なプロジェクトビュー](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![閲覧者が取得したスキルビュー](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="d2359-240">HR サポート</span><span class="sxs-lookup"><span data-stu-id="d2359-240">HR Support</span></span>

<span data-ttu-id="d2359-241">HR サポート bot は、問題が解決できないときに、そのループの人事チームのサポートプロフェッショナル/専門家を支援する bot&のフレンドリな質問です。</span><span class="sxs-lookup"><span data-stu-id="d2359-241">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="d2359-242">この場合は、bot がサポート技術情報に含まれている場合、ボットに質問をして応答を求めることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-242">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="d2359-243">できない場合は、ユーザーはクエリを送信して、チーム内から通知を受け取ることによってサポートを提供できる専門家の事前に構成されたチームに投稿することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-243">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="d2359-244">また、bot は、質問で事前に構成されたタグを検索することにより、推奨される人事ポリシー/質問へのリンクを提案します。</span><span class="sxs-lookup"><span data-stu-id="d2359-244">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="d2359-245">これらのタイルは、クイックリファレンスとして、関連付けられたタブにもあります。</span><span class="sxs-lookup"><span data-stu-id="d2359-245">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="d2359-246">人事サポートは、軽いウエイト QnA に適しており、組織内で新しいプロジェクト/イニシアチブを開始する際の迅速なサポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="d2359-246">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="d2359-247">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR サポート](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="d2359-249">アイスブレーカー</span><span class="sxs-lookup"><span data-stu-id="d2359-249">Icebreaker</span></span>

<span data-ttu-id="d2359-250">Icebreaker は [Microsoft Teams の bot](../bots/what-are-bots.md) で、チームは、2つのランダムなチームメンバーを毎週1つずつペアにすることによって近づくことができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-250">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="d2359-251">Bot は、両方のメンバーに対して動作する空き時間を自動的に提案することで、スケジュールを簡単にします。</span><span class="sxs-lookup"><span data-stu-id="d2359-251">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="d2359-252">パーソナル接続を強化し、このアプリを使用して緊密な knit コミュニティを構築します。</span><span class="sxs-lookup"><span data-stu-id="d2359-252">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="d2359-253">Icebreaker アプリは、チーム全体にわたる個人の接続を促進するだけでなく、組織内の利息ベースコミュニティを cultivate するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="d2359-253">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="d2359-254">たとえば、このアプリを DevOps の趣味グループに対して使用すると、アイデアやベストプラクティスつれを組織全体に分散させることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-254">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="d2359-255">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker アプリ](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="d2359-257">報奨金</span><span class="sxs-lookup"><span data-stu-id="d2359-257">Incentives</span></span>

<span data-ttu-id="d2359-258">インセンティブは、トレーニングや変更管理イニシアティブなど、指定されたアクティビティに incentivized 従業員の参加を管理し、追跡するための [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="d2359-258">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="d2359-259">管理者はアプリを使用して、指定されたアクティビティを確立し、完了するためにポイントを割り当て、報奨に必要な適格性ポイントレベルを指定します。</span><span class="sxs-lookup"><span data-stu-id="d2359-259">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="d2359-260">従業員はアプリを使用して、蓄積されたポイントを表示したり、適格性に達した場合には、redeemable 報奨に同意します。</span><span class="sxs-lookup"><span data-stu-id="d2359-260">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="d2359-261">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![インセンティブアプリのデモ](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="d2359-263">インシデントレポーター</span><span class="sxs-lookup"><span data-stu-id="d2359-263">Incident Reporter</span></span>

<span data-ttu-id="d2359-264">インシデントレポーターは、組織内のインシデントの管理を最適化する [Microsoft Teams の bot](../bots/what-are-bots.md)  です。</span><span class="sxs-lookup"><span data-stu-id="d2359-264">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="d2359-265">Bot は、インシデントデータの自動収集、カスタマイズされたインシデントレポート、関連するステークホルダーの通知、およびエンドツーエンドのインシデント追跡を容易にします。</span><span class="sxs-lookup"><span data-stu-id="d2359-265">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="d2359-266">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-266">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![Incident レポーターグループのスコープビュー](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![インシデントレポーター個人用スコープビュー](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="new-employee-onboarding-9734"></a><span data-ttu-id="d2359-269">新入社員のオンボード &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-269">New Employee Onboarding &#9734;</span></span>

<span data-ttu-id="d2359-270">新入社員のオンボードとは、統合された Microsoft Teams および [SharePoint 新入社員のオンボードソリューション](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) で、お客様の新入社員向けの、一貫性のある高品質の開始時の実績を、入社時に提供することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-270">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="d2359-271">このアプリは、人手と誘導プロセス全体で関連情報を提供したり、フィードバックを共有し、序文を提供したり、すべてのオンボードタスクを行ったりするために、人的リソースチームおよび雇用マネージャーが使用することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-271">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="d2359-272">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-272">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="d2359-273">**新入社員案内カード** ![新しい従業員ウェルカムカードの画像](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="d2359-273">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="d2359-274">**新入社員チェックリスト** ![新しい従業員チェックリストの画像](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="d2359-274">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="d2359-275">バッジを開く</span><span class="sxs-lookup"><span data-stu-id="d2359-275">Open Badges</span></span>

<span data-ttu-id="d2359-276">バッジは、個人が Teams のコンテキスト内でデジタル学習資格情報バッジを獲得し、すべての場所で共有できるようにする Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-276">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="d2359-277">サードパーティのデジタルバッジの発行機関である機能を使用することによって、バッジ、 [Badgr](https://badgr.org/)、特典バッジは、受信者の badgr プロファイルに記録され、利用可能な手順の充実した画像を構築して共有できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-277">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="d2359-278">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-278">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![利用可能なバッジの画像](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![落札バッジビュー](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll-9734"></a><span data-ttu-id="d2359-281">Poll &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-281">Poll &#9734;</span></span>

<span data-ttu-id="d2359-282">Poll は、ユーザーがチームの意見や好みを収集できるように、チャットまたはチャネルで投票をすばやく作成して送信できるようにするカスタム Microsoft Teams [メッセージング拡張](../messaging-extensions/what-are-messaging-extensions.md) アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-282">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="d2359-283">このアプリは、すべての Teams プラットフォームクライアント (デスクトップ、ブラウザー、iOS、および Android) でサポートされており、Microsoft 365 サブスクリプションの一部として展開の準備ができています。</span><span class="sxs-lookup"><span data-stu-id="d2359-283">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="d2359-284">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-284">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![Teams ビューでの投票の作成](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="d2359-286">クイック応答</span><span class="sxs-lookup"><span data-stu-id="d2359-286">Quick Responses</span></span>

<span data-ttu-id="d2359-287">クイック応答は、ユーザーによく寄せられる質問 (Faq) を効果的に回答するための堅牢なソリューションを提供する Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-287">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="d2359-288">アプリでは、各クエリに手動で応答して情報を繰り返し表示するのではなく、Teams の [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)によって対話的なユーザー操作に対する応答のライブラリをビルドします。</span><span class="sxs-lookup"><span data-stu-id="d2359-288">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="d2359-289">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![応答のサンプルビュー](../assets/images/quick-responses.png)

## <a name="reflect-9734"></a><span data-ttu-id="d2359-291">&#9734; 反映</span><span class="sxs-lookup"><span data-stu-id="d2359-291">Reflect &#9734;</span></span>

<span data-ttu-id="d2359-292">リフレクションは、チームメンバーが同僚やグループリーダーと Teams 内に直接連携している状態を共有するための、安全で包括的なリソースを提供するカスタムの Microsoft Teams [メッセージング拡張](../messaging-extensions/what-are-messaging-extensions.md) アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-292">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="d2359-293">このアプリは channel、group、meeting、および1:1 のチャットで利用でき、チェックインの応答は、パブリック、プライベート、または完全に匿名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-293">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="d2359-294">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-294">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="d2359-295">**良好なポーリング**</span><span class="sxs-lookup"><span data-stu-id="d2359-295">**Well-being poll**</span></span>
    
    ![アプリユーザーのポーリングを反映します。](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="d2359-297">リモートサポート</span><span class="sxs-lookup"><span data-stu-id="d2359-297">Remote Support</span></span>

<span data-ttu-id="d2359-298">リモートサポートは、組織全体のサポート依頼者と内部のサポートチームの間でフォーカスがあるインターフェイスを提供する [Microsoft Teams の bot](../bots/what-are-bots.md) です。</span><span class="sxs-lookup"><span data-stu-id="d2359-298">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="d2359-299">エンドユーザーは、サポートのための要求を提出、編集、または取り消すことができます。また、サポートチームは、すべての要求を Teams プラットフォーム内で応答、管理、および更新できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-299">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="d2359-300">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-300">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![要求サポートフォーム](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![要求サポートの詳細](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="d2359-303">チームの要求</span><span class="sxs-lookup"><span data-stu-id="d2359-303">Request-a-team</span></span>

<span data-ttu-id="d2359-304">要求-a team は、企業組織の新しいチーム作成を最適化する Microsoft Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-304">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="d2359-305">このアプリは、ウィザードで指示された要求フォーム、組み込みの承認プロセス、要求状態ダッシュボード、および自動化されたチームビルドを統合することによって、新しいチームインスタンスを作成する際の標準化とベストプラクティスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d2359-305">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="d2359-306">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-306">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![要求-a team start ページビュー](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![要求-a-チームウィザードページビュー](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="d2359-309">チャネルの Scrums</span><span class="sxs-lookup"><span data-stu-id="d2359-309">Scrums for Channels</span></span>

<span data-ttu-id="d2359-310">Scrums for Channels は、ユーザーが Microsoft Teams 内のチャネルで Scrums をスケジュールして実行できるようにする、スクラムアシスタントアプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-310">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="d2359-311">このアプリは、リモートチームとチームが、さまざまな地理的場所とタイムゾーンのメンバーで構成された、毎日の更新情報を共有し、スクラムのスタンドアップ会議に参加できるようにするために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="d2359-311">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="d2359-312">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-312">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="d2359-313">グループチャットでスクラム会議を実施するには、「 [Scrums For Group chat](#scrums-for-group-chat) app template」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2359-313">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![Scrums for channels の設定ビュー](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Scrums for channels チームメンバー状態ビュー](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="d2359-316">グループチャットの Scrums</span><span class="sxs-lookup"><span data-stu-id="d2359-316">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="d2359-317">Scrums Status app テンプレートが更新され、グループチャット用に Scrums になりました。</span><span class="sxs-lookup"><span data-stu-id="d2359-317">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="d2359-318">グループチャットの Scrums は、グループチャットメンバーが非同期のスタンドアップ会議を実行し、毎日の更新内容を簡単に共有できるようにする、支援のあるスクラムアシスタントです。</span><span class="sxs-lookup"><span data-stu-id="d2359-318">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="d2359-319">これにより、グループチャットのすべてのメンバーがスクラムに投稿し、実行中のスクラムで他者が行った更新を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-319">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="d2359-320">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-320">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![グループチャットのデモの Scrums](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now-9734"></a><span data-ttu-id="d2359-322">今すぐ共有 &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-322">Share Now &#9734;</span></span>

<span data-ttu-id="d2359-323">今すぐ共有アプリは、ユーザーが Teams 環境内でコンテンツを簡単に共有できるようにすることで、同僚間での情報交換を促進します。</span><span class="sxs-lookup"><span data-stu-id="d2359-323">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="d2359-324">ユーザーは、アプリを使用して、チームメンバーと関心のあるアイテムを共有したり、新しい共有コンテンツを検出したり、プレファレンスを設定したり、お気に入りにブックマークを設定したりして、後で閲覧できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-324">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="d2359-325">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-325">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![コンテンツビューの選択](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="d2359-327">SharePoint リスト検索</span><span class="sxs-lookup"><span data-stu-id="d2359-327">SharePoint List Search</span></span>

<span data-ttu-id="d2359-328">Microsoft Teams でのコラボレーションは、多くの場合、SharePoint リスト内のアイテムに含まれている情報を参照します。</span><span class="sxs-lookup"><span data-stu-id="d2359-328">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="d2359-329">目的のアイテムへのリンクを貼り付けるだけで、すべてのユーザーに対して、会話からのコンテキストの切り替え、必要な情報の検索、および会話を続行するために Teams に戻ることが強制されます。</span><span class="sxs-lookup"><span data-stu-id="d2359-329">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="d2359-330">会話は、通常、新しいコメントを確認し、アイテム内に含まれる情報を更新するために、参照アイテムに再び切り替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="d2359-330">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="d2359-331">このコンテキストの切り替えは、グループ作業をスムーズにするための障壁を作成し、その亀裂についてのレシピとなります。</span><span class="sxs-lookup"><span data-stu-id="d2359-331">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="d2359-332">このような問題を軽減するために、リスト検索アプリテンプレートに移動することになります。</span><span class="sxs-lookup"><span data-stu-id="d2359-332">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="d2359-333">数百万人のユーザーが SharePoint を使用して、組織内のコアワークフローの一部を強化します。</span><span class="sxs-lookup"><span data-stu-id="d2359-333">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="d2359-334">ただし、リストに関する共同作業は、特に面倒な場合があります。</span><span class="sxs-lookup"><span data-stu-id="d2359-334">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="d2359-335">Microsoft Teams でリスト検索アプリテンプレートを使用すると、ユーザーは SharePoint リストアイテムの情報をチャット会話内に直接挿入して、リンクをチャットに挿入するだけで済むようになったため、コンテキスト切り替えが軽減されます。</span><span class="sxs-lookup"><span data-stu-id="d2359-335">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="d2359-336">この情報は、簡単に読める自動フォーマットのカードとして挿入され、ユーザーが会話に参加し続けるのを支援します。</span><span class="sxs-lookup"><span data-stu-id="d2359-336">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="d2359-337">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-337">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![検索アプリを一覧表示する](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="d2359-339">スタッフのチェックイン</span><span class="sxs-lookup"><span data-stu-id="d2359-339">Staff Check-ins</span></span>

<span data-ttu-id="d2359-340">スタッフのチェックインは、ビジネス担当者と現場担当者との間での監視コミュニケーションを可能にする、 [電力アプリケーション](/powerapps/powerapps-overview)ベースのアプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-340">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="d2359-341">スタッフは、スケジュールされた、または臨時に Teams から直接、タイムクリティカルな情報と進捗状況の更新を簡単に提供できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-341">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="d2359-342">アプリでは、リアルタイムの場所、写真、およびメモだけでなく、アラームの通知や自動化されたワークフローをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d2359-342">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="d2359-343">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-343">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![チェックインビューを作成する](../assets/images/staff-check-ins-create.png)

## <a name="survey-9734"></a><span data-ttu-id="d2359-345">アンケート &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-345">Survey &#9734;</span></span>

<span data-ttu-id="d2359-346">アンケートは、チャットまたはチャネルでアンケートを作成してデータを収集し、実用的な洞察を得ることができる、カスタムの Microsoft Teams [メッセージング拡張](../messaging-extensions/what-are-messaging-extensions.md) アプリです。</span><span class="sxs-lookup"><span data-stu-id="d2359-346">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="d2359-347">このアプリは、すべての Teams プラットフォームクライアント (デスクトップ、ブラウザー、iOS、および Android) でサポートされており、Microsoft 365 サブスクリプションの一部として展開の準備ができています。</span><span class="sxs-lookup"><span data-stu-id="d2359-347">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="d2359-348">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-348">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![Teams ビューでアンケートを作成する](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="visitor-management-9734"></a><span data-ttu-id="d2359-350">ビジタ管理 &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-350">Visitor Management &#9734;</span></span>

<span data-ttu-id="d2359-351">ゲスト管理アプリを使用すると、組織や従業員は、Microsoft Teams から直接オンサイトビジタープロセスを簡単かつ効率的に管理できます。</span><span class="sxs-lookup"><span data-stu-id="d2359-351">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="d2359-352">アプリを使用すると、従業員は訪問者の要求を作成し、訪問者のダッシュボードを介して要求の状態を一元管理し、訪問者が到着したときにリアルタイムで通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-352">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="d2359-353">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![要求ビューを作成する](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![訪問者の到着通知](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards-9734"></a><span data-ttu-id="d2359-356">Workplace 賞 &#9734;</span><span class="sxs-lookup"><span data-stu-id="d2359-356">Workplace Awards &#9734;</span></span>

<span data-ttu-id="d2359-357">Workplace 賞は Teams アプリテンプレートです。これにより、モダンワークプレースで、認識を促進し、従業員の感謝を促します。</span><span class="sxs-lookup"><span data-stu-id="d2359-357">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="d2359-358">このアプリを使用すると、従業員が容易に仕事仲間を指名して承認することができる従業員報奨および認識 (R&R) プログラムを設定および管理できます。また、R&R リーダーは、送信された nominations の表示、特典の付与、受信者のアナウンスを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d2359-358">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="d2359-359">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="d2359-359">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="d2359-360">Workplace 賞の推薦カード</span><span class="sxs-lookup"><span data-stu-id="d2359-360">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Workplace 受賞リストタブ](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="d2359-362">参照したいアプリテンプレートのアイデアがあるかどうか。</span><span class="sxs-lookup"><span data-stu-id="d2359-362">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="d2359-363">お知らせ[ください](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。</span><span class="sxs-lookup"><span data-stu-id="d2359-363">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
