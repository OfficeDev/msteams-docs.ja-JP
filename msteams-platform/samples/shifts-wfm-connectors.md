---
title: 本番対応の Shifts コネクタ
description: Workforce management Shifts connectors for Teams
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
localization_priority: Normal
keywords: Microsoft Teams コネクタ kronos
ms.author: lajanuar
ms.openlocfilehash: 088c049342c36b4f126b4a9d2f788601378b7db4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069143"
---
# <a name="production-ready-shifts-connectors"></a><span data-ttu-id="a8071-104">本番対応の Shifts コネクタ</span><span class="sxs-lookup"><span data-stu-id="a8071-104">Production-ready Shifts Connectors</span></span>  

<span data-ttu-id="a8071-105">TeamsShifts Workforce Management (WFM) コネクタは、運用対応、オープン ソース、コミュニティ駆動型の統合であり、ファーストライン ワーカーに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a8071-105">Teams Shifts Workforce management (WFM) connectors are production-ready, open-source, and community-driven integrations, useful for firstline workers.</span></span> <span data-ttu-id="a8071-106">シームレスなエクスペリエンスと迅速なプロセスを提供し、シフトを使用したファーストラインワーカーのデジタルTeams提供します。</span><span class="sxs-lookup"><span data-stu-id="a8071-106">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="a8071-107">各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="a8071-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="a8071-108">完全なソース コードは、リポジトリGitHubできます。</span><span class="sxs-lookup"><span data-stu-id="a8071-108">The complete source code is available in GitHub repository.</span></span> <span data-ttu-id="a8071-109">詳細またはフォークを探索し、特定のニーズに合わせてカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="a8071-109">You can explore in detail or fork, and customize to meet your specific needs.</span></span>   

<span data-ttu-id="a8071-110">このドキュメントでは、Teams Shifts WFM コネクタ、Kronos-to-Teams Shifts コネクタ、および JDA から Teams Shifts コネクタの主な利点の概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="a8071-110">This document gives an overview of key benefits of Teams Shifts WFM connectors, Kronos-to-Teams Shifts connector, and JDA-to-Teams Shifts connector.</span></span>

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a><span data-ttu-id="a8071-111">Shifts WFM Teamsの主な利点</span><span class="sxs-lookup"><span data-stu-id="a8071-111">Key benefits of Teams Shifts WFM connectors</span></span>

<span data-ttu-id="a8071-112">Shifts WFM コネクタの主な利点Teams次に示します。</span><span class="sxs-lookup"><span data-stu-id="a8071-112">Following are the key benefits of Teams Shifts WFM connectors:</span></span>

* <span data-ttu-id="a8071-113">**プラグ アンド プレイのエクスペリエンス:** すべての Shifts WFM コネクタには、ARMのすべての必要なサービスをホストできる Azure 展開スクリプトがMicrosoft Azure。</span><span class="sxs-lookup"><span data-stu-id="a8071-113">**Plug and play experience:** All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="a8071-114">アプリを展開するためにコーディングは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="a8071-114">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="a8071-115">**実稼働可能なコード:** すべての Shifts コネクタは、推奨されるセキュリティとインフラストラクチャのベスト プラクティスに準拠し、コミュニティが提出した変更はすべて確認され、継続的に準拠します。</span><span class="sxs-lookup"><span data-stu-id="a8071-115">**Production-ready code:** All  Shifts connectors conform to the recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="a8071-116">**カスタマイズ可能で拡張可能:**  すべての Shifts WFM コネクタは、すぐに使用できるように展開できる状態ですが、コード ベースと展開スクリプト全体をすぐに利用できます。</span><span class="sxs-lookup"><span data-stu-id="a8071-116">**Customizable and extensible:**  While all Shifts WFM connectors are ready to deploy for immediate use, with the entire code base and deployment scripts readily available.</span></span> <span data-ttu-id="a8071-117">独自のニーズに合わせて簡単にカスタマイズまたは拡張できます。</span><span class="sxs-lookup"><span data-stu-id="a8071-117">You can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="a8071-118">**サポートに関する&ドキュメント:**  すべての Shifts WFM コネクタには、ソリューションのアーキテクチャ、展開、および構成手順に関するエンドツーエンドのドキュメントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="a8071-118">**Detailed documentation & support:**  All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="a8071-119">コネクタ リポジトリは監視され、repo の [問題] トラッカーを通じて発生する問題、課題、またはGitHubできます。</span><span class="sxs-lookup"><span data-stu-id="a8071-119">The connector repositories are monitored, so that you can report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="a8071-120">**シームレスな統合:** WFM ソリューションと Teams Shifts の統合により、ファーストラインワーカーは Teams Shifts アプリを使用してスケジュールとシフト時間を表示または管理し、コンテキストを別のアプリに切り替えることなく、Teams で提供される他のすべての豊富なコラボレーション機能をモバイル デバイスまたはデスクトップから使用できます。</span><span class="sxs-lookup"><span data-stu-id="a8071-120">**Seamless integration:** The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view or manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>  

<span data-ttu-id="a8071-121">**[シフト] ビューを開Teams**</span><span class="sxs-lookup"><span data-stu-id="a8071-121">**Open shifts view in Teams**</span></span> 

<span data-ttu-id="a8071-122">次の図に、Teamsシフト ビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a8071-122">The shifts view in Teams is shown in the following image:</span></span> 

![シフトを開Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="a8071-124">Kronos-to-Teams Shifts コネクタ</span><span class="sxs-lookup"><span data-stu-id="a8071-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="a8071-125">オープンソース コードを使用すると、Kronos Workforce Central Version 8.1 以上を、デスクトップやモバイル Teams アプリなどの Teams Shifts と統合して、次のファーストライン ワーカーとマネージャーのシナリオに対応できます。</span><span class="sxs-lookup"><span data-stu-id="a8071-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="a8071-126">スケジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="a8071-126">View schedule.</span></span>

* <span data-ttu-id="a8071-127">オープン シフトを発行して要求します。</span><span class="sxs-lookup"><span data-stu-id="a8071-127">Publish and request open shifts.</span></span>

* <span data-ttu-id="a8071-128">スワップ シフト。</span><span class="sxs-lookup"><span data-stu-id="a8071-128">Swap shifts.</span></span>

* <span data-ttu-id="a8071-129">要求の時間を指定します。</span><span class="sxs-lookup"><span data-stu-id="a8071-129">Request time off.</span></span>

* <span data-ttu-id="a8071-130">シフトを提供します。</span><span class="sxs-lookup"><span data-stu-id="a8071-130">Offer shifts.</span></span>

<span data-ttu-id="a8071-131">Kronos-to-Teams Shifts コネクタの展開の詳細については[、「Get it on](https://aka.ms/KronosShiftsConnector)GitHub」 を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a8071-131">For more information on deployment of Kronos-to-Teams Shifts connector, see [Get it on GitHub](https://aka.ms/KronosShiftsConnector).</span></span>

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="a8071-132">JDA-to-Teams Shifts コネクタ</span><span class="sxs-lookup"><span data-stu-id="a8071-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="a8071-133">オープンソース コードを使用すると、BlueYonder Version 17.2 以上などの JDA を、デスクトップやモバイル Teams アプリなどの Teams Shifts と統合して、次のファーストライン ワーカーおよびマネージャー シナリオに対応できます。</span><span class="sxs-lookup"><span data-stu-id="a8071-133">With open-source code, you can integrate JDA, such as BlueYonder Version 17.2 and above, with Teams Shifts  such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="a8071-134">JDA でシフトとスケジュール グループを発行し、そのグループを Teams。</span><span class="sxs-lookup"><span data-stu-id="a8071-134">Publish shifts and schedule groups in JDA and view them in Teams.</span></span>

* <span data-ttu-id="a8071-135">シフト スワップの要求やタイム オフを含む、豊富なスケジュール設定シナリオを有効にします。</span><span class="sxs-lookup"><span data-stu-id="a8071-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

* <span data-ttu-id="a8071-136">Microsoft Graph [API を使用してユーザーの可用性を設定します](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a8071-136">Set user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).</span></span>

<span data-ttu-id="a8071-137">投稿と提案の詳細については[、「Get it on GitHub」 を参照してください](https://aka.ms/JDAShiftsConnector)。</span><span class="sxs-lookup"><span data-stu-id="a8071-137">For more information on contribution and suggestion, see [Get it on GitHub](https://aka.ms/JDAShiftsConnector).</span></span></br></br>

## <a name="see-also"></a><span data-ttu-id="a8071-138">関連項目</span><span class="sxs-lookup"><span data-stu-id="a8071-138">See also</span></span>

[<span data-ttu-id="a8071-139">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="a8071-139">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
