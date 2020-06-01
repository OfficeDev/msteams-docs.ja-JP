---
title: 会話ボットとは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a88d516c57faa96e29de3e786910a13c4d65ac84
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2020
ms.locfileid: "44453869"
---
# <a name="what-are-conversational-bots"></a><span data-ttu-id="64f35-103">会話ボットとは</span><span class="sxs-lookup"><span data-stu-id="64f35-103">What are conversational bots?</span></span>

<span data-ttu-id="64f35-104">会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。</span><span class="sxs-lookup"><span data-stu-id="64f35-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="64f35-105">会話型ボットの機能は非常に柔軟性があり、単純なコマンドだけでなく、複雑で人工知能を搭載した自然言語処理の仮想アシスタントを処理できるようにスコープを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial-intelligence-powered and natural-language-processing virtual assistants.</span></span> <span data-ttu-id="64f35-106">大規模なアプリケーションはもちろん、スタンドアロンのものにも適用することができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-106">They can be one aspect of a larger application, or completely stand-alone.</span></span>

<span data-ttu-id="64f35-107">以下の GIF は、テキストと対話型カードの両方を使用して、1 対 1 のチャットのボットで会話しているユーザーを示しています。</span><span class="sxs-lookup"><span data-stu-id="64f35-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="64f35-108">カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="64f35-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="64f35-109">ボットでテキスト以上のことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="64f35-109">Don't forget, bots are much more than just text!</span></span>

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a><span data-ttu-id="64f35-111">Microsoft Bot フレームワークを使用して Teams 用の bot を構築する</span><span class="sxs-lookup"><span data-stu-id="64f35-111">Build  a bot for Teams with the Microsoft Bot Framework</span></span>

<span data-ttu-id="64f35-112">Microsoft Bot フレームワーク] ( https://dev.botframework.com/) C#、Java、Python、JavaScript を使用してボットを作成するための豊富な SDK)。</span><span class="sxs-lookup"><span data-stu-id="64f35-112">The Microsoft Bot Framework](https://dev.botframework.com/) is a rich SDK for building bots using C#, Java, Python, and JavaScript.</span></span> <span data-ttu-id="64f35-113">Bot Framework に基づくボットが既にある場合は、簡単な操作でそのボットを Microsoft Teams で動作するように適応させることができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-113">If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.</span></span> <span data-ttu-id="64f35-114">用意されている [SDK](/microsoftteams/platform/#pivot=sdk-tools) を活用するため、C# か Node.js を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="64f35-114">We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="64f35-115">これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。</span><span class="sxs-lookup"><span data-stu-id="64f35-115">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="64f35-116">Office 365 コネクタ カードなどの専用のカードを使用する。</span><span class="sxs-lookup"><span data-stu-id="64f35-116">Use specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="64f35-117">アクティビティに関する Teams 固有のチャネル データを使用して設定する。</span><span class="sxs-lookup"><span data-stu-id="64f35-117">Consume and set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="64f35-118">メッセージング拡張要求を処理する。</span><span class="sxs-lookup"><span data-stu-id="64f35-118">Process messaging extension requests.</span></span>

<span data-ttu-id="64f35-119">Teams ボットは次の 3 つ要素で構成されています。</span><span class="sxs-lookup"><span data-stu-id="64f35-119">Your Teams bot consists of three elements:</span></span>

* <span data-ttu-id="64f35-120">お客様がホストし、公開している Web サービス。</span><span class="sxs-lookup"><span data-stu-id="64f35-120">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="64f35-121">Bot Framework へのボットの登録。</span><span class="sxs-lookup"><span data-stu-id="64f35-121">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="64f35-122">アプリ マニフェストを含む Teams アプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="64f35-122">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="64f35-123">これは、ユーザーがインストールするもので、Bot Service 経由でルーティングされ、Teams クライアントをお客様の Web サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="64f35-123">This is what your users will install and connects the Teams client to your web service, routed through the Bot Service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64f35-124">任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="64f35-124">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

> [!TIP]
> <span data-ttu-id="64f35-125">Teams App Studio を使用すると、アプリ マニフェストを作成して構成でき、Web サービスを Bot Framework のボットとして登録できます。</span><span class="sxs-lookup"><span data-stu-id="64f35-125">Teams App Studio\* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="64f35-126">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="64f35-126">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="64f35-127">「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="64f35-127">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a><span data-ttu-id="64f35-128">Microsoft Power Virtual Agent を使用して Teams の chatbot を作成する</span><span class="sxs-lookup"><span data-stu-id="64f35-128">Create a chatbot for Teams with Microsoft Power Virtual Agents</span></span>

<span data-ttu-id="64f35-129">[パワー仮想エージェント](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft Power Platform および Bot フレームワーク上に構築された chatbot サービスです。</span><span class="sxs-lookup"><span data-stu-id="64f35-129">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a chatbot service, built on the Microsoft Power platform and Bot Framework.</span></span>  <span data-ttu-id="64f35-130">パワー仮想エージェントの開発プロセスでは、コード化されていないグラフィカルインターフェイスアプローチを使用して、チームのすべてのメンバーがインテリジェントな仮想エージェントを簡単に作成および管理できるようにします。</span><span class="sxs-lookup"><span data-stu-id="64f35-130">The Power Virtual Agent development process uses a guided, no-code, graphical interface approach to empower every member of your team to easily create and maintain an intelligent virtual agent.</span></span>  <span data-ttu-id="64f35-131">[Power Virtual agents ポータル](https://powervirtualagents.microsoft.com)で chatbot を作成したら、 [power virtual agents Chatbot と Teams](how-to/add-power-virtual-agents-bot-to-teams.md)を簡単に統合することができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-131">Once you have completed creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate your Power Virtual Agents chatbot with Teams](how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="64f35-132">パワー仮想エージェント chatbot の作成を開始するには、[パワー仮想エージェントのドキュメント](https://docs.microsoft.com/power-virtual-agents/)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="64f35-132">To get started creating your Power Virtual Agents chatbot, *see* the [Power Virtual Agents documentation](https://docs.microsoft.com/power-virtual-agents/).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="64f35-133">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="64f35-133">Webhooks and connectors</span></span>

<span data-ttu-id="64f35-134">Webhook とコネクタを使用すると、ワークフローやその他の単純なコマンドの開始など、基本的なやり取りを行うためのシンプルなボットを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-134">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="64f35-135">これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-135">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="64f35-136">詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="64f35-136">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="where-bots-work-best"></a><span data-ttu-id="64f35-137">ボットが最適に動作するケース</span><span class="sxs-lookup"><span data-stu-id="64f35-137">Where bots work best</span></span>

<span data-ttu-id="64f35-138">Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-138">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="64f35-139">各スコープに、会話ボット向けの機能と条件があります。</span><span class="sxs-lookup"><span data-stu-id="64f35-139">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="64f35-140">チャネル</span><span class="sxs-lookup"><span data-stu-id="64f35-140">In a channel</span></span>

<span data-ttu-id="64f35-141">チャネルでは、複数のユーザー間のスレッド形式の会話が扱われます。多くのユーザー同士 (現在は最大 2000) で会話が行われる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="64f35-141">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="64f35-142">これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="64f35-142">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="64f35-143">ただし、従来の複数ターンの対話は、うまく動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="64f35-143">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="64f35-144">多くの情報を収集する必要がある場合は、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="64f35-144">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="64f35-145">Bot は、 `@mentioned` Microsoft Graph を使用して会話から他のメッセージを取得することもできますが、組織レベルの昇格されたアクセス許可を使用してメッセージを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="64f35-145">Your bot will also only have access to messages where it's `@mentioned` directly, although you can retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="64f35-146">ボットの利点をチャネル内で活用できるシナリオは以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="64f35-146">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="64f35-147">**通知** (特にユーザーが追加情報を取得するための対話型カードを提供する場合)。</span><span class="sxs-lookup"><span data-stu-id="64f35-147">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="64f35-148">投票やアンケート調査などの**フィードバック シナリオ**。</span><span class="sxs-lookup"><span data-stu-id="64f35-148">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="64f35-149">**単一の要求/応答サイクル**で解決できる対話。複数のメンバーで会話をする場合にこれが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="64f35-149">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="64f35-150">**交流/娯楽を目的としたボット** — 面白い猫の画像を取得したり、勝者をランダムに選んだりします。</span><span class="sxs-lookup"><span data-stu-id="64f35-150">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="64f35-151">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="64f35-151">In a group chat</span></span>

<span data-ttu-id="64f35-152">グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。</span><span class="sxs-lookup"><span data-stu-id="64f35-152">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="64f35-153">チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。</span><span class="sxs-lookup"><span data-stu-id="64f35-153">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="64f35-154">チャネルと同様に、ボットは `@mentioned` のメッセージにのみに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="64f35-154">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="64f35-155">通常、チャネルで正常に動作するシナリオは、グループ チャットでも同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="64f35-155">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="64f35-156">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="64f35-156">In a one-to-one chat</span></span>

<span data-ttu-id="64f35-157">これは、会話ボットがユーザーとやり取りする従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="64f35-157">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="64f35-158">これにより、さまざまなワークロードを実現できます。</span><span class="sxs-lookup"><span data-stu-id="64f35-158">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="64f35-159">Q&A ボット、別のシステムでワークフローを開始するボット、ジョークを言うボット、メモを取るボットなどがありますが、これらはごく一部です。</span><span class="sxs-lookup"><span data-stu-id="64f35-159">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="64f35-160">機能を表示するための方法として、会話ベースのインターフェイスが最適な方法であるかどうかを必ず検討します。</span><span class="sxs-lookup"><span data-stu-id="64f35-160">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="bot-fails"></a><span data-ttu-id="64f35-161">ボットが不適切なケース</span><span class="sxs-lookup"><span data-stu-id="64f35-161">Bot fails</span></span>

### <a name="having-multi-turn-experiences-in-chat"></a><span data-ttu-id="64f35-162">チャットで複数回やり取りが交わされる場合</span><span class="sxs-lookup"><span data-stu-id="64f35-162">Having multi-turn experiences in chat</span></span>

<span data-ttu-id="64f35-163">ボットとユーザーが対話を長く続けると、タスクの完了に要する時間が長くなり、必要以上に複雑になります。また、開発者は状態を維持することが必要になります。</span><span class="sxs-lookup"><span data-stu-id="64f35-163">An extensive dialog between your bot and the user is a slow and overly complex way to get a task completed and it also requires the developer to maintain state.</span></span> <span data-ttu-id="64f35-164">このような状態を終了するには、ユーザーはタイムアウトするか、「*Cancel*」と入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="64f35-164">To exit this state a user must either time-out or type “*Cancel*”.</span></span> <span data-ttu-id="64f35-165">何より、この処理は不必要なほど長々しいものになります。</span><span class="sxs-lookup"><span data-stu-id="64f35-165">Above all, the process is unnecessarily tedious:</span></span>

<span data-ttu-id="64f35-166">ユーザー: Megan との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="64f35-166">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="64f35-167">ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。</span><span class="sxs-lookup"><span data-stu-id="64f35-167">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="64f35-168">ユーザー: Megan Bowen との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="64f35-168">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="64f35-169">ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?</span><span class="sxs-lookup"><span data-stu-id="64f35-169">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="64f35-170">ユーザー: 午後 1 時に。</span><span class="sxs-lookup"><span data-stu-id="64f35-170">USER: 1:00 pm.</span></span>

<span data-ttu-id="64f35-171">ボット: 何日のですか?</span><span class="sxs-lookup"><span data-stu-id="64f35-171">BOT: On which day?</span></span>

### <a name="supporting-too-many-commands"></a><span data-ttu-id="64f35-172">サポートすべきコマンドが多すぎる場合</span><span class="sxs-lookup"><span data-stu-id="64f35-172">Supporting too many commands</span></span>

<span data-ttu-id="64f35-173">サポートするコマンドがあまりに多く、特に広範な種類に及ぶボットは、うまく機能しないことや、ユーザーからの評価が低くなる傾向があります。</span><span class="sxs-lookup"><span data-stu-id="64f35-173">A bot that supports excessive commands, especially a broad range of commands, will not be successful or viewed positively by users.</span></span> <span data-ttu-id="64f35-174">現在のボット メニューにはコマンドが 6 つしか表示されないため、それ以外のコマンドは滅多に使用されなくなります。</span><span class="sxs-lookup"><span data-stu-id="64f35-174">Since there are only 6 visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="64f35-175">幅広いアシストを提供するボットより、特定の分野を深く掘り下げるボットの方がうまくいきます。</span><span class="sxs-lookup"><span data-stu-id="64f35-175">Bots that go deep into a specific area rather than trying to be a broad assistant will work and fare better.</span></span>

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a><span data-ttu-id="64f35-176">ランクが未設定の応答を使用した大規模な情報入手ナレッジ ベースの維持</span><span class="sxs-lookup"><span data-stu-id="64f35-176">Maintaining a large retrieval knowledge base with unranked responses</span></span>

<span data-ttu-id="64f35-177">Bot は、短時間で簡単にやり取りするのに最も適しています。これは、sifting ではなく、回答を探すために長いリストを使用しています。</span><span class="sxs-lookup"><span data-stu-id="64f35-177">Bots are best suited for short, quick interactions, not sifting through long lists looking for an answer.</span></span>

## <a name="get-started"></a><span data-ttu-id="64f35-178">作業の開始</span><span class="sxs-lookup"><span data-stu-id="64f35-178">Get started</span></span>

* [<span data-ttu-id="64f35-179">C#/dotnet での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="64f35-179">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="64f35-180">JavaScript での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="64f35-180">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="64f35-181">詳細情報</span><span class="sxs-lookup"><span data-stu-id="64f35-181">Learn more</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64f35-182">Teams でのボットの基本</span><span class="sxs-lookup"><span data-stu-id="64f35-182">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="64f35-183">Teams のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="64f35-183">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
