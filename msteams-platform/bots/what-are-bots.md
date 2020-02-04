---
title: 話し言葉の bot とは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7bde886b67788a355181c83287d999a3bfb9727a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674746"
---
# <a name="what-are-conversational-bots"></a><span data-ttu-id="f47c0-103">話し言葉の bot とは</span><span class="sxs-lookup"><span data-stu-id="f47c0-103">What are conversational bots?</span></span>

<span data-ttu-id="f47c0-104">話し言葉の bot は、ユーザーがテキスト、インタラクティブなカード、およびタスクモジュールを使用して web サービスと対話できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f47c0-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="f47c0-105">これらは非常に柔軟になっており、話し言葉の bot は、いくつかの簡単なコマンドや、複雑で人為的な知性を備えた、自然言語処理仮想アシスタントを処理するようにスコープを設定できます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial intelligence powered and natural language processing virtual assistants.</span></span> <span data-ttu-id="f47c0-106">これは、大規模なアプリケーションの1つの側面、または完全に独立したものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-106">They can be one aspect of a larger application, or completely stand alone.</span></span>

<span data-ttu-id="f47c0-107">次の GIF は、テキストカードとインタラクティブカードの両方を使用して、1対1のチャットに bot があるユーザー conversing を示しています。</span><span class="sxs-lookup"><span data-stu-id="f47c0-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="f47c0-108">カード、テキスト、タスクモジュールを適切に組み合わせて見つけることは、便利な bot を作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="f47c0-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="f47c0-109">忘れずに、ボットはテキストだけではありません。</span><span class="sxs-lookup"><span data-stu-id="f47c0-109">Don't forget, bots are much more than just text!</span></span>

![FAQ + gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="what-tasks-are-best-handled-by-bots"></a><span data-ttu-id="f47c0-111">Bot が最適に処理できるタスク</span><span class="sxs-lookup"><span data-stu-id="f47c0-111">What tasks are best handled by bots?</span></span>

<span data-ttu-id="f47c0-112">Microsoft Teams のボットは、1対1の会話、グループチャット、またはチーム内のチャネルの一部にすることができます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-112">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="f47c0-113">各スコープによって、会話の bot に固有の機会と課題が提供されます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-113">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="f47c0-114">チャネル内</span><span class="sxs-lookup"><span data-stu-id="f47c0-114">In a channel</span></span>

<span data-ttu-id="f47c0-115">チャネルには、複数のユーザー間のスレッド化された会話が含まれています。多くのユーザー (現在は最大 2000)。</span><span class="sxs-lookup"><span data-stu-id="f47c0-115">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="f47c0-116">これにより、ボットが大規模になる可能性がありますが、個々の相互作用を簡潔にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f47c0-116">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="f47c0-117">従来のマルチターンの対話は、おそらくうまく機能しません。</span><span class="sxs-lookup"><span data-stu-id="f47c0-117">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="f47c0-118">その代わりに、多くの情報を収集する必要がある場合は、対話形式のカードまたはタスクモジュールを使用するか、会話を1対1の会話に移動することをお探しください。</span><span class="sxs-lookup"><span data-stu-id="f47c0-118">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="f47c0-119">Bot は、直接メッセージにアクセスできるだけで、Microsoft `@mentioned` Graph を使用して会話から他のメッセージを取得することも、組織レベルの管理者レベルのアクセス許可を使用することもできません。</span><span class="sxs-lookup"><span data-stu-id="f47c0-119">Your bot will also only have access to messages where it's `@mentioned` directly, you cannot retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="f47c0-120">チャネルのボット excel には、次のようなシナリオがあります。</span><span class="sxs-lookup"><span data-stu-id="f47c0-120">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="f47c0-121">**通知**(特に、ユーザーが追加情報を必要とする対話カードを提供している場合)。</span><span class="sxs-lookup"><span data-stu-id="f47c0-121">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="f47c0-122">投票や調査などの**フィードバックシナリオ**。</span><span class="sxs-lookup"><span data-stu-id="f47c0-122">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="f47c0-123">**単一の要求/応答サイクル**で解決できる相互作用。これにより、結果は会話の複数のメンバーにとって役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-123">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="f47c0-124">**ソーシャル/おもしろいボット**—すばらしい cat 画像を取得し、ランダムに選択します。</span><span class="sxs-lookup"><span data-stu-id="f47c0-124">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="f47c0-125">グループチャット</span><span class="sxs-lookup"><span data-stu-id="f47c0-125">In a group chat</span></span>

<span data-ttu-id="f47c0-126">グループチャットは、3人以上のユーザー間のスレッド以外の会話です。</span><span class="sxs-lookup"><span data-stu-id="f47c0-126">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="f47c0-127">チャネルのメンバー数が少なくなる傾向があります。</span><span class="sxs-lookup"><span data-stu-id="f47c0-127">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="f47c0-128">チャネルに似ていますが、bot は`@mentioned`直接メッセージにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-128">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="f47c0-129">通常、チャネルで正常に動作するシナリオは、グループチャットでも同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="f47c0-129">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="f47c0-130">ワンツーワンチャット</span><span class="sxs-lookup"><span data-stu-id="f47c0-130">In a one-to-one chat</span></span>

<span data-ttu-id="f47c0-131">これは、会話の bot がユーザーと対話するための従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="f47c0-131">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="f47c0-132">これにより、非常に多様なワークロードを実現できます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-132">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="f47c0-133">Q&他のシステムでワークフローを開始する bot、ジョークになる bot、およびメモを取る bot は、いくつかの例にすぎません。</span><span class="sxs-lookup"><span data-stu-id="f47c0-133">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="f47c0-134">会話ベースのインターフェイスが機能を提供するのに最適な方法かどうかを考慮することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="f47c0-134">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="how-do-bots-work"></a><span data-ttu-id="f47c0-135">Bot はどのように動作しますか?</span><span class="sxs-lookup"><span data-stu-id="f47c0-135">How do bots work?</span></span>

<span data-ttu-id="f47c0-136">Bot は3つの部分で構成されます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-136">Your bot consists of three pieces:</span></span>

* <span data-ttu-id="f47c0-137">ホストしているパブリックアクセス可能な web サービス。</span><span class="sxs-lookup"><span data-stu-id="f47c0-137">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="f47c0-138">Bot を Bot フレームワークに登録する bot 登録。</span><span class="sxs-lookup"><span data-stu-id="f47c0-138">Your bot registration that registers your bot with the Bot Framework.</span></span>
* <span data-ttu-id="f47c0-139">アプリマニフェストを含む Teams アプリパッケージ。</span><span class="sxs-lookup"><span data-stu-id="f47c0-139">Your Teams app package that contains your app manifest.</span></span> <span data-ttu-id="f47c0-140">これは、ユーザーがインストールし、Teams クライアントを web サービス (Bot サービスを経由してルーティング) に接続することです。</span><span class="sxs-lookup"><span data-stu-id="f47c0-140">This is what your users install and connects the Teams client to your web service (routed through the Bot Service).</span></span>

<span data-ttu-id="f47c0-141">Microsoft Teams のボットは、 [Microsoft Bot フレームワーク](https://dev.botframework.com/)に基づいて構築されています。</span><span class="sxs-lookup"><span data-stu-id="f47c0-141">Bots for Microsoft Teams are built on the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="f47c0-142">(Bot フレームワークに基づく bot が既にある場合は、それを Microsoft Teams での動作に容易に適応させることができます)。[Sdk](/microsoftteams/platform/#pivot=sdk-tools)を利用するには、C# または node.js のどちらかを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f47c0-142">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="f47c0-143">これらのパッケージは、基本的な Bot ビルダー SDK のクラスとメソッドを拡張します。</span><span class="sxs-lookup"><span data-stu-id="f47c0-143">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="f47c0-144">Office 365 コネクタカードなどの特殊なカードの種類を使用します。</span><span class="sxs-lookup"><span data-stu-id="f47c0-144">Using specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="f47c0-145">アクティビティのチーム固有のチャネルデータの使用と設定。</span><span class="sxs-lookup"><span data-stu-id="f47c0-145">Consuming and setting Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="f47c0-146">メッセージング拡張要求を処理する。</span><span class="sxs-lookup"><span data-stu-id="f47c0-146">Processing messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f47c0-147">任意の web プログラミングテクノロジで Teams アプリを開発し、 [Bot フレームワーク REST api](/bot-framework/rest-api/bot-framework-rest-overview)を直接呼び出すことができますが、すべてのトークン処理を自分自身で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f47c0-147">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="f47c0-148">*Teams アプリ Studio*は、アプリマニフェストを作成して構成し、web サービスを bot フレームワーク上の bot として登録できます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-148">*Teams App Studio* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="f47c0-149">また、コントロールライブラリとインタラクティブカードビルダーを備えています。</span><span class="sxs-lookup"><span data-stu-id="f47c0-149">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="f47c0-150">「 [Teams アプリ Studio の](~/concepts/build-and-test/app-studio-overview.md)概要 *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="f47c0-150">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="f47c0-151">Webhooks とコネクタ</span><span class="sxs-lookup"><span data-stu-id="f47c0-151">Webhooks and connectors</span></span>

<span data-ttu-id="f47c0-152">Webhooks とコネクタを使用すると、ワークフローまたは他の単純なコマンドのや議など、基本的な操作のための簡単な bot を作成できます。</span><span class="sxs-lookup"><span data-stu-id="f47c0-152">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="f47c0-153">これらのユーザーは、それらを作成したチーム内にのみ存在し、会社のワークフローに固有の単純なプロセスを対象としています。</span><span class="sxs-lookup"><span data-stu-id="f47c0-153">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="f47c0-154">詳細について[は、「webhook とコネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)につい*て」を参照して*ください。</span><span class="sxs-lookup"><span data-stu-id="f47c0-154">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="get-started"></a><span data-ttu-id="f47c0-155">作業の開始</span><span class="sxs-lookup"><span data-stu-id="f47c0-155">Get started</span></span>

* [<span data-ttu-id="f47c0-156">C#/dotnet での Teams 会話のボット</span><span class="sxs-lookup"><span data-stu-id="f47c0-156">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="f47c0-157">JavaScript での Teams の会話のボット</span><span class="sxs-lookup"><span data-stu-id="f47c0-157">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="f47c0-158">詳細情報</span><span class="sxs-lookup"><span data-stu-id="f47c0-158">Learn more</span></span>

* [<span data-ttu-id="f47c0-159">Teams でのボットの基本</span><span class="sxs-lookup"><span data-stu-id="f47c0-159">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)
* [<span data-ttu-id="f47c0-160">Teams の bot を作成する</span><span class="sxs-lookup"><span data-stu-id="f47c0-160">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
