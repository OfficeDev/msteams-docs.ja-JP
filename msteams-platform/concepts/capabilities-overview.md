---
title: アプリの機能について
author: heath-hamilton
description: Teamsアプリの機能について説明
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565152"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="e3c89-103">アプリの機能Microsoft Teams理解する</span><span class="sxs-lookup"><span data-stu-id="e3c89-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="e3c89-104">機能拡張やエントリ ポイントは、アプリがユーザーに対してマニフェストを作成する方法が異なります。</span><span class="sxs-lookup"><span data-stu-id="e3c89-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="e3c89-105">たとえば、ユーザーがキャンバス タブでアプリを操作してアクティビティを実行したり、会話型ボットを使用して同じ操作を行ったりできます。</span><span class="sxs-lookup"><span data-stu-id="e3c89-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="e3c89-106">Teams アプリの構築に使用するさまざまな機能により、その使用範囲を拡大できます。</span><span class="sxs-lookup"><span data-stu-id="e3c89-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="e3c89-107">Teams拡張する方法は複数あるので、すべてのアプリは一意です。</span><span class="sxs-lookup"><span data-stu-id="e3c89-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="e3c89-108">Webhook などの機能は 1 つしかない場合もあれば、ユーザーにさまざまなオプションを提供する機能が複数あるものもあります。</span><span class="sxs-lookup"><span data-stu-id="e3c89-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="e3c89-109">たとえば、アプリは、データを中央の場所、つまり **タブ** に表示し、会話型インターフェイス、つまり **ボット** を通じて同じ情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="e3c89-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="e3c89-110">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="e3c89-110">App capabilities</span></span>

<span data-ttu-id="e3c89-111">Teamsアプリには、次のコア機能のいずれかまたはすべてが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e3c89-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="e3c89-112">タブ</span><span class="sxs-lookup"><span data-stu-id="e3c89-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="e3c89-113">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="e3c89-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="e3c89-114">ボット</span><span class="sxs-lookup"><span data-stu-id="e3c89-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="e3c89-115">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="e3c89-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="e3c89-116">アプリは[、Teams用](/graph/teams-concept-overview)の Microsoft Graph API などの高度な機能を利用することもできます。</span><span class="sxs-lookup"><span data-stu-id="e3c89-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="e3c89-117">次の図は、アプリで必要な機能を提供する機能を示しています。</span><span class="sxs-lookup"><span data-stu-id="e3c89-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app:</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="アプリの機能Teams示すマインドマップ。":::

## <a name="always-consider-your-user"></a><span data-ttu-id="e3c89-119">常にユーザーを考慮する</span><span class="sxs-lookup"><span data-stu-id="e3c89-119">Always consider your user</span></span>

<span data-ttu-id="e3c89-120">アプリ開発に慣れTeams、その基本を理解します。</span><span class="sxs-lookup"><span data-stu-id="e3c89-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="e3c89-121">特定の機能を構築する方法が複数あることを理解しています。</span><span class="sxs-lookup"><span data-stu-id="e3c89-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="e3c89-122">このようなシナリオでは、ユーザーによりネイティブなエクスペリエンスを提供する方法を検討してください。</span><span class="sxs-lookup"><span data-stu-id="e3c89-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="e3c89-123">たとえば、アプリのタブとして作成されたフォームでユーザー入力を収集できます。</span><span class="sxs-lookup"><span data-stu-id="e3c89-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="e3c89-124">また、ビューを切り替え、ユーザーの作業フローを中断することなく、タスク モジュールを使用してこれを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="e3c89-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="e3c89-125">ユーザーの通常の作業フローからの偏差を最小限にする拡張ポイントを選択することが重要です。</span><span class="sxs-lookup"><span data-stu-id="e3c89-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="e3c89-126">関連項目</span><span class="sxs-lookup"><span data-stu-id="e3c89-126">See also</span></span>

[<span data-ttu-id="e3c89-127">Teams用のアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="e3c89-127">Build apps for Teams</span></span>](../overview.md)

## <a name="next-step"></a><span data-ttu-id="e3c89-128">次の手順</span><span class="sxs-lookup"><span data-stu-id="e3c89-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3c89-129">Teams アプリのエントリ ポイント</span><span class="sxs-lookup"><span data-stu-id="e3c89-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
