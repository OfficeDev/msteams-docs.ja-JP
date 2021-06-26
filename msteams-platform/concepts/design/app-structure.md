---
title: アプリを設計する - アプリの構造を理解する
description: アプリを設計する際に、アプリでカスタマイズMicrosoft Teamsを理解します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a574ebeb5416e614152bb24d52cc798f0032943c
ms.sourcegitcommit: 0fe60b3fd406a5768b18977df53d1f4c665e5300
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53133394"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="eb55b-103">アプリ構造Microsoft Teams理解する</span><span class="sxs-lookup"><span data-stu-id="eb55b-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="eb55b-104">アプリを構築する際には、アプリでカスタマイズできる機能とカスタマイズできない機能を知Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="eb55b-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="eb55b-105">この情報は、コントロールするアプリ エクスペリエンスの部分をよりよく理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="eb55b-106">次のワイヤーフレームを使用すると、次の情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-106">The following wireframes show you:</span></span>

* <span data-ttu-id="eb55b-107">各アプリ機能でカスタマイズできるTeams (ピンクで示されています)。</span><span class="sxs-lookup"><span data-stu-id="eb55b-107">The surfaces you can customize in each Teams app capability (outlined in pink).</span></span>
* <span data-ttu-id="eb55b-108">各機能がサポートするスコープ。</span><span class="sxs-lookup"><span data-stu-id="eb55b-108">The scopes each capability supports.</span></span>

> [!TIP]
> <span data-ttu-id="eb55b-109">**スコープとはどういう意味ですか?**</span><span class="sxs-lookup"><span data-stu-id="eb55b-109">**What does scope mean?**</span></span> <span data-ttu-id="eb55b-110">スコープは、ユーザーがアプリをTeamsできる領域です。</span><span class="sxs-lookup"><span data-stu-id="eb55b-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="eb55b-111">アプリには、個人、チャネル、チャット、会議など、1 つ以上のスコープを設定できます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="eb55b-112">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="eb55b-112">Personal apps</span></span>

<span data-ttu-id="eb55b-113">個人用アプリは、個々のユーザーのアプリ コンテンツをホストする大きなキャンバスを提供します。</span><span class="sxs-lookup"><span data-stu-id="eb55b-113">Personal apps provide a large canvas to host your app content for individual users.</span></span>

<span data-ttu-id="eb55b-114">\***サポートされているスコープ**: 個人用\*</span><span class="sxs-lookup"><span data-stu-id="eb55b-114">\***Supported scopes**: Personal\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="eb55b-115">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="eb55b-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="eb55b-116">キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-116">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="開発者がデスクトップ上の個人用アプリ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="eb55b-118">モバイル</span><span class="sxs-lookup"><span data-stu-id="eb55b-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="eb55b-119">キャンバスは Web ビューなので、エクスペリエンスを完全にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-119">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="開発者がモバイル上の個人用アプリ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

---

## <a name="tabs"></a><span data-ttu-id="eb55b-121">タブ</span><span class="sxs-lookup"><span data-stu-id="eb55b-121">Tabs</span></span>

<span data-ttu-id="eb55b-122">タブは、ユーザーグループのアプリ コンテンツをホストする大きなキャンバスを提供します。</span><span class="sxs-lookup"><span data-stu-id="eb55b-122">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="eb55b-123">チャネル、チャット、会議出席招待などの共有スペースにタブを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-123">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span>

<span data-ttu-id="eb55b-124">\***サポートされているスコープ**: チャネル、チャット、会議\*</span><span class="sxs-lookup"><span data-stu-id="eb55b-124">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="eb55b-125">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="eb55b-125">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="eb55b-126">キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-126">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="開発者がデスクトップ上のタブ用にカスタマイズTeamsフロントエンド領域を示す概念イメージ。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="eb55b-128">モバイル</span><span class="sxs-lookup"><span data-stu-id="eb55b-128">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="eb55b-129">キャンバスは Web ビューなので、エクスペリエンスを完全にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-129">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="開発者がモバイル上のタブ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

---

## <a name="bots"></a><span data-ttu-id="eb55b-131">ボット</span><span class="sxs-lookup"><span data-stu-id="eb55b-131">Bots</span></span>

<span data-ttu-id="eb55b-132">ボットは、ネイティブ メッセージング機能Teams統合する会話型アプリなので、UI の作業が処理されます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-132">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="eb55b-133">デザインの観点からは、自然言語処理 (NLP) サポートとアダプティブ カード プラットフォームを使用して、個性、カスタム機能、豊富で操作可能な情報を追加する機会がまだ存在します。</span><span class="sxs-lookup"><span data-stu-id="eb55b-133">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="eb55b-134">\***サポートされているスコープ**: 個人用、チャネル、チャット、会議\*</span><span class="sxs-lookup"><span data-stu-id="eb55b-134">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="eb55b-135">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="eb55b-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="開発者がデスクトップ上のボット用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="eb55b-137">モバイル</span><span class="sxs-lookup"><span data-stu-id="eb55b-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="開発者がモバイル上のボット用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

---

## <a name="messaging-extensions"></a><span data-ttu-id="eb55b-139">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eb55b-139">Messaging extensions</span></span>

<span data-ttu-id="eb55b-140">メッセージング拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作したりするためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="eb55b-140">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="eb55b-141">アクション ベースのメッセージング拡張機能を使用すると、エクスペリエンスの制御が向上しますが、Teamsベースのメッセージング拡張機能のレンダリングの多くを処理できます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-141">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="eb55b-142">\***サポートされているスコープ**: 個人用、チャネル、チャット、会議\*</span><span class="sxs-lookup"><span data-stu-id="eb55b-142">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="eb55b-143">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="eb55b-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="開発者がデスクトップ上のメッセージング拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="eb55b-145">モバイル</span><span class="sxs-lookup"><span data-stu-id="eb55b-145">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="開発者がモバイル上のメッセージング拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

---

## <a name="meeting-extensions"></a><span data-ttu-id="eb55b-147">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="eb55b-147">Meeting extensions</span></span>

<span data-ttu-id="eb55b-148">会議拡張機能は、ライブ会議を強化するアプリです。</span><span class="sxs-lookup"><span data-stu-id="eb55b-148">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="eb55b-149">会議の前、中、後など、いくつかのシナリオでアプリ コンテンツをホストできます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-149">You can host your app content in several scenarios, including before, during, and after meetings.</span></span>

<span data-ttu-id="eb55b-150">\***サポートされているスコープ**: 会議、チャット\*</span><span class="sxs-lookup"><span data-stu-id="eb55b-150">\***Supported scopes**: Meetings, Chats\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="eb55b-151">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="eb55b-151">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="eb55b-152">サーフェスは iframe であり、エクスペリエンスをカスタマイズできますが、会議中にこれらのアプリは暗いテーマを使用し、狭いという念頭に置いておきます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-152">The surface is an iframe, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme and are narrow.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="開発者がデスクトップ上の会議拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="eb55b-154">モバイル</span><span class="sxs-lookup"><span data-stu-id="eb55b-154">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="eb55b-155">サーフェスは Web ビューで、エクスペリエンスをカスタマイズできますが、会議中にこれらのアプリは暗いテーマを使用することを念頭に置いておきます。</span><span class="sxs-lookup"><span data-stu-id="eb55b-155">The surface is a webview, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="開発者がモバイルでの会議拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

---
