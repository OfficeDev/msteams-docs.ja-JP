---
title: アプリを設計する - アプリの構造を理解する
description: アプリを設計する際に、アプリでカスタマイズMicrosoft Teamsを理解します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631389"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="721e2-103">アプリ構造Microsoft Teams理解する</span><span class="sxs-lookup"><span data-stu-id="721e2-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="721e2-104">アプリを構築する際には、アプリでカスタマイズできる機能とカスタマイズできない機能を知Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="721e2-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="721e2-105">この情報は、コントロールするアプリ エクスペリエンスの部分をよりよく理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="721e2-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="721e2-106">次のワイヤーフレームを使用すると、次の情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="721e2-106">The following wireframes show you:</span></span>

* <span data-ttu-id="721e2-107">各アプリ機能でカスタマイズできるTeams (青で示されています)。</span><span class="sxs-lookup"><span data-stu-id="721e2-107">The surfaces you can customize in each Teams app capability (outlined in blue).</span></span>
* <span data-ttu-id="721e2-108">各機能がサポートするスコープ。</span><span class="sxs-lookup"><span data-stu-id="721e2-108">The scopes each capability supports.</span></span>

> [!NOTE]
> <span data-ttu-id="721e2-109">**スコープとはどういう意味ですか?**</span><span class="sxs-lookup"><span data-stu-id="721e2-109">**What does scope mean?**</span></span> <span data-ttu-id="721e2-110">スコープは、ユーザーがアプリをTeamsできる領域です。</span><span class="sxs-lookup"><span data-stu-id="721e2-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="721e2-111">アプリには、個人、チャネル、チャット、会議など、1 つ以上のスコープを設定できます。</span><span class="sxs-lookup"><span data-stu-id="721e2-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="721e2-112">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="721e2-112">Personal apps</span></span>

<span data-ttu-id="721e2-113">個人用アプリは、個々のユーザーのアプリ コンテンツをホストする大きなキャンバスを提供します。</span><span class="sxs-lookup"><span data-stu-id="721e2-113">Personal apps provide a large canvas to host your app content for individual users.</span></span> <span data-ttu-id="721e2-114">キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="721e2-114">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="721e2-115">\***サポートされているスコープ**: 個人用\*</span><span class="sxs-lookup"><span data-stu-id="721e2-115">\***Supported scopes**: Personal\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="開発者が個人用アプリ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

## <a name="tabs"></a><span data-ttu-id="721e2-117">タブ</span><span class="sxs-lookup"><span data-stu-id="721e2-117">Tabs</span></span>

<span data-ttu-id="721e2-118">タブは、ユーザーグループのアプリ コンテンツをホストする大きなキャンバスを提供します。</span><span class="sxs-lookup"><span data-stu-id="721e2-118">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="721e2-119">チャネル、チャット、会議出席招待などの共有スペースにタブを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="721e2-119">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span> <span data-ttu-id="721e2-120">キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="721e2-120">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="721e2-121">\***サポートされているスコープ**: チャネル、チャット、会議\*</span><span class="sxs-lookup"><span data-stu-id="721e2-121">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="開発者がタブ用にカスタマイズできるTeamsフロントエンド領域を示す概念図。" border="false":::

## <a name="bots"></a><span data-ttu-id="721e2-123">ボット</span><span class="sxs-lookup"><span data-stu-id="721e2-123">Bots</span></span>

<span data-ttu-id="721e2-124">ボットは、ネイティブ メッセージング機能Teams統合する会話型アプリなので、UI の作業が処理されます。</span><span class="sxs-lookup"><span data-stu-id="721e2-124">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="721e2-125">デザインの観点からは、自然言語処理 (NLP) サポートとアダプティブ カード プラットフォームを使用して、個性、カスタム機能、豊富で操作可能な情報を追加する機会がまだ存在します。</span><span class="sxs-lookup"><span data-stu-id="721e2-125">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="721e2-126">\***サポートされているスコープ**: 個人用、チャネル、チャット、会議\*</span><span class="sxs-lookup"><span data-stu-id="721e2-126">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="開発者がボット用にカスタマイズできるTeamsフロントエンド領域を示す概念イメージ。" border="false":::

## <a name="messaging-extensions"></a><span data-ttu-id="721e2-128">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="721e2-128">Messaging extensions</span></span>

<span data-ttu-id="721e2-129">メッセージング拡張機能は、アプリコンテンツを挿入したり、会話から離れることなくメッセージに作用するためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="721e2-129">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="721e2-130">アクション ベースのメッセージング拡張機能を使用すると、エクスペリエンスの制御が向上しますが、Teamsベースのメッセージング拡張機能のレンダリングの多くを処理できます。</span><span class="sxs-lookup"><span data-stu-id="721e2-130">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="721e2-131">\***サポートされているスコープ**: 個人用、チャネル、チャット、会議\*</span><span class="sxs-lookup"><span data-stu-id="721e2-131">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="開発者がメッセージング拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

## <a name="meeting-extensions"></a><span data-ttu-id="721e2-133">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="721e2-133">Meeting extensions</span></span>

<span data-ttu-id="721e2-134">会議拡張機能は、ライブ会議を強化するアプリです。</span><span class="sxs-lookup"><span data-stu-id="721e2-134">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="721e2-135">会議の前、中、後など、いくつかのシナリオでアプリ コンテンツをホストできます。</span><span class="sxs-lookup"><span data-stu-id="721e2-135">You can host your app content in several scenarios, including before, during, and after meetings.</span></span> <span data-ttu-id="721e2-136">サーフェスは iframe であり、エクスペリエンスをカスタマイズできますが、これらのアプリは暗いテーマで、会議中は狭くなります。</span><span class="sxs-lookup"><span data-stu-id="721e2-136">The surface is an iframe, allowing you to customize the experience, but keep in mind that these apps are dark themed and narrow during meetings.</span></span>

<span data-ttu-id="721e2-137">\***サポートされているスコープ**: 会議、チャット\*</span><span class="sxs-lookup"><span data-stu-id="721e2-137">\***Supported scopes**: Meetings, Chats\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="開発者が会議の拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::
