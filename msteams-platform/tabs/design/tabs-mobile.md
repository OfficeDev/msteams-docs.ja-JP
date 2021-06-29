---
title: モバイルのタブ
description: モバイルでタブを実装するための開発者Microsoft Teams説明します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 5053160f2456a5d1c5f68cb74ea3ccc5c5eabca5
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179721"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="1a5e5-103">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-103">Tabs on mobile</span></span>

<span data-ttu-id="1a5e5-104">タブを含む Microsoft Teamsアプリを構築する場合は、Android クライアントと iOS クライアントの両方でタブがどのように機能Microsoft Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-104">When you are building a Microsoft Teams app that includes a tab, you must test how your tab functions on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="1a5e5-105">この記事では、考慮する必要がある主要なシナリオの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-105">This article outlines some of the key scenarios you must consider.</span></span>

<span data-ttu-id="1a5e5-106">モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-106">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="1a5e5-107">最適なユーザー エクスペリエンスを実現するには、タブを作成する際に、この記事のモバイルタブのガイダンスに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-107">To ensure optimal user experience, you must follow the guidance for tabs on mobile in this article when creating your tabs.</span></span>

<span data-ttu-id="1a5e5-108">モバイル[ストアを通じて配布Teamsモバイル](~/concepts/deploy-and-publish/appsource/publish.md)クライアントに対する個別の承認プロセスがあります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-108">Apps [distributed through the Teams store](~/concepts/deploy-and-publish/appsource/publish.md) have a separate approval process for mobile clients.</span></span> <span data-ttu-id="1a5e5-109">このようなアプリの既定の動作は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-109">The default behavior of such apps is as follows:</span></span>

| <span data-ttu-id="1a5e5-110">**アプリの機能**</span><span class="sxs-lookup"><span data-stu-id="1a5e5-110">**App capability**</span></span> | <span data-ttu-id="1a5e5-111">**アプリが承認された場合の動作**</span><span class="sxs-lookup"><span data-stu-id="1a5e5-111">**Behavior if app is approved**</span></span> | <span data-ttu-id="1a5e5-112">**アプリが承認されていない場合の動作**</span><span class="sxs-lookup"><span data-stu-id="1a5e5-112">**Behavior if app is not approved**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a5e5-113">**[個人] タブ**</span><span class="sxs-lookup"><span data-stu-id="1a5e5-113">**Personal tabs**</span></span> | <span data-ttu-id="1a5e5-114">モバイル クライアントの下部バーにアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-114">App appears in the bottom bar of the mobile clients.</span></span> <span data-ttu-id="1a5e5-115">タブは、クライアントTeams開きます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-115">Tabs open in the Teams client.</span></span> | <span data-ttu-id="1a5e5-116">モバイル クライアントの下部バーにアプリが表示されません。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-116">App does not appear in the bottom bar of the mobile clients.</span></span> |
| <span data-ttu-id="1a5e5-117">**チャネルタブとグループ タブ**</span><span class="sxs-lookup"><span data-stu-id="1a5e5-117">**Channel and group tabs**</span></span> | <span data-ttu-id="1a5e5-118">タブは、 を使用してクライアントTeams開きます `contentUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-118">The tab opens in the Teams client using `contentUrl`.</span></span> | <span data-ttu-id="1a5e5-119">タブは、 を使用してクライアントの外部Teams開きます `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-119">The tab opens in a browser outside the Teams client using `websiteUrl`.</span></span> |

> [!NOTE]
> * <span data-ttu-id="1a5e5-120">アプリをアプリに[公開するために AppSource](https://appsource.microsoft.com)に送信Teams、モバイルの応答性が自動的に評価されます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-120">Apps submitted to the [AppSource](https://appsource.microsoft.com) for publishing on Teams are evaluated automatically for mobile responsiveness.</span></span> <span data-ttu-id="1a5e5-121">クエリの場合は、ユーザーに問い合 teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-121">For any queries, reach out to teamsubm@microsoft.com.</span></span>
> * <span data-ttu-id="1a5e5-122">AppSource を介して配布されていないすべてのアプリでは、タブは既定で Teams クライアント内のアプリ内 Web ビューで開き、個別の承認プロセスは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-122">For all apps that are not distributed through the AppSource, the tabs open in an in-app webview within the Teams clients by default and there is no separate approval process required.</span></span>
> * <span data-ttu-id="1a5e5-123">アプリの既定の動作は、アプリ ストアを通じて配布Teamsです。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-123">The default behavior of apps is only applicable if distributed through the Teams store.</span></span> <span data-ttu-id="1a5e5-124">既定では、すべてのタブがクライアントでTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-124">By default, all tabs open in the Teams client.</span></span>
> * <span data-ttu-id="1a5e5-125">モバイルに優しいアプリの評価を開始するには、アプリの詳細 teamsubm@microsoft.com 確認してください。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-125">To initiate an evaluation of your app for mobile-friendliness, reach out to teamsubm@microsoft.com with your app details.</span></span>

## <a name="authentication"></a><span data-ttu-id="1a5e5-126">認証</span><span class="sxs-lookup"><span data-stu-id="1a5e5-126">Authentication</span></span>

<span data-ttu-id="1a5e5-127">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-127">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

## <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="1a5e5-128">低帯域幅と断続的な接続</span><span class="sxs-lookup"><span data-stu-id="1a5e5-128">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="1a5e5-129">モバイル クライアントは、低帯域幅と断続的な接続で機能します。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-129">Mobile clients function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="1a5e5-130">アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-130">Your app must handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="1a5e5-131">また、進行状況インジケーターを使用して、長時間実行されるプロセスに対するフィードバックをユーザーに提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-131">You must also use progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="testing-on-mobile-clients"></a><span data-ttu-id="1a5e5-132">モバイル クライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="1a5e5-132">Testing on mobile clients</span></span>

<span data-ttu-id="1a5e5-133">さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-133">You must validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="1a5e5-134">Android デバイスの場合 [、DevTools を使用して](~/tabs/how-to/developer-tools.md) 、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-134">For Android devices, you can use [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="1a5e5-135">タブレットを含む高パフォーマンスデバイスと低パフォーマンスデバイスの両方でテストをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-135">It is recommended that you test on both high and low-performance devices, including a tablet.</span></span>

## <a name="distribution"></a><span data-ttu-id="1a5e5-136">配布</span><span class="sxs-lookup"><span data-stu-id="1a5e5-136">Distribution</span></span>

<span data-ttu-id="1a5e5-137">モバイル クライアントで適切にTeams機能するには、モバイル ストアに一覧表示されているアプリTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-137">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="1a5e5-138">タブの可用性と動作は、アプリが承認されたかどうかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-138">Tab availability and behavior depends on whether your app is approved.</span></span>

### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="1a5e5-139">モバイル用にTeamsストア上のアプリ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-139">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="1a5e5-140">次の表では、アプリがモバイル ストアに表示され、モバイルTeams承認された場合のタブの可用性と動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-140">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use:</span></span>

|<span data-ttu-id="1a5e5-141">機能</span><span class="sxs-lookup"><span data-stu-id="1a5e5-141">Capability</span></span>   |<span data-ttu-id="1a5e5-142">モバイルの可用性</span><span class="sxs-lookup"><span data-stu-id="1a5e5-142">Mobile availability?</span></span>   |<span data-ttu-id="1a5e5-143">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="1a5e5-143">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="1a5e5-144">チャネル</span><span class="sxs-lookup"><span data-stu-id="1a5e5-144">Channel</span></span> <br /> <span data-ttu-id="1a5e5-145">[グループ] タブ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-145">and group tab</span></span>|<span data-ttu-id="1a5e5-146">はい</span><span class="sxs-lookup"><span data-stu-id="1a5e5-146">Yes</span></span>|<span data-ttu-id="1a5e5-147">アプリの構成を使用Teamsモバイル クライアントのタブが開 `contentUrl` きます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-147">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="1a5e5-148">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-148">Personal app</span></span>|<span data-ttu-id="1a5e5-149">はい</span><span class="sxs-lookup"><span data-stu-id="1a5e5-149">Yes</span></span>|<span data-ttu-id="1a5e5-150">[個人用アプリ] タブの各タブが、Teamsを使用してモバイル クライアントに表示 `contentUrl` されます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-150">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="1a5e5-151">モバイルで承認Teamsアプリストアのアプリ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-151">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="1a5e5-152">次の表は、アプリがモバイル ストアに一覧表示されているが、モバイルTeams承認されていない場合のタブの可用性と動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-152">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use:</span></span>

| <span data-ttu-id="1a5e5-153">機能</span><span class="sxs-lookup"><span data-stu-id="1a5e5-153">Capability</span></span> | <span data-ttu-id="1a5e5-154">モバイルの可用性</span><span class="sxs-lookup"><span data-stu-id="1a5e5-154">Mobile availability?</span></span> | <span data-ttu-id="1a5e5-155">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="1a5e5-155">Mobile behavior</span></span> |
|----------|-----------|------------|
|<span data-ttu-id="1a5e5-156">[チャネルとグループ] タブ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-156">Channel and group tab</span></span>|<span data-ttu-id="1a5e5-157">はい</span><span class="sxs-lookup"><span data-stu-id="1a5e5-157">Yes</span></span>|<span data-ttu-id="1a5e5-158">タブは、アプリの構成を使用して Teams モバイル クライアントではなく、デバイスの既定のブラウザーで開きます。これは、ソース コードの関数にも含める `websiteUrl` 必要 `setSettings()` [があります](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-158">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration, which must also be included in your source code's `setSettings()` [function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true).</span></span> <span data-ttu-id="1a5e5-159">ただし、ユーザーは、アプリの横にある [詳細Teams] を選択し、[開く] を選択してアプリの構成をトリガーすることで、モバイル クライアントのタブを表示 `contentUrl` できます。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-159">However, users can view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="1a5e5-160">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-160">Personal app</span></span>|<span data-ttu-id="1a5e5-161">なし</span><span class="sxs-lookup"><span data-stu-id="1a5e5-161">No</span></span>|<span data-ttu-id="1a5e5-162">該当なし</span><span class="sxs-lookup"><span data-stu-id="1a5e5-162">Not applicable</span></span>|

### <a name="apps-not-on-teams-store"></a><span data-ttu-id="1a5e5-163">アプリがストアTeamsしない</span><span class="sxs-lookup"><span data-stu-id="1a5e5-163">Apps not on Teams store</span></span>

<span data-ttu-id="1a5e5-164">アプリをサイドロードする場合や、組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。</span><span class="sxs-lookup"><span data-stu-id="1a5e5-164">If you are sideloading your app or publishing to an organization's app catalog, tab behavior is the same as Teams store apps approved by Microsoft for mobile.</span></span>

## <a name="see-also"></a><span data-ttu-id="1a5e5-165">関連項目</span><span class="sxs-lookup"><span data-stu-id="1a5e5-165">See also</span></span>

* [<span data-ttu-id="1a5e5-166">タブデザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="1a5e5-166">Tab design guidelines</span></span>](~/tabs/design/tabs.md)
* [<span data-ttu-id="1a5e5-167">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="1a5e5-167">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="1a5e5-168">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="1a5e5-168">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="1a5e5-169">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="1a5e5-169">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="1a5e5-170">次の手順</span><span class="sxs-lookup"><span data-stu-id="1a5e5-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a5e5-171">タブのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="1a5e5-171">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
