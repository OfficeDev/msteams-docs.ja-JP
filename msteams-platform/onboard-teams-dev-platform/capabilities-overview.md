---
title: Teams アプリの機能について
author: heath-hamilton
description: Teams プラットフォーム機能の概要。 Teams アプリを構築するための拡張点です。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 9bb94d2cfd5c30b2245c5ccf580d374972315e72
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964565"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="c0178-103">Teams アプリの機能について</span><span class="sxs-lookup"><span data-stu-id="c0178-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="c0178-104">*機能* は、Microsoft Teams プラットフォームでアプリを作成するための拡張点です。</span><span class="sxs-lookup"><span data-stu-id="c0178-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="c0178-105">Teams クライアントを拡張する方法は複数ありますが、すべてのアプリが一意であるため、一部のアプリは、1つの機能 (webhook など) しか持たないため、ユーザーのオプションを提供する方法がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="c0178-105">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="c0178-106">たとえば、アプリではデータを中央の場所 (タブ) に表示し、会話インターフェイス (bot) を通じて同じ情報を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="c0178-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="c0178-107">Teams アプリには、次のコア機能のいずれかまたはすべてを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c0178-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="c0178-108">タブ</span><span class="sxs-lookup"><span data-stu-id="c0178-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="c0178-109">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c0178-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="c0178-110">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="c0178-110">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="c0178-111">ボット</span><span class="sxs-lookup"><span data-stu-id="c0178-111">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="c0178-112">アプリでは、 [Microsoft GRAPH REST API](../graph-api/rsc/resource-specific-consent.md)などの高度な機能を利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="c0178-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="c0178-113">アプリに必要な機能を提供する機能については、次の図を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c0178-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![Teams アプリの機能についてのマインドマップ](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="c0178-115">ユーザーにとって最適な方法</span><span class="sxs-lookup"><span data-stu-id="c0178-115">Doing what's best for your users</span></span>

<span data-ttu-id="c0178-116">Teams アプリの開発について理解すると、その微妙な違いについて理解し始められます。</span><span class="sxs-lookup"><span data-stu-id="c0178-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="c0178-117">特定の機能 (ユーザー入力の収集など) を構築する方法は複数あります。</span><span class="sxs-lookup"><span data-stu-id="c0178-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="c0178-118">たとえば、を使用して、web ベースのフォームをタブに埋め込むことができ `<iframe>` ます。</span><span class="sxs-lookup"><span data-stu-id="c0178-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="c0178-119">また、タスクモジュールである Teams の UI 規則を使用して、ユーザーが望むようによりネイティブな操作を行うことができるタブで、これを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="c0178-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="c0178-120">機能と UI の規則、コントロール、および要素の適切な組み合わせを選択することによって、最初に [対象ユーザーのユースケースを理解](../concepts/design/understand-use-cases.md)することができます。</span><span class="sxs-lookup"><span data-stu-id="c0178-120">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="c0178-121">詳細情報</span><span class="sxs-lookup"><span data-stu-id="c0178-121">Learn more</span></span>

* [<span data-ttu-id="c0178-122">アプリの計画を開始する</span><span class="sxs-lookup"><span data-stu-id="c0178-122">Start planning your app</span></span>](../concepts/extensibility-points.md)
