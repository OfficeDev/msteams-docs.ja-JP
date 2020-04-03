---
title: 会話ボットとは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 132b71a4da7462c426468c7fc2f79b26b6fbb03b
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120291"
---
# <a name="what-are-conversational-bots"></a><span data-ttu-id="28587-103">会話ボットとは</span><span class="sxs-lookup"><span data-stu-id="28587-103">What are conversational bots?</span></span>

<span data-ttu-id="28587-104">会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。</span><span class="sxs-lookup"><span data-stu-id="28587-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="28587-105">会話型ボットの機能は非常に柔軟性があり、単純なコマンドだけでなく、複雑で人工知能を搭載した自然言語処理の仮想アシスタントを処理できるようにスコープを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="28587-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial-intelligence-powered and natural-language-processing virtual assistants.</span></span> <span data-ttu-id="28587-106">大規模なアプリケーションはもちろん、スタンドアロンのものにも適用することができます。</span><span class="sxs-lookup"><span data-stu-id="28587-106">They can be one aspect of a larger application, or completely stand-alone.</span></span>

<span data-ttu-id="28587-107">以下の GIF は、テキストと対話型カードの両方を使用して、1 対 1 のチャットのボットで会話しているユーザーを示しています。</span><span class="sxs-lookup"><span data-stu-id="28587-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="28587-108">カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="28587-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="28587-109">ボットでテキスト以上のことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="28587-109">Don't forget, bots are much more than just text!</span></span>

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="how-bots-work"></a><span data-ttu-id="28587-111">ボットの機能</span><span class="sxs-lookup"><span data-stu-id="28587-111">How bots work</span></span>

<span data-ttu-id="28587-112">Teams ボットは次の 3 つ要素で構成されています。</span><span class="sxs-lookup"><span data-stu-id="28587-112">Your Teams bot consists of three elements:</span></span>

* <span data-ttu-id="28587-113">お客様がホストし、公開している Web サービス。</span><span class="sxs-lookup"><span data-stu-id="28587-113">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="28587-114">Bot Framework へのボットの登録。</span><span class="sxs-lookup"><span data-stu-id="28587-114">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="28587-115">アプリ マニフェストを含む Teams アプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="28587-115">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="28587-116">これは、ユーザーがインストールするもので、Bot Service 経由でルーティングされ、Teams クライアントをお客様の Web サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="28587-116">This is what your users will install and connects the Teams client to your web service, routed through the Bot Service.</span></span>

<span data-ttu-id="28587-117">Microsoft Teams のボットは、[Microsoft Bot Framework](https://dev.botframework.com/) に基づいて構築されています。</span><span class="sxs-lookup"><span data-stu-id="28587-117">Bots for Microsoft Teams are built on the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="28587-118">Bot Framework に基づくボットが既にある場合は、簡単な操作でそのボットを Microsoft Teams で動作するように適応させることができます。</span><span class="sxs-lookup"><span data-stu-id="28587-118">If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.</span></span> <span data-ttu-id="28587-119">用意されている [SDK](/microsoftteams/platform/#pivot=sdk-tools) を活用するため、C# か Node.js を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="28587-119">We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="28587-120">これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。</span><span class="sxs-lookup"><span data-stu-id="28587-120">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="28587-121">Office 365 コネクタ カードなどの専用のカードを使用する。</span><span class="sxs-lookup"><span data-stu-id="28587-121">Use specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="28587-122">アクティビティに関する Teams 固有のチャネル データを使用して設定する。</span><span class="sxs-lookup"><span data-stu-id="28587-122">Consume and set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="28587-123">メッセージング拡張要求を処理する。</span><span class="sxs-lookup"><span data-stu-id="28587-123">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28587-124">任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="28587-124">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

> [!TIP]
> <span data-ttu-id="28587-125">Teams App Studio を使用すると、アプリ マニフェストを作成して構成でき、Web サービスを Bot Framework のボットとして登録できます。</span><span class="sxs-lookup"><span data-stu-id="28587-125">Teams App Studio\* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="28587-126">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="28587-126">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="28587-127">「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="28587-127">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="28587-128">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="28587-128">Webhooks and connectors</span></span>

<span data-ttu-id="28587-129">Webhook とコネクタを使用すると、ワークフローやその他の単純なコマンドの開始など、基本的なやり取りを行うためのシンプルなボットを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="28587-129">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="28587-130">これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。</span><span class="sxs-lookup"><span data-stu-id="28587-130">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="28587-131">詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="28587-131">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="where-bots-work-best"></a><span data-ttu-id="28587-132">ボットが最適に動作するケース</span><span class="sxs-lookup"><span data-stu-id="28587-132">Where bots work best</span></span>

<span data-ttu-id="28587-133">Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。</span><span class="sxs-lookup"><span data-stu-id="28587-133">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="28587-134">各スコープに、会話ボット向けの機能と条件があります。</span><span class="sxs-lookup"><span data-stu-id="28587-134">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="28587-135">チャネル</span><span class="sxs-lookup"><span data-stu-id="28587-135">In a channel</span></span>

<span data-ttu-id="28587-136">チャネルでは、複数のユーザー間のスレッド形式の会話が扱われます。多くのユーザー同士 (現在は最大 2000) で会話が行われる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="28587-136">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="28587-137">これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="28587-137">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="28587-138">ただし、従来の複数ターンの対話は、うまく動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="28587-138">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="28587-139">多くの情報を収集する必要がある場合は、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="28587-139">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="28587-140">ボットは `@mentioned` のメッセージにのみ直接アクセスできますが、Microsoft Graph および組織レベルの引き上げられたアクセス許可を使用して、会話から追加のメッセージを取得することはできません。</span><span class="sxs-lookup"><span data-stu-id="28587-140">Your bot will also only have access to messages where it's `@mentioned` directly, you cannot retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="28587-141">ボットの利点をチャネル内で活用できるシナリオは以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="28587-141">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="28587-142">**通知** (特にユーザーが追加情報を取得するための対話型カードを提供する場合)。</span><span class="sxs-lookup"><span data-stu-id="28587-142">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="28587-143">投票やアンケート調査などの**フィードバック シナリオ**。</span><span class="sxs-lookup"><span data-stu-id="28587-143">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="28587-144">**単一の要求/応答サイクル**で解決できる対話。複数のメンバーで会話をする場合にこれが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="28587-144">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="28587-145">**交流/娯楽を目的としたボット** — 面白い猫の画像を取得したり、勝者をランダムに選んだりします。</span><span class="sxs-lookup"><span data-stu-id="28587-145">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="28587-146">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="28587-146">In a group chat</span></span>

<span data-ttu-id="28587-147">グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。</span><span class="sxs-lookup"><span data-stu-id="28587-147">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="28587-148">チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。</span><span class="sxs-lookup"><span data-stu-id="28587-148">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="28587-149">チャネルと同様に、ボットは `@mentioned` のメッセージにのみに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="28587-149">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="28587-150">通常、チャネルで正常に動作するシナリオは、グループ チャットでも同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="28587-150">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="28587-151">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="28587-151">In a one-to-one chat</span></span>

<span data-ttu-id="28587-152">これは、会話ボットがユーザーとやり取りする従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="28587-152">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="28587-153">これにより、さまざまなワークロードを実現できます。</span><span class="sxs-lookup"><span data-stu-id="28587-153">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="28587-154">Q&A ボット、別のシステムでワークフローを開始するボット、ジョークを言うボット、メモを取るボットなどがありますが、これらはごく一部です。</span><span class="sxs-lookup"><span data-stu-id="28587-154">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="28587-155">機能を表示するための方法として、会話ベースのインターフェイスが最適な方法であるかどうかを必ず検討します。</span><span class="sxs-lookup"><span data-stu-id="28587-155">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="bot-fails"></a><span data-ttu-id="28587-156">ボットが不適切なケース</span><span class="sxs-lookup"><span data-stu-id="28587-156">Bot fails</span></span>

### <a name="having-multi-turn-experiences-in-chat"></a><span data-ttu-id="28587-157">チャットで複数回やり取りが交わされる場合</span><span class="sxs-lookup"><span data-stu-id="28587-157">Having multi-turn experiences in chat</span></span>

<span data-ttu-id="28587-158">ボットとユーザーが対話を長く続けると、タスクの完了に要する時間が長くなり、必要以上に複雑になります。また、開発者は状態を維持することが必要になります。</span><span class="sxs-lookup"><span data-stu-id="28587-158">An extensive dialog between your bot and the user is a slow and overly complex way to get a task completed and it also requires the developer to maintain state.</span></span> <span data-ttu-id="28587-159">このような状態を終了するには、ユーザーはタイムアウトするか、「*Cancel*」と入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="28587-159">To exit this state a user must either time-out or type “*Cancel*”.</span></span> <span data-ttu-id="28587-160">何より、この処理は不必要なほど長々しいものになります。</span><span class="sxs-lookup"><span data-stu-id="28587-160">Above all, the process is unnecessarily tedious:</span></span>

<span data-ttu-id="28587-161">ユーザー: Megan との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="28587-161">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="28587-162">ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。</span><span class="sxs-lookup"><span data-stu-id="28587-162">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="28587-163">ユーザー: Megan Bowen との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="28587-163">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="28587-164">ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?</span><span class="sxs-lookup"><span data-stu-id="28587-164">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="28587-165">ユーザー: 午後 1 時に。</span><span class="sxs-lookup"><span data-stu-id="28587-165">USER: 1:00 pm.</span></span>

<span data-ttu-id="28587-166">ボット: 何日のですか?</span><span class="sxs-lookup"><span data-stu-id="28587-166">BOT: On which day?</span></span>

### <a name="supporting-too-many-commands"></a><span data-ttu-id="28587-167">サポートすべきコマンドが多すぎる場合</span><span class="sxs-lookup"><span data-stu-id="28587-167">Supporting too many commands</span></span>

<span data-ttu-id="28587-168">サポートするコマンドがあまりに多く、特に広範な種類に及ぶボットは、うまく機能しないことや、ユーザーからの評価が低くなる傾向があります。</span><span class="sxs-lookup"><span data-stu-id="28587-168">A bot that supports excessive commands, especially a broad range of commands, will not be successful or viewed positively by users.</span></span> <span data-ttu-id="28587-169">現在のボット メニューにはコマンドが 6 つしか表示されないため、それ以外のコマンドは滅多に使用されなくなります。</span><span class="sxs-lookup"><span data-stu-id="28587-169">Since there are only 6 visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="28587-170">幅広いアシストを提供するボットより、特定の分野を深く掘り下げるボットの方がうまくいきます。</span><span class="sxs-lookup"><span data-stu-id="28587-170">Bots that go deep into a specific area rather than trying to be a broad assistant will work and fare better.</span></span>

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a><span data-ttu-id="28587-171">ランクが未設定の応答を使用した大規模な情報入手ナレッジ ベースの維持</span><span class="sxs-lookup"><span data-stu-id="28587-171">Maintaining a large retrieval knowledge base with unranked responses</span></span>

<span data-ttu-id="28587-172">Bot は、短時間で簡単にやり取りするのに最も適しています。これは、sifting ではなく、回答を探すために長いリストを使用しています。</span><span class="sxs-lookup"><span data-stu-id="28587-172">Bots are best suited for short, quick interactions, not sifting through long lists looking for an answer.</span></span>

## <a name="get-started"></a><span data-ttu-id="28587-173">作業の開始</span><span class="sxs-lookup"><span data-stu-id="28587-173">Get started</span></span>

* [<span data-ttu-id="28587-174">C#/dotnet での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="28587-174">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="28587-175">JavaScript での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="28587-175">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="28587-176">詳細情報</span><span class="sxs-lookup"><span data-stu-id="28587-176">Learn more</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="28587-177">Teams でのボットの基本</span><span class="sxs-lookup"><span data-stu-id="28587-177">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="28587-178">Teams のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="28587-178">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
