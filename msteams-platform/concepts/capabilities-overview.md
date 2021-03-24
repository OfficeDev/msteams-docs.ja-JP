---
title: Teams アプリの機能について
author: heath-hamilton
description: Teams アプリの機能の説明
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034706"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="532ee-103">Teams アプリの機能について</span><span class="sxs-lookup"><span data-stu-id="532ee-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="532ee-104">*機能は* 、Microsoft Teams プラットフォームでアプリを構築する拡張ポイントです。</span><span class="sxs-lookup"><span data-stu-id="532ee-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="532ee-105">Teams を拡張する方法は複数あるので、すべてのアプリは一意です。一部のアプリには 1 つの機能 (webhook など) しか持てない場合と、ユーザーにオプションを提供する機能がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="532ee-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="532ee-106">たとえば、アプリは中央の場所 (タブ) にデータを表示し、会話インターフェイス (ボット) を通じて同じ情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="532ee-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="532ee-107">Teams アプリには、次のコア機能の 1 つまたはすべてが含まれます。</span><span class="sxs-lookup"><span data-stu-id="532ee-107">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="532ee-108">タブ</span><span class="sxs-lookup"><span data-stu-id="532ee-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="532ee-109">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="532ee-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="532ee-110">ボット</span><span class="sxs-lookup"><span data-stu-id="532ee-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="532ee-111">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="532ee-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="532ee-112">アプリでは、Microsoft Graph API for Teams などの高度な [機能を利用することもできます](https://docs.microsoft.com/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="532ee-112">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="532ee-113">アプリで必要な機能を提供する機能を確認するには、次の図を参照してください。</span><span class="sxs-lookup"><span data-stu-id="532ee-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Teams アプリの機能を示すマインド マップ。":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="532ee-115">ユーザーに最適な機能を実行する</span><span class="sxs-lookup"><span data-stu-id="532ee-115">Doing what's best for your users</span></span>

<span data-ttu-id="532ee-116">Teams アプリの開発に慣れ親しんだら、その微妙な点を理解し始めるでしょう。</span><span class="sxs-lookup"><span data-stu-id="532ee-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="532ee-117">特定の機能 (ユーザー入力の収集など) を作成する方法は複数ある。</span><span class="sxs-lookup"><span data-stu-id="532ee-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="532ee-118">たとえば、Web ベースのフォームをタブに埋め込むには、 を使用します `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="532ee-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="532ee-119">また、ユーザーが優先するよりネイティブなエクスペリエンスを得る場合は、タスク モジュールである Teams UI 規則を使用してタブでこれを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="532ee-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="532ee-120">適切な機能と設計を選ぶには、まず対象ユーザーの使用例 [を理解する必要があります](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="532ee-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
