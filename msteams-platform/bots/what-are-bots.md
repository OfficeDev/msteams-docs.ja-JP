---
title: 会話ボットとは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e10275cba97f835cd59e572b48d2db7cb902d096
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "42635306"
---
# <a name="what-are-conversational-bots"></a><span data-ttu-id="8ec84-103">会話ボットとは</span><span class="sxs-lookup"><span data-stu-id="8ec84-103">What are conversational bots?</span></span>

<span data-ttu-id="8ec84-104">会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="8ec84-105">これらは非常に柔軟になっており、話し言葉の bot は、いくつかの簡単なコマンドまたは複雑で人為的に処理される、自然言語の仮想アシスタントを処理するようにスコープを設定できます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial-intelligence-powered and natural-language-processing virtual assistants.</span></span> <span data-ttu-id="8ec84-106">大規模なアプリケーションの1つの側面、または完全にスタンドアロンにすることができます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-106">They can be one aspect of a larger application, or completely stand-alone.</span></span>

<span data-ttu-id="8ec84-107">以下の GIF は、テキストと対話型カードの両方を使用して、1 対 1 のチャットのボットで会話しているユーザーを示しています。</span><span class="sxs-lookup"><span data-stu-id="8ec84-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="8ec84-108">カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="8ec84-109">ボットでテキスト以上のことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-109">Don't forget, bots are much more than just text!</span></span>

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="how-bots-work"></a><span data-ttu-id="8ec84-111">Bot のしくみ</span><span class="sxs-lookup"><span data-stu-id="8ec84-111">How bots work</span></span>

<span data-ttu-id="8ec84-112">Teams の bot は3つの要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-112">Your Teams bot consists of three elements:</span></span>

* <span data-ttu-id="8ec84-113">ホストをして、公開している Web サービス。</span><span class="sxs-lookup"><span data-stu-id="8ec84-113">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="8ec84-114">Bot が Bot フレームワークに登録されます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-114">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="8ec84-115">アプリマニフェストを含む Teams アプリパッケージ。</span><span class="sxs-lookup"><span data-stu-id="8ec84-115">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="8ec84-116">これは、ユーザーがインストールし、チームクライアントを Bot サービスを経由して web サービスに接続することです。</span><span class="sxs-lookup"><span data-stu-id="8ec84-116">This is what your users will install and connects the Teams client to your web service, routed through the Bot Service.</span></span>

<span data-ttu-id="8ec84-117">Microsoft Teams のボットは、[Microsoft Bot Framework](https://dev.botframework.com/)に基づいて構築されています。</span><span class="sxs-lookup"><span data-stu-id="8ec84-117">Bots for Microsoft Teams are built on the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="8ec84-118">Bot フレームワークに基づく bot が既にインストールされている場合は、それを Microsoft Teams での動作に容易に適応させることができます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-118">If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.</span></span> <span data-ttu-id="8ec84-119">[Sdk](/microsoftteams/platform/#pivot=sdk-tools)を利用するには、C# または node.js のどちらかを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8ec84-119">We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="8ec84-120">これらのパッケージは、基本的な Bot ビルダー SDK のクラスとメソッドを次のように拡張します。</span><span class="sxs-lookup"><span data-stu-id="8ec84-120">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="8ec84-121">Office 365 コネクタカードなどの専用カードの種類を使用します。</span><span class="sxs-lookup"><span data-stu-id="8ec84-121">Use specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="8ec84-122">アクティビティのチーム固有のチャネルデータを使用して設定します。</span><span class="sxs-lookup"><span data-stu-id="8ec84-122">Consume and set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="8ec84-123">メッセージング拡張要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="8ec84-123">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ec84-124">任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-124">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

> [!TIP]
> <span data-ttu-id="8ec84-125">Teams アプリ Studio \* を使用すると、アプリマニフェストを作成して構成し、web サービスを bot フレームワーク上の bot として登録できます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-125">Teams App Studio\* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="8ec84-126">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="8ec84-126">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="8ec84-127">「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="8ec84-127">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="8ec84-128">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="8ec84-128">Webhooks and connectors</span></span>

<span data-ttu-id="8ec84-129">Webhook とコネクタを使用すると、ワークフローやその他の単純なコマンドの開始など、基本的なやり取りを行うためのシンプルなボットを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-129">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="8ec84-130">これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-130">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="8ec84-131">詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="8ec84-131">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="where-bots-work-best"></a><span data-ttu-id="8ec84-132">Bot の最適な動作</span><span class="sxs-lookup"><span data-stu-id="8ec84-132">Where bots work best</span></span>

<span data-ttu-id="8ec84-133">Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-133">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="8ec84-134">各スコープに、会話ボット向けの機能と条件があります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-134">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="8ec84-135">チャネル</span><span class="sxs-lookup"><span data-stu-id="8ec84-135">In a channel</span></span>

<span data-ttu-id="8ec84-136">チャネルでは、複数のユーザー間のスレッド形式の会話が扱われます。多くのユーザー同士 (現在は最大 2000) で会話が行われる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-136">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="8ec84-137">これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-137">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="8ec84-138">ただし、従来の複数ターンの対話は、うまく動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-138">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="8ec84-139">多くの情報を収集する必要がある場合は、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8ec84-139">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="8ec84-140">ボットは `@mentioned` のメッセージにのみ直接アクセスできますが、Microsoft Graph および組織レベルの引き上げられたアクセス許可を使用して、会話から追加のメッセージを取得することはできません。</span><span class="sxs-lookup"><span data-stu-id="8ec84-140">Your bot will also only have access to messages where it's `@mentioned` directly, you cannot retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="8ec84-141">ボットの利点をチャネル内で活用できるシナリオは以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8ec84-141">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="8ec84-142">**通知** (特にユーザーが追加情報を取得するための対話型カードを提供する場合)。</span><span class="sxs-lookup"><span data-stu-id="8ec84-142">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="8ec84-143">投票やアンケート調査などの**フィードバック シナリオ**。</span><span class="sxs-lookup"><span data-stu-id="8ec84-143">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="8ec84-144">**単一の要求/応答サイクル**で解決できる対話。複数のメンバーで会話をする場合にこれが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-144">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="8ec84-145">**交流/娯楽を目的としたボット** — 面白い猫の画像を取得したり、勝者をランダムに選んだりします。</span><span class="sxs-lookup"><span data-stu-id="8ec84-145">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="8ec84-146">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="8ec84-146">In a group chat</span></span>

<span data-ttu-id="8ec84-147">グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。</span><span class="sxs-lookup"><span data-stu-id="8ec84-147">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="8ec84-148">チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。</span><span class="sxs-lookup"><span data-stu-id="8ec84-148">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="8ec84-149">チャネルと同様に、ボットは `@mentioned` のメッセージにのみに直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-149">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="8ec84-150">通常、チャネルで正常に動作するシナリオは、グループ チャットでも同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="8ec84-150">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="8ec84-151">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="8ec84-151">In a one-to-one chat</span></span>

<span data-ttu-id="8ec84-152">これは、会話ボットがユーザーとやり取りする従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="8ec84-152">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="8ec84-153">これにより、さまざまなワークロードを実現できます。</span><span class="sxs-lookup"><span data-stu-id="8ec84-153">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="8ec84-154">Q&A ボット、別のシステムでワークフローを開始するボット、ジョークを言うボット、メモを取るボットなどがありますが、これらはごく一部です。</span><span class="sxs-lookup"><span data-stu-id="8ec84-154">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="8ec84-155">機能を表示するための方法として、会話ベースのインターフェイスが最適な方法であるかどうかを必ず検討します。</span><span class="sxs-lookup"><span data-stu-id="8ec84-155">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="bot-fails"></a><span data-ttu-id="8ec84-156">Bot が失敗する</span><span class="sxs-lookup"><span data-stu-id="8ec84-156">Bot fails</span></span>

### <a name="having-multi-turn-experiences-in-chat"></a><span data-ttu-id="8ec84-157">チャットでの複数ターンエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="8ec84-157">Having multi-turn experiences in chat</span></span>

<span data-ttu-id="8ec84-158">Bot とユーザーの間の広範なダイアログは、タスクを完了するための低速で複雑な方法であり、開発者が状態を維持する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-158">An extensive dialog between your bot and the user is a slow and overly complex way to get a task completed and it also requires the developer to maintain state.</span></span> <span data-ttu-id="8ec84-159">この状態を終了するには、ユーザーはタイムアウトまたは「*キャンセル*」と入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ec84-159">To exit this state a user must either time-out or type “*Cancel*”.</span></span> <span data-ttu-id="8ec84-160">すべてのプロセスは、不必要に面倒です。</span><span class="sxs-lookup"><span data-stu-id="8ec84-160">Above all, the process is unnecessarily tedious:</span></span>

<span data-ttu-id="8ec84-161">ユーザー: Megan を使用して会議をスケジュールします。</span><span class="sxs-lookup"><span data-stu-id="8ec84-161">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="8ec84-162">BOT: 200 の結果が見つかった場合は、姓と名を含めるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="8ec84-162">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="8ec84-163">ユーザー: Megan Bowen を使用して会議をスケジュールします。</span><span class="sxs-lookup"><span data-stu-id="8ec84-163">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="8ec84-164">BOT: Megan Bowen とどのような時間を使用しますか?</span><span class="sxs-lookup"><span data-stu-id="8ec84-164">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="8ec84-165">ユーザー: 1:00 pm。</span><span class="sxs-lookup"><span data-stu-id="8ec84-165">USER: 1:00 pm.</span></span>

<span data-ttu-id="8ec84-166">BOT: どちらの日になりますか?</span><span class="sxs-lookup"><span data-stu-id="8ec84-166">BOT: On which day?</span></span>

### <a name="supporting-too-many-commands"></a><span data-ttu-id="8ec84-167">サポートするコマンドの数が多すぎる</span><span class="sxs-lookup"><span data-stu-id="8ec84-167">Supporting too many commands</span></span>

<span data-ttu-id="8ec84-168">特に広範なコマンドをサポートしているボットは、ユーザーによって成功または肯定されることはありません。</span><span class="sxs-lookup"><span data-stu-id="8ec84-168">A bot that supports excessive commands, especially a broad range of commands, will not be successful or viewed positively by users.</span></span> <span data-ttu-id="8ec84-169">現在の bot メニューに表示されるコマンドは6つだけなので、どのような頻度でも使用される可能性はほとんどありません。</span><span class="sxs-lookup"><span data-stu-id="8ec84-169">Since there are only 6 visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="8ec84-170">広範なアシスタントではなく、特定の地域に深く関係している bot は、fare に適しています。</span><span class="sxs-lookup"><span data-stu-id="8ec84-170">Bots that go deep into a specific area rather than trying to be a broad assistant will work and fare better.</span></span>

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a><span data-ttu-id="8ec84-171">ランク付けされていない応答を持つ大規模な取得ナレッジベースを維持する</span><span class="sxs-lookup"><span data-stu-id="8ec84-171">Maintaining a large retrieval knowledge base with unranked responses</span></span>

<span data-ttu-id="8ec84-172">Bot は短時間ですばやく対話するのに適していますが、sifting では、回答を検索するのに長いリストは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="8ec84-172">Bots are best suited for short, quick interactions, not sifting though long lists looking for an answer.</span></span>

## <a name="get-started"></a><span data-ttu-id="8ec84-173">作業の開始</span><span class="sxs-lookup"><span data-stu-id="8ec84-173">Get started</span></span>

* [<span data-ttu-id="8ec84-174">C#/dotnet での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="8ec84-174">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="8ec84-175">JavaScript での Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="8ec84-175">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="8ec84-176">詳細情報</span><span class="sxs-lookup"><span data-stu-id="8ec84-176">Learn more</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ec84-177">Teams でのボットの基本</span><span class="sxs-lookup"><span data-stu-id="8ec84-177">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ec84-178">Teams のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="8ec84-178">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
