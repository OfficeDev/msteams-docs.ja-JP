---
title: Teams アプリの機能について
author: heath-hamilton
description: ''
ms.topic: overview
ms.author: heath-hamilton
ms.openlocfilehash: 580d75b648bde1caf0e85647c89635804c91fb70
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652092"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="47389-102">Teams アプリの機能について</span><span class="sxs-lookup"><span data-stu-id="47389-102">Understanding Teams app capabilities</span></span>

<span data-ttu-id="47389-103">*機能* は、Microsoft Teams プラットフォームでアプリを作成するための拡張点です。</span><span class="sxs-lookup"><span data-stu-id="47389-103">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="47389-104">Teams クライアントを拡張する方法は複数ありますが、すべてのアプリが一意であるため、一部のアプリは、1つの機能 (webhook など) しか持たないため、ユーザーのオプションを提供する方法がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="47389-104">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="47389-105">たとえば、アプリではデータを中央の場所 (タブ) に表示し、会話インターフェイス (bot) を通じて同じ情報を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="47389-105">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="47389-106">Teams アプリには、次のコア機能のいずれかまたはすべてを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="47389-106">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="47389-107">タブ</span><span class="sxs-lookup"><span data-stu-id="47389-107">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="47389-108">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="47389-108">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="47389-109">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="47389-109">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="47389-110">ボット</span><span class="sxs-lookup"><span data-stu-id="47389-110">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="47389-111">アプリでは、 [Microsoft GRAPH REST API](../graph-api/rsc/resource-specific-consent.md)などの高度な機能を利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="47389-111">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="47389-112">アプリに必要な機能を提供する機能については、次の図を参照してください。</span><span class="sxs-lookup"><span data-stu-id="47389-112">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![Teams アプリの機能についてのマインドマップ](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="47389-114">ユーザーにとって最適な方法</span><span class="sxs-lookup"><span data-stu-id="47389-114">Doing what's best for your users</span></span>

<span data-ttu-id="47389-115">Teams アプリの開発について理解すると、その微妙な違いについて理解し始められます。</span><span class="sxs-lookup"><span data-stu-id="47389-115">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="47389-116">特定の機能 (ユーザー入力の収集など) を構築する方法は複数あります。</span><span class="sxs-lookup"><span data-stu-id="47389-116">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="47389-117">たとえば、を使用して、web ベースのフォームをタブに埋め込むことができ `<iframe>` ます。</span><span class="sxs-lookup"><span data-stu-id="47389-117">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="47389-118">また、タスクモジュールである Teams の UI 規則を使用して、ユーザーが望むようによりネイティブな操作を行うことができるタブで、これを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="47389-118">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="47389-119">機能と UI の規則、コントロール、および要素の適切な組み合わせを選択することによって、最初に [対象ユーザーのユースケースを理解](../concepts/design/understand-use-cases.md)することができます。</span><span class="sxs-lookup"><span data-stu-id="47389-119">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="47389-120">詳細情報</span><span class="sxs-lookup"><span data-stu-id="47389-120">Learn more</span></span>

* [<span data-ttu-id="47389-121">アプリの計画を開始する</span><span class="sxs-lookup"><span data-stu-id="47389-121">Start planning your app</span></span>](../concepts/extensibility-points.md)
