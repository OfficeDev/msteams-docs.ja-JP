---
title: Teams アプリの機能について
author: heath-hamilton
description: Teams の機能と拡張点の概要
ms.topic: overview
ms.author: v-heha
ms.openlocfilehash: f83cf0240b32d35028135b48e7d4c56b939777a9
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819082"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="bf065-103">Teams アプリの機能について</span><span class="sxs-lookup"><span data-stu-id="bf065-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="bf065-104">*機能* は、Microsoft Teams プラットフォームでアプリを作成するための拡張点です。</span><span class="sxs-lookup"><span data-stu-id="bf065-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="bf065-105">Teams クライアントを拡張する方法は複数ありますが、すべてのアプリが一意であるため、一部のアプリは、1つの機能 (webhook など) しか持たないため、ユーザーのオプションを提供する方法がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="bf065-105">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="bf065-106">たとえば、アプリではデータを中央の場所 (タブ) に表示し、会話インターフェイス (bot) を通じて同じ情報を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="bf065-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="bf065-107">Teams アプリには、次のコア機能のいずれかまたはすべてを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="bf065-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="bf065-108">タブ</span><span class="sxs-lookup"><span data-stu-id="bf065-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="bf065-109">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="bf065-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="bf065-110">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="bf065-110">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="bf065-111">ボット</span><span class="sxs-lookup"><span data-stu-id="bf065-111">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="bf065-112">アプリでは、 [Microsoft GRAPH REST API](../graph-api/rsc/resource-specific-consent.md)などの高度な機能を利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="bf065-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="bf065-113">アプリに必要な機能を提供する機能については、次の図を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bf065-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![Teams アプリの機能についてのマインドマップ](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="bf065-115">ユーザーにとって最適な方法</span><span class="sxs-lookup"><span data-stu-id="bf065-115">Doing what's best for your users</span></span>

<span data-ttu-id="bf065-116">Teams アプリの開発について理解すると、その微妙な違いについて理解し始められます。</span><span class="sxs-lookup"><span data-stu-id="bf065-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="bf065-117">特定の機能 (ユーザー入力の収集など) を構築する方法は複数あります。</span><span class="sxs-lookup"><span data-stu-id="bf065-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="bf065-118">たとえば、を使用して、web ベースのフォームをタブに埋め込むことができ `<iframe>` ます。</span><span class="sxs-lookup"><span data-stu-id="bf065-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="bf065-119">また、タスクモジュールである Teams の UI 規則を使用して、ユーザーが望むようによりネイティブな操作を行うことができるタブで、これを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="bf065-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="bf065-120">機能と UI の規則、コントロール、および要素の適切な組み合わせを選択することによって、最初に [対象ユーザーのユースケースを理解](../concepts/design/understand-use-cases.md)することができます。</span><span class="sxs-lookup"><span data-stu-id="bf065-120">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="bf065-121">詳細情報</span><span class="sxs-lookup"><span data-stu-id="bf065-121">Learn more</span></span>

* [<span data-ttu-id="bf065-122">アプリの計画を開始する</span><span class="sxs-lookup"><span data-stu-id="bf065-122">Start planning your app</span></span>](../concepts/extensibility-points.md)
