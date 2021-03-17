---
title: Microsoft Teams でのタブ余白の削除
author: laujan
description: タブ 余白を削除すると、開発者のエクスペリエンスが向上する方法について説明します。
keywords: タブの余白の余白の削除
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: f26701b2c432ba35ce6f069eabd3b401aae8e369
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827929"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="b42d5-104">タブ余白の変更</span><span class="sxs-lookup"><span data-stu-id="b42d5-104">Tab margin changes</span></span>

<span data-ttu-id="b42d5-105">このドキュメントでは、Microsoft Teams のすべてのタブの余白を削除すると、アプリを構築する際の開発者のエクスペリエンスが向上する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b42d5-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="b42d5-106">これは、2021 年に Microsoft Teams で導入された拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="b42d5-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="b42d5-107">すべてのタブの余白を削除すると、開発者は Teams のネイティブに見えるアプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b42d5-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="b42d5-108">これは、UI キットのデザイン [にも対応します](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="b42d5-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="b42d5-109">ほとんどのアプリは、エクスペリエンスを取り巻く余白がなくても、既に見た目が良くなります。</span><span class="sxs-lookup"><span data-stu-id="b42d5-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="b42d5-110">ただし、一部のタブは、この変更によって視覚的に影響を受け、開発者は必要な変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b42d5-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="タブの wit と余白なし" border="false":::

## <a name="timelines"></a><span data-ttu-id="b42d5-112">タイムライン</span><span class="sxs-lookup"><span data-stu-id="b42d5-112">Timelines</span></span>

* <span data-ttu-id="b42d5-113">2021 年 3 月 5 日 - パブリック Developer Preview で [余白が削除されました](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="b42d5-113">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="b42d5-114">2021 年 6 月 15 日 - 実稼働環境で余白が削除されます。</span><span class="sxs-lookup"><span data-stu-id="b42d5-114">June 15, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="b42d5-115">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="b42d5-115">Guidelines</span></span>

<span data-ttu-id="b42d5-116">タブを使用する Microsoft Teams アプリは、この変更の影響を受ける可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b42d5-116">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="b42d5-117">開発者は、タブ [の](~/resources/dev-preview/developer-preview-intro.md) 影響をDeveloper Previewし、必要な変更を行う場合は、[パブリック] に切り替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="b42d5-117">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="b42d5-118">タブ開発者は、タブを囲む余白を提供するために Teams に依存しなけらな</span><span class="sxs-lookup"><span data-stu-id="b42d5-118">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="b42d5-119">開発者は、必要なタブ デザインの周囲に余白を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b42d5-119">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="b42d5-120">実稼働環境のアプリデザインは、追加のパディング、つまり Teams によって提供される余白と、タブによって提供される余白のように見えます。ただし、余分なパディングは一時的なだけであり、数週間で離れ、アプリが提供するパディングのみを残します。</span><span class="sxs-lookup"><span data-stu-id="b42d5-120">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="b42d5-121">よくあるご質問 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="b42d5-121">FAQ</span></span>

<span data-ttu-id="b42d5-122">**ヘッダー バーやタスク バーなどのアプリクロムがデザインの端に触れても問題ないか。**</span><span class="sxs-lookup"><span data-stu-id="b42d5-122">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="b42d5-123">はい、これは問題ありません。推奨されます。</span><span class="sxs-lookup"><span data-stu-id="b42d5-123">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="b42d5-124">これは、アプリがネイティブと感じるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b42d5-124">This helps the app feel native.</span></span>

<span data-ttu-id="b42d5-125">**テキスト、ロゴ、画像などのアプリ コンテンツがデザインの左右の端に触れても問題ないか。**</span><span class="sxs-lookup"><span data-stu-id="b42d5-125">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="b42d5-126">いいえ、UI の端に触れ込むのを確認するには、すべてのアプリ コンテンツの左右に独自のパディングまたは余白を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b42d5-126">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="b42d5-127">必要に応じて、タブの上部に余白を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="b42d5-127">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="b42d5-128">**Teams が以前に適用した余白のサイズは何ですか?**</span><span class="sxs-lookup"><span data-stu-id="b42d5-128">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="b42d5-129">左右: 20px</span><span class="sxs-lookup"><span data-stu-id="b42d5-129">Left and right: 20px</span></span>
* <span data-ttu-id="b42d5-130">Top: 16px</span><span class="sxs-lookup"><span data-stu-id="b42d5-130">Top: 16px</span></span>
* <span data-ttu-id="b42d5-131">下: 0px</span><span class="sxs-lookup"><span data-stu-id="b42d5-131">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b42d5-132">すべてのタブには、個人用タブ、(グループ) チャット タブ、会議タブ、チャネル タブなど、余白が削除されています。</span><span class="sxs-lookup"><span data-stu-id="b42d5-132">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="b42d5-133">この変更をオプトインまたはオプトアウトする方法はありません。</span><span class="sxs-lookup"><span data-stu-id="b42d5-133">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="b42d5-134">すべてのタブに適用されます。</span><span class="sxs-lookup"><span data-stu-id="b42d5-134">It will apply to all tabs.</span></span>
> * <span data-ttu-id="b42d5-135">この変更は、UI を囲む余白を提供するために Microsoft Teams に依存するタブに影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b42d5-135">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
