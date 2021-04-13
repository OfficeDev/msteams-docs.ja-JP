---
title: アプリの機能を理解する
author: heath-hamilton
description: Teams アプリの機能の説明
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6d08d06c55aed4b531fba4bb533c896c13073cfc
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654434"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="2f86d-103">Microsoft Teams アプリの機能について</span><span class="sxs-lookup"><span data-stu-id="2f86d-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="2f86d-104">機能拡張またはエントリ ポイントは、アプリがユーザーに表示されるさまざまな方法です。</span><span class="sxs-lookup"><span data-stu-id="2f86d-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="2f86d-105">たとえば、ユーザーはキャンバス タブでアプリを操作してアクティビティを実行したり、会話型ボットを使用して同じ操作を行う場合があります。</span><span class="sxs-lookup"><span data-stu-id="2f86d-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="2f86d-106">Teams アプリの構築に使用されるさまざまな機能を使用すると、使用範囲を拡大できます。</span><span class="sxs-lookup"><span data-stu-id="2f86d-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="2f86d-107">Teams を拡張する方法は複数あるので、すべてのアプリは一意です。</span><span class="sxs-lookup"><span data-stu-id="2f86d-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="2f86d-108">Webhook などの機能は 1 つのみ、ユーザーにさまざまなオプションを提供する複数の機能を備える機能もあります。</span><span class="sxs-lookup"><span data-stu-id="2f86d-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="2f86d-109">たとえば、アプリは、データを中央の場所 (タブ) に表示し、会話インターフェイス (ボット) を介して同じ情報を表示 **できます**。</span><span class="sxs-lookup"><span data-stu-id="2f86d-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="2f86d-110">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="2f86d-110">App capabilities</span></span>

<span data-ttu-id="2f86d-111">Teams アプリには、次のコア機能の 1 つまたはすべてが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2f86d-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="2f86d-112">タブ</span><span class="sxs-lookup"><span data-stu-id="2f86d-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="2f86d-113">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="2f86d-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="2f86d-114">ボット</span><span class="sxs-lookup"><span data-stu-id="2f86d-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="2f86d-115">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="2f86d-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="2f86d-116">アプリでは、Microsoft Graph API for Teams などの高度な [機能を利用することもできます](https://docs.microsoft.com/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="2f86d-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="2f86d-117">次の図は、アプリで必要な機能を提供する機能を示しています。</span><span class="sxs-lookup"><span data-stu-id="2f86d-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Teams アプリの機能を示すマインド マップ。":::

## <a name="always-consider-your-user"></a><span data-ttu-id="2f86d-119">ユーザーを常に考慮する</span><span class="sxs-lookup"><span data-stu-id="2f86d-119">Always consider your user</span></span>

<span data-ttu-id="2f86d-120">Teams アプリの開発に慣れ親しんだら、その基本的な基本を理解できます。</span><span class="sxs-lookup"><span data-stu-id="2f86d-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="2f86d-121">特定の機能を構築する方法は複数あると理解しています。</span><span class="sxs-lookup"><span data-stu-id="2f86d-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="2f86d-122">このようなシナリオでは、ユーザーによりネイティブなエクスペリエンスを提供する方法を検討してください。</span><span class="sxs-lookup"><span data-stu-id="2f86d-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="2f86d-123">たとえば、アプリ内のタブとして構築されたフォームでユーザー入力を収集できます。</span><span class="sxs-lookup"><span data-stu-id="2f86d-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="2f86d-124">また、ビューを切り替え、ユーザーの作業フローを中断することなく、タスク モジュールを使用してこれを実行できます。</span><span class="sxs-lookup"><span data-stu-id="2f86d-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="2f86d-125">ユーザーの通常の作業フローから最も逸脱しない拡張ポイントを選択することが重要です。</span><span class="sxs-lookup"><span data-stu-id="2f86d-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="2f86d-126">関連項目</span><span class="sxs-lookup"><span data-stu-id="2f86d-126">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f86d-127">Teams 用アプリのビルド</span><span class="sxs-lookup"><span data-stu-id="2f86d-127">Build apps for Teams</span></span>](../overview.md)
## <a name="next-step"></a><span data-ttu-id="2f86d-128">次の手順</span><span class="sxs-lookup"><span data-stu-id="2f86d-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f86d-129">Teams アプリのエントリ ポイント</span><span class="sxs-lookup"><span data-stu-id="2f86d-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
