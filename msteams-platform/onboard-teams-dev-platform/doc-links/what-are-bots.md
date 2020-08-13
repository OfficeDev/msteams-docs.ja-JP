---
title: ボットとは
author: clearab
description: Microsoft Teams のボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 1e07d56769cbb303f9af98f84c8ae6064325c1a7
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652063"
---
# <a name="what-are-bots"></a><span data-ttu-id="7ce89-103">ボットとは</span><span class="sxs-lookup"><span data-stu-id="7ce89-103">What are bots?</span></span>

<span data-ttu-id="7ce89-104">Bot は、ユーザーがテキスト、インタラクティブなカード、およびタスクモジュールを使用して web サービスを操作することを許可します。</span><span class="sxs-lookup"><span data-stu-id="7ce89-104">Bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="7ce89-105">これらは非常に柔軟性があります。ボットをスコープ化して、人工知能や自然言語処理で提供されるいくつかの簡単なコマンドや仮想アシスタントを処理することができます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-105">They're incredibly flexible — you can scope bots to handle a few simple commands or virtual assistants powered by artificial intelligence and natural language processing.</span></span> <span data-ttu-id="7ce89-106">大規模なアプリケーションまたは完全にスタンドアロンのいずれかの側面にすることができます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-106">They can be one aspect of a larger application or completely standalone.</span></span>

<span data-ttu-id="7ce89-107">カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-107">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="7ce89-108">ボットでテキスト以上のことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-108">Don't forget, bots are much more than just text!</span></span>

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="user-scenarios"></a><span data-ttu-id="7ce89-110">ユーザーのシナリオ</span><span class="sxs-lookup"><span data-stu-id="7ce89-110">User scenarios</span></span>

<span data-ttu-id="7ce89-111">Microsoft Teams のボットは、チャネル、グループチャット、または1対1のチャットの一部にすることができます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-111">Bots in Microsoft Teams can be part of a channel, group chat, or one-on-one chat.</span></span> <span data-ttu-id="7ce89-112">各スコープに、会話ボット向けの機能と条件があります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-112">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="7ce89-113">チャネル</span><span class="sxs-lookup"><span data-stu-id="7ce89-113">In a channel</span></span>

<span data-ttu-id="7ce89-114">チャネルでは、複数のユーザー間のスレッド形式の会話が扱われます。多くのユーザー同士 (現在は最大 2000) で会話が行われる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-114">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="7ce89-115">これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-115">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="7ce89-116">ただし、従来の複数ターンの対話は、うまく動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-116">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="7ce89-117">多くの情報を収集する必要がある場合は、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7ce89-117">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="7ce89-118">Bot は、 `@mentioned` Microsoft Graph を使用して会話から他のメッセージを取得することもできますが、組織レベルの昇格されたアクセス許可を使用してメッセージを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-118">Your bot will also only have access to messages where it's `@mentioned` directly, although you can retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="7ce89-119">ボットの利点をチャネル内で活用できるシナリオは以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7ce89-119">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="7ce89-120">**通知** (特にユーザーが追加情報を取得するための対話型カードを提供する場合)。</span><span class="sxs-lookup"><span data-stu-id="7ce89-120">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="7ce89-121">投票やアンケート調査などの**フィードバック シナリオ**。</span><span class="sxs-lookup"><span data-stu-id="7ce89-121">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="7ce89-122">**単一の要求/応答サイクル**で解決できる対話。複数のメンバーで会話をする場合にこれが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-122">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="7ce89-123">**交流/娯楽を目的としたボット** — 面白い猫の画像を取得したり、勝者をランダムに選んだりします。</span><span class="sxs-lookup"><span data-stu-id="7ce89-123">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="7ce89-124">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="7ce89-124">In a group chat</span></span>

<span data-ttu-id="7ce89-125">グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。</span><span class="sxs-lookup"><span data-stu-id="7ce89-125">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="7ce89-126">チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。</span><span class="sxs-lookup"><span data-stu-id="7ce89-126">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="7ce89-127">チャネルと同様に、ボットは `@mentioned` のメッセージにのみに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-127">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="7ce89-128">通常、チャネルで正常に動作するシナリオは、グループ チャットでも同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="7ce89-128">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-on-one-chat"></a><span data-ttu-id="7ce89-129">1対1のチャット</span><span class="sxs-lookup"><span data-stu-id="7ce89-129">In a one-on-one chat</span></span>

<span data-ttu-id="7ce89-130">これは、会話ボットがユーザーとやり取りする従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="7ce89-130">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="7ce89-131">これにより、さまざまなワークロードを実現できます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-131">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="7ce89-132">Q&A ボット、別のシステムでワークフローを開始するボット、ジョークを言うボット、メモを取るボットなどがありますが、これらはごく一部です。</span><span class="sxs-lookup"><span data-stu-id="7ce89-132">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="7ce89-133">機能を表示するための方法として、会話ベースのインターフェイスが最適な方法であるかどうかを必ず検討します。</span><span class="sxs-lookup"><span data-stu-id="7ce89-133">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="building-a-teams-bot-with-the-microsoft-bot-framework"></a><span data-ttu-id="7ce89-134">Microsoft Bot フレームワークを使用して Teams bot を構築する</span><span class="sxs-lookup"><span data-stu-id="7ce89-134">Building a Teams bot with the Microsoft Bot Framework</span></span>

<span data-ttu-id="7ce89-135">[Microsoft Bot フレームワーク](https://dev.botframework.com/)は、C#、Java、Python、または JavaScript を使用してボットを作成するための豊富な SDK です。</span><span class="sxs-lookup"><span data-stu-id="7ce89-135">The [Microsoft Bot Framework](https://dev.botframework.com/) is a rich SDK for building bots using C#, Java, Python, or JavaScript.</span></span> <span data-ttu-id="7ce89-136">Bot Framework に基づくボットが既にある場合は、簡単な操作でそのボットを Microsoft Teams で動作するように適応させることができます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-136">If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.</span></span> <span data-ttu-id="7ce89-137">用意されている [SDK](/microsoftteams/platform/#pivot=sdk-tools) を活用するため、C# か Node.js を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7ce89-137">We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="7ce89-138">これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。</span><span class="sxs-lookup"><span data-stu-id="7ce89-138">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="7ce89-139">Office 365 コネクタ カードなどの専用のカードを使用する。</span><span class="sxs-lookup"><span data-stu-id="7ce89-139">Use specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="7ce89-140">アクティビティに関する Teams 固有のチャネル データを使用して設定する。</span><span class="sxs-lookup"><span data-stu-id="7ce89-140">Consume and set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="7ce89-141">メッセージング拡張要求を処理する。</span><span class="sxs-lookup"><span data-stu-id="7ce89-141">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ce89-142">任意の web プログラミングテクノロジで Teams アプリを開発し、 [Bot フレームワーク REST api](/bot-framework/rest-api/bot-framework-rest-overview)を直接呼び出すことができますが、すべてのトークン処理を自分自身で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-142">You can develop Teams apps in any web programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="7ce89-143">Teams ボットは次の 3 つ要素で構成されています。</span><span class="sxs-lookup"><span data-stu-id="7ce89-143">Your Teams bot consists of three elements:</span></span>

* <span data-ttu-id="7ce89-144">お客様がホストし、公開している Web サービス。</span><span class="sxs-lookup"><span data-stu-id="7ce89-144">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="7ce89-145">Bot Framework へのボットの登録。</span><span class="sxs-lookup"><span data-stu-id="7ce89-145">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="7ce89-146">アプリ マニフェストを含む Teams アプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="7ce89-146">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="7ce89-147">これは、ユーザーがインストールするもので、Bot Service 経由でルーティングされ、Teams クライアントをお客様の Web サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="7ce89-147">This is what your users will install and connects the Teams client to your web service, routed through the Bot Service.</span></span>

> [!TIP]
> <span data-ttu-id="7ce89-148">Teams アプリ Studio \* を使用すると、アプリマニフェストを作成して構成し、その web サービスを bot フレームワーク上の bot として登録できます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-148">Teams App Studio\* helps you create and configure your app manifest and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="7ce89-149">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="7ce89-149">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="7ce89-150">「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="7ce89-150">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="building-a-teams-bot-with-microsoft-power-virtual-agents"></a><span data-ttu-id="7ce89-151">Microsoft Power Virtual Agent を使用して Teams bot を構築する</span><span class="sxs-lookup"><span data-stu-id="7ce89-151">Building a Teams bot with Microsoft Power Virtual Agents</span></span>

<span data-ttu-id="7ce89-152">[パワー仮想エージェント](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft power Platform および Bot フレームワーク上に構築されたサービスです。</span><span class="sxs-lookup"><span data-stu-id="7ce89-152">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a service built on the Microsoft Power platform and Bot Framework.</span></span> <span data-ttu-id="7ce89-153">パワー仮想エージェントの開発プロセスでは、コード化されていないグラフィカルインターフェイスアプローチを使用して、チームのすべてのメンバーがインテリジェントな仮想エージェントを簡単に作成および管理できるようにします。</span><span class="sxs-lookup"><span data-stu-id="7ce89-153">The Power Virtual Agent development process uses a guided, no-code, graphical interface approach to empower every member of your team to easily create and maintain an intelligent virtual agent.</span></span> <span data-ttu-id="7ce89-154">[Power Virtual agents ポータル](https://powervirtualagents.microsoft.com)で chatbot を作成したら、 [power virtual agents Chatbot と Teams](../../bots/how-to/add-power-virtual-agents-bot-to-teams.md)を簡単に統合することができます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-154">Once you have completed creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate your Power Virtual Agents chatbot with Teams](../../bots/how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="7ce89-155">パワー仮想エージェント chatbot の作成を開始するには、[パワー仮想エージェントのドキュメント](https://docs.microsoft.com/power-virtual-agents/)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="7ce89-155">To get started creating your Power Virtual Agents chatbot, *see* the [Power Virtual Agents documentation](https://docs.microsoft.com/power-virtual-agents/).</span></span>

## <a name="connectors-and-bots"></a><span data-ttu-id="7ce89-156">コネクタとボット</span><span class="sxs-lookup"><span data-stu-id="7ce89-156">Connectors and bots</span></span>

<span data-ttu-id="7ce89-157">コネクタを使用すると、ワークフローなどの単純なコマンドのや議など、基本的な操作のための簡単な bot を作成できます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-157">Connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="7ce89-158">これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-158">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="7ce89-159">詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="7ce89-159">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="bot-fails"></a><span data-ttu-id="7ce89-160">ボットが不適切なケース</span><span class="sxs-lookup"><span data-stu-id="7ce89-160">Bot fails</span></span>

### <a name="having-multi-turn-experiences-in-chat"></a><span data-ttu-id="7ce89-161">チャットで複数回やり取りが交わされる場合</span><span class="sxs-lookup"><span data-stu-id="7ce89-161">Having multi-turn experiences in chat</span></span>

<span data-ttu-id="7ce89-162">ボットとユーザーが対話を長く続けると、タスクの完了に要する時間が長くなり、必要以上に複雑になります。また、開発者は状態を維持することが必要になります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-162">An extensive dialog between your bot and the user is a slow and overly complex way to get a task completed and it also requires the developer to maintain state.</span></span> <span data-ttu-id="7ce89-163">このような状態を終了するには、ユーザーはタイムアウトするか、「*Cancel*」と入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-163">To exit this state a user must either time-out or type “*Cancel*”.</span></span> <span data-ttu-id="7ce89-164">何より、この処理は不必要なほど長々しいものになります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-164">Above all, the process is unnecessarily tedious:</span></span>

<span data-ttu-id="7ce89-165">ユーザー: Megan との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="7ce89-165">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="7ce89-166">ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。</span><span class="sxs-lookup"><span data-stu-id="7ce89-166">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="7ce89-167">ユーザー: Megan Bowen との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="7ce89-167">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="7ce89-168">ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?</span><span class="sxs-lookup"><span data-stu-id="7ce89-168">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="7ce89-169">ユーザー: 午後 1 時に。</span><span class="sxs-lookup"><span data-stu-id="7ce89-169">USER: 1:00 pm.</span></span>

<span data-ttu-id="7ce89-170">ボット: 何日のですか?</span><span class="sxs-lookup"><span data-stu-id="7ce89-170">BOT: On which day?</span></span>

### <a name="supporting-too-many-commands"></a><span data-ttu-id="7ce89-171">サポートすべきコマンドが多すぎる場合</span><span class="sxs-lookup"><span data-stu-id="7ce89-171">Supporting too many commands</span></span>

<span data-ttu-id="7ce89-172">サポートするコマンドがあまりに多く、特に広範な種類に及ぶボットは、うまく機能しないことや、ユーザーからの評価が低くなる傾向があります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-172">A bot that supports excessive commands, especially a broad range of commands, will not be successful or viewed positively by users.</span></span> <span data-ttu-id="7ce89-173">現在のボット メニューにはコマンドが 6 つしか表示されないため、それ以外のコマンドは滅多に使用されなくなります。</span><span class="sxs-lookup"><span data-stu-id="7ce89-173">Since there are only 6 visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="7ce89-174">幅広いアシストを提供するボットより、特定の分野を深く掘り下げるボットの方がうまくいきます。</span><span class="sxs-lookup"><span data-stu-id="7ce89-174">Bots that go deep into a specific area rather than trying to be a broad assistant will work and fare better.</span></span>

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a><span data-ttu-id="7ce89-175">ランクが未設定の応答を使用した大規模な情報入手ナレッジ ベースの維持</span><span class="sxs-lookup"><span data-stu-id="7ce89-175">Maintaining a large retrieval knowledge base with unranked responses</span></span>

<span data-ttu-id="7ce89-176">Bot は、短時間で簡単にやり取りするのに最も適しています。これは、sifting ではなく、回答を探すために長いリストを使用しています。</span><span class="sxs-lookup"><span data-stu-id="7ce89-176">Bots are best suited for short, quick interactions, not sifting through long lists looking for an answer.</span></span>

## <a name="get-started"></a><span data-ttu-id="7ce89-177">作業の開始</span><span class="sxs-lookup"><span data-stu-id="7ce89-177">Get started</span></span>

* [<span data-ttu-id="7ce89-178">C#/dotnet での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="7ce89-178">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="7ce89-179">JavaScript での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="7ce89-179">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="7ce89-180">詳細情報</span><span class="sxs-lookup"><span data-stu-id="7ce89-180">Learn more</span></span>

* [<span data-ttu-id="7ce89-181">Teams でのボットの基本</span><span class="sxs-lookup"><span data-stu-id="7ce89-181">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)
* [<span data-ttu-id="7ce89-182">Teams のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="7ce89-182">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
* [<span data-ttu-id="7ce89-183">アプリを計画する</span><span class="sxs-lookup"><span data-stu-id="7ce89-183">Planning your app</span></span>](../../concepts/extensibility-points.md)
* <span data-ttu-id="7ce89-184">[アプリを設計する]./(../デザインの概要 (英語) (英語)</span><span class="sxs-lookup"><span data-stu-id="7ce89-184">[Designing your app]../(../designing-your-app/designing-overview.md)</span></span>
* [<span data-ttu-id="7ce89-185">アプリのビルド</span><span class="sxs-lookup"><span data-stu-id="7ce89-185">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="7ce89-186">アプリの発行</span><span class="sxs-lookup"><span data-stu-id="7ce89-186">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
