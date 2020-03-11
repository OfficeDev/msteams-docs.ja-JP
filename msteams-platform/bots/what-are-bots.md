---
title: 会話ボットとは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7bde886b67788a355181c83287d999a3bfb9727a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674746"
---
# <a name="what-are-conversational-bots"></a><span data-ttu-id="0f862-103">会話ボットとは</span><span class="sxs-lookup"><span data-stu-id="0f862-103">What are conversational bots?</span></span>

<span data-ttu-id="0f862-104">会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。</span><span class="sxs-lookup"><span data-stu-id="0f862-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="0f862-105">会話型ボットの機能は非常に柔軟性があり、単純なコマンドだけでなく、複雑で人工知能を搭載した自然言語処理の仮想アシスタントを処理できるようにスコープを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="0f862-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial intelligence powered and natural language processing virtual assistants.</span></span> <span data-ttu-id="0f862-106">大規模なアプリケーションはもちろん、スタンドアロンのものにも適用することができます。</span><span class="sxs-lookup"><span data-stu-id="0f862-106">They can be one aspect of a larger application, or completely stand alone.</span></span>

<span data-ttu-id="0f862-107">以下の GIF は、テキストと対話型カードの両方を使用して、1 対 1 のチャットのボットで会話しているユーザーを示しています。</span><span class="sxs-lookup"><span data-stu-id="0f862-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="0f862-108">カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="0f862-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="0f862-109">ボットでテキスト以上のことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="0f862-109">Don't forget, bots are much more than just text!</span></span>

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="what-tasks-are-best-handled-by-bots"></a><span data-ttu-id="0f862-111">ボットによって最適に処理されるタスク</span><span class="sxs-lookup"><span data-stu-id="0f862-111">What tasks are best handled by bots?</span></span>

<span data-ttu-id="0f862-112">Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。</span><span class="sxs-lookup"><span data-stu-id="0f862-112">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="0f862-113">各スコープに、会話ボット向けの機能と条件があります。</span><span class="sxs-lookup"><span data-stu-id="0f862-113">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="0f862-114">チャネル</span><span class="sxs-lookup"><span data-stu-id="0f862-114">In a channel</span></span>

<span data-ttu-id="0f862-115">チャネルでは、複数のユーザー間のスレッド形式の会話が扱われます。多くのユーザー同士 (現在は最大 2000) で会話が行われる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="0f862-115">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="0f862-116">これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f862-116">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="0f862-117">ただし、従来の複数ターンの対話は、うまく動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0f862-117">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="0f862-118">多くの情報を収集する必要がある場合は、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0f862-118">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="0f862-119">ボットは `@mentioned` のメッセージにのみ直接アクセスできますが、Microsoft Graph および組織レベルの引き上げられたアクセス許可を使用して、会話から追加のメッセージを取得することはできません。</span><span class="sxs-lookup"><span data-stu-id="0f862-119">Your bot will also only have access to messages where it's `@mentioned` directly, you cannot retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="0f862-120">ボットの利点をチャネル内で活用できるシナリオは以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0f862-120">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="0f862-121">**通知** (特にユーザーが追加情報を取得するための対話型カードを提供する場合)。</span><span class="sxs-lookup"><span data-stu-id="0f862-121">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="0f862-122">投票やアンケート調査などの**フィードバック シナリオ**。</span><span class="sxs-lookup"><span data-stu-id="0f862-122">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="0f862-123">**単一の要求/応答サイクル**で解決できる対話。複数のメンバーで会話をする場合にこれが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0f862-123">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="0f862-124">**交流/娯楽を目的としたボット** — 面白い猫の画像を取得したり、勝者をランダムに選んだりします。</span><span class="sxs-lookup"><span data-stu-id="0f862-124">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="0f862-125">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="0f862-125">In a group chat</span></span>

<span data-ttu-id="0f862-126">グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。</span><span class="sxs-lookup"><span data-stu-id="0f862-126">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="0f862-127">チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。</span><span class="sxs-lookup"><span data-stu-id="0f862-127">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="0f862-128">チャネルと同様に、ボットは `@mentioned` のメッセージにのみに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="0f862-128">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="0f862-129">通常、チャネルで正常に動作するシナリオは、グループ チャットでも同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="0f862-129">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="0f862-130">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="0f862-130">In a one-to-one chat</span></span>

<span data-ttu-id="0f862-131">これは、会話ボットがユーザーとやり取りする従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="0f862-131">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="0f862-132">これにより、さまざまなワークロードを実現できます。</span><span class="sxs-lookup"><span data-stu-id="0f862-132">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="0f862-133">Q&A ボット、別のシステムでワークフローを開始するボット、ジョークを言うボット、メモを取るボットなどがありますが、これらはごく一部です。</span><span class="sxs-lookup"><span data-stu-id="0f862-133">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="0f862-134">機能を表示するための方法として、会話ベースのインターフェイスが最適な方法であるかどうかを必ず検討します。</span><span class="sxs-lookup"><span data-stu-id="0f862-134">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="how-do-bots-work"></a><span data-ttu-id="0f862-135">ボットの機能</span><span class="sxs-lookup"><span data-stu-id="0f862-135">How do bots work?</span></span>

<span data-ttu-id="0f862-136">ボットは、以下の 3 つで構成されています。</span><span class="sxs-lookup"><span data-stu-id="0f862-136">Your bot consists of three pieces:</span></span>

* <span data-ttu-id="0f862-137">ホストをして、公開している Web サービス。</span><span class="sxs-lookup"><span data-stu-id="0f862-137">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="0f862-138">ボット登録 (Bot Framework にボットを登録する)。</span><span class="sxs-lookup"><span data-stu-id="0f862-138">Your bot registration that registers your bot with the Bot Framework.</span></span>
* <span data-ttu-id="0f862-139">アプリ マニフェストを含む Teams アプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="0f862-139">Your Teams app package that contains your app manifest.</span></span> <span data-ttu-id="0f862-140">これは、ユーザーがインストールし、Teams クライアントを Web サービスに接続 (Bot Service を経由してルーティング) します。</span><span class="sxs-lookup"><span data-stu-id="0f862-140">This is what your users install and connects the Teams client to your web service (routed through the Bot Service).</span></span>

<span data-ttu-id="0f862-141">Microsoft Teams のボットは、[Microsoft Bot Framework](https://dev.botframework.com/)に基づいて構築されています。</span><span class="sxs-lookup"><span data-stu-id="0f862-141">Bots for Microsoft Teams are built on the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="0f862-142">(Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0f862-142">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="0f862-143">これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。</span><span class="sxs-lookup"><span data-stu-id="0f862-143">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="0f862-144">Office 365 コネクタ カードなどの専用のカードの使用。</span><span class="sxs-lookup"><span data-stu-id="0f862-144">Using specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="0f862-145">アクティビティに関する Teams 固有のチャネル データの使用と設定。</span><span class="sxs-lookup"><span data-stu-id="0f862-145">Consuming and setting Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="0f862-146">メッセージング拡張要求の処理。</span><span class="sxs-lookup"><span data-stu-id="0f862-146">Processing messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f862-147">任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f862-147">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="0f862-148">*Teams App Studio* を使用すれば、アプリ マニフェストの作成と構成を行うことができ、Web サービスを Bot Framework のボットとして登録することができます。</span><span class="sxs-lookup"><span data-stu-id="0f862-148">*Teams App Studio* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="0f862-149">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="0f862-149">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="0f862-150">「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="0f862-150">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="0f862-151">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="0f862-151">Webhooks and connectors</span></span>

<span data-ttu-id="0f862-152">Webhook とコネクタを使用すると、ワークフローやその他の単純なコマンドの開始など、基本的なやり取りを行うためのシンプルなボットを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="0f862-152">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="0f862-153">これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。</span><span class="sxs-lookup"><span data-stu-id="0f862-153">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="0f862-154">詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="0f862-154">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="get-started"></a><span data-ttu-id="0f862-155">作業の開始</span><span class="sxs-lookup"><span data-stu-id="0f862-155">Get started</span></span>

* [<span data-ttu-id="0f862-156">C#/dotnet での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="0f862-156">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="0f862-157">JavaScript での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="0f862-157">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="0f862-158">詳細情報</span><span class="sxs-lookup"><span data-stu-id="0f862-158">Learn more</span></span>

* [<span data-ttu-id="0f862-159">Teams でのボットの基本</span><span class="sxs-lookup"><span data-stu-id="0f862-159">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)
* [<span data-ttu-id="0f862-160">Teams のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="0f862-160">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
