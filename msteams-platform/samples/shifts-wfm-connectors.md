---
title: Teams シフト コネクタ
description: Teams の従業員管理シフト コネクタ
ms.topic: reference
author: laujan
ms.date: 03/09/2020
keywords: Microsoft Teams コネクタ kronos
ms.author: lajanuar
ms.openlocfilehash: 9d32c9e1aa3baba660440492df55bb00f677baa4
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014594"
---
# <a name="microsoft-teams-shifts-wfm-connectors"></a><span data-ttu-id="75356-104">Microsoft Teams が WFM コネクタをシフトする</span><span class="sxs-lookup"><span data-stu-id="75356-104">Microsoft Teams Shifts WFM connectors</span></span>  

## <a name="workforce-management-connectors-wfm-for-firstline-workers"></a><span data-ttu-id="75356-105">ファーストライン ワーカー用の要員管理コネクタ (WFM)</span><span class="sxs-lookup"><span data-stu-id="75356-105">Workforce management connectors (WFM) for firstline workers</span></span> 

<span data-ttu-id="75356-106">Teams シフト WFM コネクタは、Teams シフトによるファーストライン ワーカーのデジタル変換のためのシームレスなエクスペリエンスと迅速なプロセスを提供する、実稼働対応、オープン ソース、およびコミュニティ駆動型の統合です。</span><span class="sxs-lookup"><span data-stu-id="75356-106">Teams Shifts WFM connectors are production-ready, open-source, and community-driven integrations that offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="75356-107">各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="75356-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="75356-108">完全なソース コードは、GitHub リポジトリで入手できます。このリポジトリでは、特定のニーズに合わせて詳細に探索したり、フォークしたり、カスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="75356-108">The complete source code is available in our GitHub repo where it can be explored in detail and/or forked and tailored to meet your specific needs.</span></span>

## <a name="key-benefits-teams-shifts-wfm-connectors"></a><span data-ttu-id="75356-109">主な利点: Teams が WFM コネクタをシフトする</span><span class="sxs-lookup"><span data-stu-id="75356-109">Key benefits: Teams Shifts WFM connectors</span></span>

* <span data-ttu-id="75356-110">**プラグ アンド プレイ エクスペリエンス。**</span><span class="sxs-lookup"><span data-stu-id="75356-110">**Plug and play experience.**</span></span> <span data-ttu-id="75356-111">すべての Shifts WFM コネクタには、必要ARMサービスを Microsoft Azure でホストできる Azure 展開スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="75356-111">All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="75356-112">アプリを展開するためにコーディングは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="75356-112">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="75356-113">**実稼働対応のコード。**</span><span class="sxs-lookup"><span data-stu-id="75356-113">**Production-ready code.**</span></span> <span data-ttu-id="75356-114">すべてのシフト コネクタは推奨されるセキュリティとインフラストラクチャのベスト プラクティスに準拠し、コミュニティから提出された変更はすべて、継続的に準拠するためにレビューされます。</span><span class="sxs-lookup"><span data-stu-id="75356-114">All  Shifts connectors conform to recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="75356-115">**カスタマイズ可能で拡張可能。**</span><span class="sxs-lookup"><span data-stu-id="75356-115">**Customizable and extensible.**</span></span> <span data-ttu-id="75356-116"> すべての Shifts WFM コネクタは、すぐに使用するために展開できる状態ですが、独自のニーズに合わせて簡単にカスタマイズまたは拡張できるよう、コード ベースと展開スクリプト全体が用意されています。</span><span class="sxs-lookup"><span data-stu-id="75356-116"> While all Shifts WFM connectors are ready to deploy for immediate use, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="75356-117">**サポートに関する&ドキュメント。**</span><span class="sxs-lookup"><span data-stu-id="75356-117">**Detailed documentation & support.**</span></span> <span data-ttu-id="75356-118"> すべての Shifts WFM コネクタには、ソリューションのアーキテクチャ、展開、および構成の手順に関するエンドツーエンドのドキュメントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="75356-118"> All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="75356-119">コネクタ リポジトリは監視されます。そのため、リポジトリの GitHub の問題追跡ツールを使用して、発生した問題、課題、または困難を報告してください。</span><span class="sxs-lookup"><span data-stu-id="75356-119">The connector repositories are monitored, so please report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="75356-120">**シームレスな統合。**</span><span class="sxs-lookup"><span data-stu-id="75356-120">**Seamless integration.**</span></span> <span data-ttu-id="75356-121">WFM ソリューションと Teams シフトの統合により、ファーストライン ワーカーは Teams シフト アプリを使用してスケジュールとシフト タイムを表示/管理し、Teams で提供されるその他すべての豊富なコラボレーション機能をモバイル デバイスやデスクトップから使用できます。コンテキストを別のアプリに切り替える必要が生じることなく、Teams で提供されます。</span><span class="sxs-lookup"><span data-stu-id="75356-121">The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view/manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>

<span data-ttu-id="75356-122">**Teams でシフト ビューを開く**</span><span class="sxs-lookup"><span data-stu-id="75356-122">**Open shifts view in Teams**</span></span>  
<span data-ttu-id="75356-123">![Teams でシフトを開く](../assets/images/teams-open-shifts-view.png)</span><span class="sxs-lookup"><span data-stu-id="75356-123">![Open shifts in Teams](../assets/images/teams-open-shifts-view.png)</span></span>

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="75356-124">Kronos から Teams へのシフト コネクタ</span><span class="sxs-lookup"><span data-stu-id="75356-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="75356-125">オープン ソース コードを使用すると、Kronos Workforce Central Version 8.1 以上を Teams シフト (デスクトップ/モバイル Teams アプリ) と統合して、次のファーストライン ワーカーおよびマネージャー シナリオに対応できます。</span><span class="sxs-lookup"><span data-stu-id="75356-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="75356-126">スケジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="75356-126">View schedule.</span></span>

1. <span data-ttu-id="75356-127">オープン シフトを公開して要求します。</span><span class="sxs-lookup"><span data-stu-id="75356-127">Publish and request open shifts.</span></span>

1. <span data-ttu-id="75356-128">スワップ シフト。</span><span class="sxs-lookup"><span data-stu-id="75356-128">Swap shifts.</span></span>

1. <span data-ttu-id="75356-129">要求のタイム オフ。</span><span class="sxs-lookup"><span data-stu-id="75356-129">Request time off.</span></span>

1. <span data-ttu-id="75356-130">シフトを提供します。</span><span class="sxs-lookup"><span data-stu-id="75356-130">Offer shifts.</span></span>

[<span data-ttu-id="75356-131">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="75356-131">Get it on GitHub</span></span>]( https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="75356-132">JDA から Teams へのシフト コネクタ</span><span class="sxs-lookup"><span data-stu-id="75356-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="75356-133">オープン ソース コードを使用すると、JDA (BlueYonder) バージョン 17.2 以上を Teams シフト (デスクトップ/モバイル Teams アプリ) と統合して、次のファーストライン ワーカーおよびマネージャー シナリオに対応できます。</span><span class="sxs-lookup"><span data-stu-id="75356-133">With open-source code, you can integrate JDA (BlueYonder) Version 17.2 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="75356-134">JDA でシフトを公開し、グループをスケジュールし、Teams で表示します。</span><span class="sxs-lookup"><span data-stu-id="75356-134">Publish shifts and schedule groups in JDA and view in Teams.</span></span>

1. <span data-ttu-id="75356-135">シフト スワップの要求やタイム オフなど、豊富なスケジュールシナリオを有効にします。</span><span class="sxs-lookup"><span data-stu-id="75356-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

1. <span data-ttu-id="75356-136">シフト用 Microsoft [Graph API を使用してユーザーの可用性を設定します](/graph/api/resources/shift?view=graph-rest-beta) 。</span><span class="sxs-lookup"><span data-stu-id="75356-136">Set  user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta) .</span></span>

[<span data-ttu-id="75356-137">GitHub で入手する</span><span class="sxs-lookup"><span data-stu-id="75356-137">Get it on GitHub</span></span>](https://aka.ms/JDAShiftsConnector)</br></br>
