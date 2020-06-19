---
title: Teams でコネクタをシフトする
description: 要員管理は、Teams のコネクタをシフト
author: laujan
ms.date: 03/09/2020
keywords: Microsoft Teams コネクタ kronos
ms.author: lajanuar
ms.openlocfilehash: eae88d02647f0547eed53d8bd5e00e13a8e62096
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "44801297"
---
# <a name="microsoft-teams-shifts-wfm-connectors"></a><span data-ttu-id="066df-104">Microsoft Teams が WFM コネクタをシフトする</span><span class="sxs-lookup"><span data-stu-id="066df-104">Microsoft Teams Shifts WFM connectors</span></span>  

## <a name="workforce-management-connectors-wfm-for-firstline-workers"></a><span data-ttu-id="066df-105">第一線ワーカーの労働力管理コネクタ (wfm)</span><span class="sxs-lookup"><span data-stu-id="066df-105">Workforce management connectors (WFM) for firstline workers</span></span> 

<span data-ttu-id="066df-106">Teams は、wfm コネクタをシフトする、運用の準備が整っているオープンソースであり、コミュニティによる統合による統合を提供しています。これは、チームがシフトしてくる第一線ワーカーのデジタル変換に対して、シームレスな操作と迅速なプロセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="066df-106">Teams Shifts WFM connectors are production-ready, open-source, and community-driven integrations that offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="066df-107">各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="066df-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="066df-108">完全なソースコードは、詳細に調査したり、特定のニーズに合わせて調整したりできる、GitHub リポジトリで利用できます。</span><span class="sxs-lookup"><span data-stu-id="066df-108">The complete source code is available in our GitHub repo where it can be explored in detail and/or forked and tailored to meet your specific needs.</span></span>

## <a name="key-benefits-teams-shifts-wfm-connectors"></a><span data-ttu-id="066df-109">主な利点: Teams での WFM コネクタのシフト</span><span class="sxs-lookup"><span data-stu-id="066df-109">Key benefits: Teams Shifts WFM connectors</span></span>

* <span data-ttu-id="066df-110">**プラグアンドプレイの操作。**</span><span class="sxs-lookup"><span data-stu-id="066df-110">**Plug and play experience.**</span></span> <span data-ttu-id="066df-111">すべてのシフトの WFM コネクタには、Microsoft Azure で必要なすべてのサービスをホストできる ARM Azure 展開スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="066df-111">All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="066df-112">アプリを展開するためのコーディングは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="066df-112">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="066df-113">**運用可能なコード。**</span><span class="sxs-lookup"><span data-stu-id="066df-113">**Production-ready code.**</span></span> <span data-ttu-id="066df-114">すべてのシフトコネクタは、推奨されるセキュリティとインフラストラクチャのベストプラクティスに準拠しており、コミュニティで提出されたすべての変更を確認して、引き続き準拠するようにします。</span><span class="sxs-lookup"><span data-stu-id="066df-114">All  Shifts connectors conform to recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="066df-115">**カスタマイズと拡張。**</span><span class="sxs-lookup"><span data-stu-id="066df-115">**Customizable and extensible.**</span></span> <span data-ttu-id="066df-116"> すべてのシフトがすぐに使用できるように展開する準備が整っていますが、コードベースと展開スクリプト全体が提供されるので、独自のニーズに合わせてカスタマイズまたは拡張することが容易になります。</span><span class="sxs-lookup"><span data-stu-id="066df-116"> While all Shifts WFM connectors are ready to deploy for immediate use, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="066df-117">**詳細なドキュメント & サポート。**</span><span class="sxs-lookup"><span data-stu-id="066df-117">**Detailed documentation & support.**</span></span> <span data-ttu-id="066df-118"> すべてのシフトの WFM コネクタには、ソリューションのアーキテクチャ、展開、および構成手順に関するエンドツーエンドのドキュメントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="066df-118"> All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="066df-119">コネクタリポジトリは監視されるので、リポジトリの GitHub 問題追跡ツールを使用して発生した問題、課題、または問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="066df-119">The connector repositories are monitored, so please report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="066df-120">**シームレスな統合。**</span><span class="sxs-lookup"><span data-stu-id="066df-120">**Seamless integration.**</span></span> <span data-ttu-id="066df-121">Wfm ソリューションと teams のシフトを統合することで、第一線ワーカーは teams の交代アプリを使用して、自分のスケジュールとシフト時間を表示/管理し、別のアプリにコンテキストを切り替えることなく、自分のモバイルデバイスやデスクトップから teams で提供されている他のすべてのコラボレーション機能を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="066df-121">The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view/manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>

<span data-ttu-id="066df-122">**Teams でのシフトビューを開く**</span><span class="sxs-lookup"><span data-stu-id="066df-122">**Open shifts view in Teams**</span></span>  
<span data-ttu-id="066df-123">![Teams でのオープンシフト](../assets/images/teams-open-shifts-view.png)</span><span class="sxs-lookup"><span data-stu-id="066df-123">![Open shifts in Teams](../assets/images/teams-open-shifts-view.png)</span></span>

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="066df-124">Kronos-Teams シフトコネクタ</span><span class="sxs-lookup"><span data-stu-id="066df-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="066df-125">オープンソースコードでは、次の最初の行のワーカーおよびマネージャーのシナリオについて Teams の移行 (デスクトップ/モバイル Teams アプリ) を使用して、Kronos 労働力の中央バージョン8.1 以降を統合することができます。</span><span class="sxs-lookup"><span data-stu-id="066df-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="066df-126">スケジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="066df-126">View schedule.</span></span>

1. <span data-ttu-id="066df-127">公開して、オープンシフトを要求します。</span><span class="sxs-lookup"><span data-stu-id="066df-127">Publish and request open shifts.</span></span>

1. <span data-ttu-id="066df-128">切り替えを行います。</span><span class="sxs-lookup"><span data-stu-id="066df-128">Swap shifts.</span></span>

1. <span data-ttu-id="066df-129">要求時間がオフになっています。</span><span class="sxs-lookup"><span data-stu-id="066df-129">Request time off.</span></span>

1. <span data-ttu-id="066df-130">シフトを提供します。</span><span class="sxs-lookup"><span data-stu-id="066df-130">Offer shifts.</span></span>

[<span data-ttu-id="066df-131">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="066df-131">Get it on GitHub</span></span>]( https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="066df-132">JDA-Teams シフトコネクタ</span><span class="sxs-lookup"><span data-stu-id="066df-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="066df-133">オープンソースコードでは、JDA (BlueYonder) バージョン17.2 以降を統合できます。この場合、次の最初の行のワーカーおよびマネージャーのシナリオについて Teams の交代 (デスクトップ/モバイル Teams アプリ) を使用します。</span><span class="sxs-lookup"><span data-stu-id="066df-133">With open-source code, you can integrate JDA (BlueYonder) Version 17.2 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="066df-134">JDA の移動とスケジュールグループを発行し、Teams で表示します。</span><span class="sxs-lookup"><span data-stu-id="066df-134">Publish shifts and schedule groups in JDA and view in Teams.</span></span>

1. <span data-ttu-id="066df-135">シフトの切り替えや休暇の要求など、高度なスケジュールシナリオを有効にします。</span><span class="sxs-lookup"><span data-stu-id="066df-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

1. <span data-ttu-id="066df-136">[Microsoft GRAPH API](/graph/api/resources/shift?view=graph-rest-beta)を使用して、ユーザーの可用性をシフトに設定します。</span><span class="sxs-lookup"><span data-stu-id="066df-136">Set  user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta) .</span></span>

[<span data-ttu-id="066df-137">GitHub で取得する</span><span class="sxs-lookup"><span data-stu-id="066df-137">Get it on GitHub</span></span>](https://aka.ms/JDAShiftsConnector)</br></br>
