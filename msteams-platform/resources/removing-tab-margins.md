---
title: タブの余白を削除Microsoft Teams
author: laujan
description: タブ 余白を削除すると、開発者のエクスペリエンスが向上する方法について説明します。
keywords: タブの余白の余白の削除
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 78d97dca73e7fce2bf4b911f5ea4588525667378
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019714"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="51cd7-104">タブ余白の変更</span><span class="sxs-lookup"><span data-stu-id="51cd7-104">Tab margin changes</span></span>

<span data-ttu-id="51cd7-105">このドキュメントでは、アプリを構築する際に、Microsoft Teamsタブの余白を削除すると、開発者のエクスペリエンスが向上する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="51cd7-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="51cd7-106">これは、2021 年にMicrosoft Teams拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="51cd7-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="51cd7-107">すべてのタブの余白を削除すると、開発者はアプリのネイティブに見えるアプリをTeams。</span><span class="sxs-lookup"><span data-stu-id="51cd7-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="51cd7-108">これは、UI キットのデザイン [にも対応します](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="51cd7-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="51cd7-109">ほとんどのアプリは、エクスペリエンスを取り巻く余白がなくても、既に見た目が良くなります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="51cd7-110">ただし、一部のタブは、この変更によって視覚的に影響を受け、開発者は必要な変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="タブの wit と余白なし" border="false":::

> [!NOTE]
> <span data-ttu-id="51cd7-112">モバイル クライアントで表示されるタブに余白が含まれるので、この機能はモバイル クライアントには適用されません。</span><span class="sxs-lookup"><span data-stu-id="51cd7-112">This feature is not applicable to mobile clients, as the tabs viewed in the mobile clients do not have margins.</span></span> 

## <a name="timelines"></a><span data-ttu-id="51cd7-113">タイムライン</span><span class="sxs-lookup"><span data-stu-id="51cd7-113">Timelines</span></span>

* <span data-ttu-id="51cd7-114">2021 年 3 月 5 日 - パブリック Developer Preview で [余白が削除されました](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="51cd7-114">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="51cd7-115">2021 年 6 月 15 日 - 実稼働環境で余白が削除されます。</span><span class="sxs-lookup"><span data-stu-id="51cd7-115">June 15, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="51cd7-116">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="51cd7-116">Guidelines</span></span>

<span data-ttu-id="51cd7-117">Microsoft Teamsを使用するアプリは、この変更の影響を受ける可能性があります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-117">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="51cd7-118">開発者は、タブ [の](~/resources/dev-preview/developer-preview-intro.md) 影響をDeveloper Previewし、必要な変更を行う場合は、[パブリック] に切り替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-118">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="51cd7-119">タブ開発者は、タブの周囲に余白Teamsを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-119">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="51cd7-120">開発者は、必要なタブ デザインの周囲に余白を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-120">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="51cd7-121">実稼働環境のアプリデザインは、追加のパディング、つまり、タブによって提供される余白Teams余白のように見えます。ただし、余分なパディングは一時的なだけであり、数週間で離れ、アプリが提供するパディングのみを残します。</span><span class="sxs-lookup"><span data-stu-id="51cd7-121">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="51cd7-122">よくあるご質問 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="51cd7-122">FAQ</span></span>

<span data-ttu-id="51cd7-123">**ヘッダー バーやタスク バーなどのアプリクロムがデザインの端に触れても問題ないか。**</span><span class="sxs-lookup"><span data-stu-id="51cd7-123">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="51cd7-124">はい、これは問題ありません。推奨されます。</span><span class="sxs-lookup"><span data-stu-id="51cd7-124">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="51cd7-125">これは、アプリがネイティブと感じるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="51cd7-125">This helps the app feel native.</span></span>

<span data-ttu-id="51cd7-126">**テキスト、ロゴ、画像などのアプリ コンテンツがデザインの左右の端に触れても問題ないか。**</span><span class="sxs-lookup"><span data-stu-id="51cd7-126">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="51cd7-127">いいえ、UI の端に触れ込むのを確認するには、すべてのアプリ コンテンツの左右に独自のパディングまたは余白を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-127">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="51cd7-128">必要に応じて、タブの上部に余白を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="51cd7-128">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="51cd7-129">**以前に適用した余白のTeamsは何ですか?**</span><span class="sxs-lookup"><span data-stu-id="51cd7-129">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="51cd7-130">左右: 20px</span><span class="sxs-lookup"><span data-stu-id="51cd7-130">Left and right: 20px</span></span>
* <span data-ttu-id="51cd7-131">Top: 16px</span><span class="sxs-lookup"><span data-stu-id="51cd7-131">Top: 16px</span></span>
* <span data-ttu-id="51cd7-132">下: 0px</span><span class="sxs-lookup"><span data-stu-id="51cd7-132">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="51cd7-133">すべてのタブには、個人用タブ、(グループ) チャット タブ、会議タブ、チャネル タブなど、余白が削除されています。</span><span class="sxs-lookup"><span data-stu-id="51cd7-133">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="51cd7-134">この変更をオプトインまたはオプトアウトする方法はありません。</span><span class="sxs-lookup"><span data-stu-id="51cd7-134">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="51cd7-135">すべてのタブに適用されます。</span><span class="sxs-lookup"><span data-stu-id="51cd7-135">It will apply to all tabs.</span></span>
> * <span data-ttu-id="51cd7-136">この変更は、UI を囲む余白Microsoft Teamsに依存するタブに影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="51cd7-136">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
