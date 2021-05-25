---
title: モバイルのタブ
description: モバイルでタブを実装するための開発者Microsoft Teams説明します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 41ba96b64bd31f3b226aeba72969bc44c1ae8955
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630657"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="fb6de-103">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="fb6de-103">Tabs on mobile</span></span>

<span data-ttu-id="fb6de-104">タブを含む Microsoft Teams アプリを構築する場合は、Android クライアントと iOS クライアントの両方でタブがどのように機能Microsoft Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="fb6de-104">When you're building a Microsoft Teams app that includes a tab, you must consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="fb6de-105">以下のセクションでは、考慮する必要がある主要なシナリオの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb6de-105">The sections below outline some of the key scenarios you need to consider.</span></span>

## <a name="authentication"></a><span data-ttu-id="fb6de-106">認証</span><span class="sxs-lookup"><span data-stu-id="fb6de-106">Authentication</span></span>

<span data-ttu-id="fb6de-107">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb6de-107">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

## <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="fb6de-108">低帯域幅と断続的な接続</span><span class="sxs-lookup"><span data-stu-id="fb6de-108">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="fb6de-109">モバイル クライアントは、低帯域幅と断続的な接続で定期的に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb6de-109">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="fb6de-110">アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb6de-110">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="fb6de-111">また、長時間実行されるプロセスに対してユーザーにフィードバックを提供するユーザー進行状況インジケーターも必要です。</span><span class="sxs-lookup"><span data-stu-id="fb6de-111">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="testing-on-mobile-clients"></a><span data-ttu-id="fb6de-112">モバイル クライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="fb6de-112">Testing on mobile clients</span></span>

<span data-ttu-id="fb6de-113">さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb6de-113">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="fb6de-114">Android デバイスの場合 [、DevTools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="fb6de-114">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="fb6de-115">タブレットを含む、高パフォーマンスデバイスと低パフォーマンスデバイスの両方でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="fb6de-115">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

## <a name="distribution"></a><span data-ttu-id="fb6de-116">配布</span><span class="sxs-lookup"><span data-stu-id="fb6de-116">Distribution</span></span>

<span data-ttu-id="fb6de-117">モバイル クライアントで適切にTeams機能するには、モバイル ストアに一覧表示されているアプリTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb6de-117">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="fb6de-118">タブの可用性と動作は、アプリが承認されたかどうかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="fb6de-118">Tab availability and behavior depends on whether your app is approved.</span></span>

### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="fb6de-119">モバイル用にTeamsストア上のアプリ</span><span class="sxs-lookup"><span data-stu-id="fb6de-119">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="fb6de-120">次の表では、アプリがモバイル ストアに表示され、モバイルTeams承認された場合のタブの可用性と動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb6de-120">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use:</span></span>

|<span data-ttu-id="fb6de-121">機能</span><span class="sxs-lookup"><span data-stu-id="fb6de-121">Capability</span></span>   |<span data-ttu-id="fb6de-122">モバイルの可用性</span><span class="sxs-lookup"><span data-stu-id="fb6de-122">Mobile availability?</span></span>   |<span data-ttu-id="fb6de-123">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="fb6de-123">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="fb6de-124">チャネル</span><span class="sxs-lookup"><span data-stu-id="fb6de-124">Channel</span></span> <br /> <span data-ttu-id="fb6de-125">[グループ] タブ</span><span class="sxs-lookup"><span data-stu-id="fb6de-125">and group tab</span></span>|<span data-ttu-id="fb6de-126">はい</span><span class="sxs-lookup"><span data-stu-id="fb6de-126">Yes</span></span>|<span data-ttu-id="fb6de-127">アプリの構成を使用Teamsモバイル クライアントのタブが開 `contentUrl` きます。</span><span class="sxs-lookup"><span data-stu-id="fb6de-127">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="fb6de-128">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="fb6de-128">Personal app</span></span>|<span data-ttu-id="fb6de-129">はい</span><span class="sxs-lookup"><span data-stu-id="fb6de-129">Yes</span></span>|<span data-ttu-id="fb6de-130">[個人用アプリ] タブの各タブが、Teamsを使用してモバイル クライアントに表示 `contentUrl` されます。</span><span class="sxs-lookup"><span data-stu-id="fb6de-130">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="fb6de-131">モバイルで承認Teamsアプリストアのアプリ</span><span class="sxs-lookup"><span data-stu-id="fb6de-131">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="fb6de-132">次の表は、アプリがモバイル ストアに一覧表示されているが、モバイルTeams承認されていない場合のタブの可用性と動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb6de-132">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use:</span></span>

| <span data-ttu-id="fb6de-133">機能</span><span class="sxs-lookup"><span data-stu-id="fb6de-133">Capability</span></span> | <span data-ttu-id="fb6de-134">モバイルの可用性</span><span class="sxs-lookup"><span data-stu-id="fb6de-134">Mobile availability?</span></span> | <span data-ttu-id="fb6de-135">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="fb6de-135">Mobile behavior</span></span> |
|----------|-----------|------------|
|<span data-ttu-id="fb6de-136">[チャネルとグループ] タブ</span><span class="sxs-lookup"><span data-stu-id="fb6de-136">Channel and group tab</span></span>|<span data-ttu-id="fb6de-137">はい</span><span class="sxs-lookup"><span data-stu-id="fb6de-137">Yes</span></span>|<span data-ttu-id="fb6de-138">タブは、アプリの構成を使用して Teams モバイル クライアントではなく、デバイスの既定のブラウザーで開きます。これは、ソース コードの関数にも含める `websiteUrl` 必要 `setSettings()` [があります](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="fb6de-138">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration, which also must be included in your source code's `setSettings()` [function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true).</span></span> <span data-ttu-id="fb6de-139">ただし、アプリの横にある [詳細] を選択し、[開く]を選択すると、Teams モバイルクライアントのタブが表示され、アプリの構成がトリガー `contentUrl` されます。</span><span class="sxs-lookup"><span data-stu-id="fb6de-139">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="fb6de-140">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="fb6de-140">Personal app</span></span>|<span data-ttu-id="fb6de-141">なし</span><span class="sxs-lookup"><span data-stu-id="fb6de-141">No</span></span>|<span data-ttu-id="fb6de-142">該当なし</span><span class="sxs-lookup"><span data-stu-id="fb6de-142">Not applicable</span></span>|

### <a name="apps-not-on-teams-store"></a><span data-ttu-id="fb6de-143">アプリがストアTeamsしない</span><span class="sxs-lookup"><span data-stu-id="fb6de-143">Apps not on Teams store</span></span>

<span data-ttu-id="fb6de-144">アプリをサイドロードする場合や、組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。</span><span class="sxs-lookup"><span data-stu-id="fb6de-144">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>

## <a name="see-also"></a><span data-ttu-id="fb6de-145">関連項目</span><span class="sxs-lookup"><span data-stu-id="fb6de-145">See also</span></span>

* [<span data-ttu-id="fb6de-146">タブデザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="fb6de-146">Tab design guidelines</span></span>](~/tabs/design/tabs.md)
