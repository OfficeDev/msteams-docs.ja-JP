---
title: アプリ開発の基本の概要
author: heath-hamilton
description: Teams プラットフォーム開発の基本的な概念について説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4af23e06cbf7a3f630b77ee1693e0931c9c9c03e
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654273"
---
# <a name="microsoft-teams-app-development-fundamentals"></a><span data-ttu-id="f7032-103">Microsoft Teams アプリ開発の基本</span><span class="sxs-lookup"><span data-stu-id="f7032-103">Microsoft Teams app development fundamentals</span></span>

<span data-ttu-id="f7032-104">Microsoft Teams アプリの基本は、カスタム Teams アプリを作成するために必要な指示を示します。</span><span class="sxs-lookup"><span data-stu-id="f7032-104">Microsoft Teams app fundamentals give the direction you need to create your custom Teams app.</span></span> <span data-ttu-id="f7032-105">Teams アプリの計画に必要なフレームワークを認識できます。</span><span class="sxs-lookup"><span data-stu-id="f7032-105">You can recognize the framework required to plan your Teams app.</span></span> <span data-ttu-id="f7032-106">このドキュメントは、ユーザー アプリの通信を理解し、使用する必要があるアプリサーフェスの種類や、プロセスでアプリが必要とする可能性がある API を把握するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f7032-106">The document helps you to understand the user-app communication and figure out the kind of app surfaces you need to use or the APIs your app might require in the process.</span></span> <span data-ttu-id="f7032-107">Teams との統合時にアプリ エクスペリエンスを深める対話機能を受け入れるインスピレーションを得る。</span><span class="sxs-lookup"><span data-stu-id="f7032-107">Get some inspiration to embrace interactivity that can deepen the app experience when you integrate with Teams.</span></span>

## <a name="capabilities-and-entry-points"></a><span data-ttu-id="f7032-108">機能とエントリ ポイント</span><span class="sxs-lookup"><span data-stu-id="f7032-108">Capabilities and entry points</span></span>

<span data-ttu-id="f7032-109">Teams アプリを複数の方法で拡張できます。</span><span class="sxs-lookup"><span data-stu-id="f7032-109">You can extend your Teams app in multiple ways.</span></span> <span data-ttu-id="f7032-110">アプリを拡張するには、共同作業スペースで動作する主要な機能とエントリ ポイントを理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7032-110">To be able to extend your app you must understand all the core capabilities and the entry points that work in a collaborative space.</span></span> <span data-ttu-id="f7032-111">アプリを構築する拡張機能ポイントを試してみろ。</span><span class="sxs-lookup"><span data-stu-id="f7032-111">You can experiment with the extension points for building your apps.</span></span> <span data-ttu-id="f7032-112">重要なアプリ プロジェクト コンポーネントは、アプリ ページを正しく構成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f7032-112">Important app project components help you to correctly configure your app page.</span></span> <span data-ttu-id="f7032-113">Teams アプリには、複数[の機能とエントリ](../concepts/capabilities-overview.md)[ポイントを設定できます](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="f7032-113">Teams app can have [multiple capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span>

## <a name="understand-your-use-cases"></a><span data-ttu-id="f7032-114">ユース ケースを理解する</span><span class="sxs-lookup"><span data-stu-id="f7032-114">Understand your use cases</span></span>

<span data-ttu-id="f7032-115">ユーザーの問題を認識し、ユーザーが直面する一般的な問題に対する回答を特定できます。</span><span class="sxs-lookup"><span data-stu-id="f7032-115">You can recognize user issues and identify the answers to some common problems the users face.</span></span> <span data-ttu-id="f7032-116">ユーザーのニーズを満たす適切な組み合わせを見つけることで、Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="f7032-116">You can build your Teams app by finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="f7032-117">[使用例を理解して](../concepts/design/understand-use-cases.md) 、エンド ユーザーがアプリとやり取りする方法を知る。</span><span class="sxs-lookup"><span data-stu-id="f7032-117">[Understand use cases](../concepts/design/understand-use-cases.md) to know how an end-user interacts with your app.</span></span> <span data-ttu-id="f7032-118">ユーザーとその問題を理解する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f7032-118">You learn to understand the user and their problem.</span></span> <span data-ttu-id="f7032-119">一般的な質問の回答は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f7032-119">Some common questions answered are as follows:</span></span>

* <span data-ttu-id="f7032-120">認証が必要ですか?</span><span class="sxs-lookup"><span data-stu-id="f7032-120">Do you need authentication?</span></span>
* <span data-ttu-id="f7032-121">アプリが解決する問題は何ですか?</span><span class="sxs-lookup"><span data-stu-id="f7032-121">What problem is your app going to solve?</span></span>
* <span data-ttu-id="f7032-122">アプリのエンドユーザーは誰ですか?</span><span class="sxs-lookup"><span data-stu-id="f7032-122">Who are the end-users of the app?</span></span>
* <span data-ttu-id="f7032-123">オンボーディングエクスペリエンスの方法と、アプリが他に何を行う必要がありますか?</span><span class="sxs-lookup"><span data-stu-id="f7032-123">How should the onboarding experience be and what else the app can do?</span></span>

## <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="f7032-124">使用例を Teams アプリの機能にマップする</span><span class="sxs-lookup"><span data-stu-id="f7032-124">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="f7032-125">[使用例をマップするには、](../concepts/design/map-use-cases.md) 一般的なシナリオとアプリの機能を選択する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f7032-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span></span> <span data-ttu-id="f7032-126">アプリを共有し、外部システム内のアイテムで共同作業を行う情報が提供されます。</span><span class="sxs-lookup"><span data-stu-id="f7032-126">Information to share your app and collaborate on items in an external system is provided.</span></span> <span data-ttu-id="f7032-127">ワークフローを開始し、ユーザーに通知を送信する方法も説明します。</span><span class="sxs-lookup"><span data-stu-id="f7032-127">You can also learn how to initiate workflows and send notifications to users.</span></span> <span data-ttu-id="f7032-128">開始する場所、ユーザーとのソーシャルを取得する方法、会話型ボット、複数の機能の組み合わせに関するその他のヒントを取得します。</span><span class="sxs-lookup"><span data-stu-id="f7032-128">Get additional tips on where to start, how to get social with users, conversational bots, and combining multiple features.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7032-129">関連項目</span><span class="sxs-lookup"><span data-stu-id="f7032-129">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7032-130">Web アプリを Teams と統合する</span><span class="sxs-lookup"><span data-stu-id="f7032-130">Integrate web apps with Teams</span></span>](../samples/integrating-web-apps.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7032-131">最初の Microsoft Teams アプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="f7032-131">Build your first Microsoft Teams app</span></span>](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="f7032-132">次の手順</span><span class="sxs-lookup"><span data-stu-id="f7032-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7032-133">Teams アプリの機能について</span><span class="sxs-lookup"><span data-stu-id="f7032-133">Understand Teams app capabilities</span></span>](capabilities-overview.md)

