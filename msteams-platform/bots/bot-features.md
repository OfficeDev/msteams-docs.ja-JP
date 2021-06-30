---
title: ボットと SDK
author: surbhigupta
description: ボットを構築するためのツールと SDK Microsoft Teams概要。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: c346d7b7a1c720e651a847fb8a650fc549689654
ms.sourcegitcommit: f62634c59b697107e5bb3c38867b21007d328b1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53196244"
---
# <a name="bots-and-sdks"></a><span data-ttu-id="31726-103">ボットと SDK</span><span class="sxs-lookup"><span data-stu-id="31726-103">Bots and SDKs</span></span>

<span data-ttu-id="31726-104">次のいずれかのツールまたは機能を使用して、Microsoft Teamsで動作するボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="31726-104">You can create a bot that works in Microsoft Teams with one of the following tools or capabilities:</span></span>

* [<span data-ttu-id="31726-105">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="31726-105">Microsoft Bot Framework SDK</span></span>](#bots-with-the-microsoft-bot-framework)
* [<span data-ttu-id="31726-106">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="31726-106">Power Virtual Agents</span></span>](#bots-with-power-virtual-agents)
* [<span data-ttu-id="31726-107">Virtual Assistant</span><span class="sxs-lookup"><span data-stu-id="31726-107">Virtual Assistant</span></span>](~/samples/virtual-assistant.md)
* [<span data-ttu-id="31726-108">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="31726-108">Webhooks and connectors</span></span>](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a><span data-ttu-id="31726-109">ボットとMicrosoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="31726-109">Bots with the Microsoft Bot Framework</span></span>

<span data-ttu-id="31726-110">ボットTeams、次の要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="31726-110">Your Teams bot consists of the following:</span></span>

* <span data-ttu-id="31726-111">ユーザーがホストする一般にアクセス可能な Web サービス。</span><span class="sxs-lookup"><span data-stu-id="31726-111">A publicly accessible web service hosted by you.</span></span>
* <span data-ttu-id="31726-112">Web サービスのボット フレームワーク登録。</span><span class="sxs-lookup"><span data-stu-id="31726-112">A Bot Framework registration for your web service.</span></span>
* <span data-ttu-id="31726-113">クライアントTeams Web サービスに接続するTeamsアプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="31726-113">Your Teams app package, which connects the Teams client to your web service.</span></span>

> [!TIP]
> <span data-ttu-id="31726-114">開発者ポータルを使用して、Web サービスをボット フレームワークに登録し、アプリ構成を指定します。</span><span class="sxs-lookup"><span data-stu-id="31726-114">Use the Developer Portal to register your web service with the Bot Framework and specify your app configurations.</span></span> <span data-ttu-id="31726-115">詳細については、「開発者ポータルでアプリを管理する」[を参照Teams。](~/concepts/build-and-test/teams-developer-portal.md)</span><span class="sxs-lookup"><span data-stu-id="31726-115">For more information, see [manage your apps with the Developer Portal for Teams](~/concepts/build-and-test/teams-developer-portal.md).</span></span>

<span data-ttu-id="31726-116">ボット [フレームワークは、](https://dev.botframework.com/) カスタム スクリプト、C#、Python、および JavaScript をJavaボットを作成するために使用される豊富な SDK です。</span><span class="sxs-lookup"><span data-stu-id="31726-116">The [Bot Framework](https://dev.botframework.com/) is a rich SDK used to create bots using C#, Java, Python, and JavaScript.</span></span> <span data-ttu-id="31726-117">ボット フレームワークに基づくボットが既に存在する場合は、ボットフレームワークで動作するボットを簡単にTeams。</span><span class="sxs-lookup"><span data-stu-id="31726-117">If you already have a bot that is based on the Bot Framework, you can easily modify it to work in Teams.</span></span> <span data-ttu-id="31726-118">SDK を利用C#またはNode.jsを使用 [します](/microsoftteams/platform/#pivot=sdk-tools)。</span><span class="sxs-lookup"><span data-stu-id="31726-118">Use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="31726-119">これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。</span><span class="sxs-lookup"><span data-stu-id="31726-119">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="31726-120">コネクタ カードのような特殊なカードOffice 365使用します。</span><span class="sxs-lookup"><span data-stu-id="31726-120">Use specialized card types like the Office 365 connector card.</span></span>
* <span data-ttu-id="31726-121">アクティビティTeams固有のチャネル データを設定します。</span><span class="sxs-lookup"><span data-stu-id="31726-121">Set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="31726-122">メッセージング拡張要求を処理する。</span><span class="sxs-lookup"><span data-stu-id="31726-122">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31726-123">任意の web プログラミング Teamsアプリを開発し[、Bot Framework REST API を直接呼び出](/bot-framework/rest-api/bot-framework-rest-overview)します。</span><span class="sxs-lookup"><span data-stu-id="31726-123">You can develop Teams apps in any web programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly.</span></span> <span data-ttu-id="31726-124">ただし、すべてのケースでトークン処理を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31726-124">But you must perform token handling in all cases.</span></span>

## <a name="bots-with-power-virtual-agents"></a><span data-ttu-id="31726-125">ボットとPower Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="31726-125">Bots with Power Virtual Agents</span></span>

<span data-ttu-id="31726-126">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft Power プラットフォームとボット フレームワーク上に構築されたチャットボット サービスです。</span><span class="sxs-lookup"><span data-stu-id="31726-126">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a chatbot service built on the Microsoft Power platform and Bot Framework.</span></span> <span data-ttu-id="31726-127">Power Virtual Agent 開発プロセスでは、ガイド付き、コードなし、グラフィカル インターフェイスのアプローチを使用して、チーム メンバーがインテリジェントな仮想エージェントを簡単に作成および維持できます。</span><span class="sxs-lookup"><span data-stu-id="31726-127">The Power Virtual Agent development process uses a guided, no-code, and graphical interface approach that empowers your team members to easily create and maintain an intelligent virtual agent.</span></span> <span data-ttu-id="31726-128">ポータルでチャットボットを作成[Power Virtual Agents、](https://powervirtualagents.microsoft.com)チャットボットとチャットボットを簡単に統合[Teams。](how-to/add-power-virtual-agents-bot-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="31726-128">After creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate it with Teams](how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="31726-129">開始方法の詳細については、「ドキュメント」[をPower Virtual Agentsしてください](/power-virtual-agents)。</span><span class="sxs-lookup"><span data-stu-id="31726-129">For more information on getting started, see [Power Virtual Agents documentation](/power-virtual-agents).</span></span>

## <a name="bots-with-webhooks-and-connectors"></a><span data-ttu-id="31726-130">Webhooks とコネクタを持つボット</span><span class="sxs-lookup"><span data-stu-id="31726-130">Bots with webhooks and connectors</span></span>

<span data-ttu-id="31726-131">Webhooks とコネクタは、ボットを Web サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="31726-131">Webhooks and connectors connect your bot to your web services.</span></span> <span data-ttu-id="31726-132">Webhooks とコネクタを使用すると、ワークフローや他の簡単なコマンドの作成など、基本的な操作を行う簡単なボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="31726-132">Using webhooks and connectors, you can create a simple bot for basic interaction, such as creating a workflow or other simple commands.</span></span> <span data-ttu-id="31726-133">これらは、作成したチームでのみ使用できます。会社のワークフローに固有の単純なプロセスを対象とします。</span><span class="sxs-lookup"><span data-stu-id="31726-133">They are available only in the team where you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="31726-134">詳細については [、「webhooks とコネクタについて」を参照してください](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="31726-134">For more information, see [what are webhooks and connectors](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="advantages-of-bots"></a><span data-ttu-id="31726-135">ボットの利点</span><span class="sxs-lookup"><span data-stu-id="31726-135">Advantages of bots</span></span>

<span data-ttu-id="31726-136">Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。</span><span class="sxs-lookup"><span data-stu-id="31726-136">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a team.</span></span> <span data-ttu-id="31726-137">各スコープは、会話ボットに固有の機会と課題を提供します。</span><span class="sxs-lookup"><span data-stu-id="31726-137">Each scope provides unique opportunities and challenges for your conversational bot.</span></span>

| <span data-ttu-id="31726-138">チャネル</span><span class="sxs-lookup"><span data-stu-id="31726-138">In a channel</span></span> | <span data-ttu-id="31726-139">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="31726-139">In a group chat</span></span> | <span data-ttu-id="31726-140">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="31726-140">In a one-to-one chat</span></span> |
| :-- | :-- | :-- |
| <span data-ttu-id="31726-141">大規模なリーチ</span><span class="sxs-lookup"><span data-stu-id="31726-141">Massive reach</span></span> | <span data-ttu-id="31726-142">メンバーの数が少ない</span><span class="sxs-lookup"><span data-stu-id="31726-142">Fewer members</span></span> | <span data-ttu-id="31726-143">従来の方法</span><span class="sxs-lookup"><span data-stu-id="31726-143">Traditional way</span></span> |
| <span data-ttu-id="31726-144">個々の対話を簡潔に</span><span class="sxs-lookup"><span data-stu-id="31726-144">Concise individual interactions</span></span> | <span data-ttu-id="31726-145">@mentionボットへのアクセス</span><span class="sxs-lookup"><span data-stu-id="31726-145">@mention to bot</span></span>  | <span data-ttu-id="31726-146">Q&ボット</span><span class="sxs-lookup"><span data-stu-id="31726-146">Q&A bots</span></span> |
| <span data-ttu-id="31726-147">@mentionボットへのアクセス</span><span class="sxs-lookup"><span data-stu-id="31726-147">@mention to bot</span></span> | <span data-ttu-id="31726-148">チャネルに似ている</span><span class="sxs-lookup"><span data-stu-id="31726-148">Similar to channel</span></span> | <span data-ttu-id="31726-149">ジョークを伝え、メモを取るボット</span><span class="sxs-lookup"><span data-stu-id="31726-149">Bots that tell jokes and take notes</span></span> |

### <a name="in-a-channel"></a><span data-ttu-id="31726-150">チャネル</span><span class="sxs-lookup"><span data-stu-id="31726-150">In a channel</span></span>

<span data-ttu-id="31726-151">チャネルには、最大 2,000 人までの複数のユーザー間のスレッド会話が含まれる。</span><span class="sxs-lookup"><span data-stu-id="31726-151">Channels contain threaded conversations between multiple people even up to two thousand.</span></span> <span data-ttu-id="31726-152">これにより、ボットに大量のリーチが生まれる可能性がありますが、個々のやり取りは簡潔である必要があります。</span><span class="sxs-lookup"><span data-stu-id="31726-152">This potentially gives your bot massive reach, but individual interactions must be concise.</span></span> <span data-ttu-id="31726-153">従来のマルチターン操作は機能しません。</span><span class="sxs-lookup"><span data-stu-id="31726-153">Traditional multi-turn interactions do not work.</span></span> <span data-ttu-id="31726-154">代わりに、対話型カードまたはタスク モジュールを使用するか、会話を 1 対 1 の会話に移動して多くの情報を収集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31726-154">Instead, you must look to use interactive cards or task modules, or move the conversation to a one-to-one conversation to collect lots of information.</span></span> <span data-ttu-id="31726-155">ボットにはメッセージへのアクセスのみ許可されます `@mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="31726-155">Your bot only has access to messages where it is `@mentioned`.</span></span> <span data-ttu-id="31726-156">会話から追加のメッセージを取得するには、Microsoft Graphおよび組織レベルのアクセス許可を使用します。</span><span class="sxs-lookup"><span data-stu-id="31726-156">You can retrieve additional messages from the conversation using Microsoft Graph and organization-level permissions.</span></span>

<span data-ttu-id="31726-157">ボットは、次の場合にチャネルで優れた機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="31726-157">Bots work better in a channel in the following cases:</span></span>

* <span data-ttu-id="31726-158">通知: ユーザーが追加情報を取得する対話型カードを提供します。</span><span class="sxs-lookup"><span data-stu-id="31726-158">Notifications, where you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="31726-159">アンケートやアンケートなどのフィードバック シナリオ。</span><span class="sxs-lookup"><span data-stu-id="31726-159">Feedback scenarios, such as polls and surveys.</span></span>
* <span data-ttu-id="31726-160">単一の要求または応答サイクルは対話を解決し、結果は会話の複数のメンバーに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="31726-160">Single request or response cycle resolves interactions and the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="31726-161">ソーシャルボットや楽しいボット。素晴らしい猫の画像を取得し、ランダムに勝者を選ぶなどです。</span><span class="sxs-lookup"><span data-stu-id="31726-161">Social or fun bots, where you get an awesome cat image, randomly pick a winner, and so on.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="31726-162">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="31726-162">In a group chat</span></span>

<span data-ttu-id="31726-163">グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。</span><span class="sxs-lookup"><span data-stu-id="31726-163">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="31726-164">チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。</span><span class="sxs-lookup"><span data-stu-id="31726-164">They tend to have fewer members than a channel and are more transient.</span></span> <span data-ttu-id="31726-165">チャネルと同様に、ボットはメッセージに直接アクセスできる `@mentioned` のみです。</span><span class="sxs-lookup"><span data-stu-id="31726-165">Similar to a channel, your bot only has access to messages where it is `@mentioned` directly.</span></span>

<span data-ttu-id="31726-166">チャネルでボットがうまく機能する場合は、グループ チャットの方がうまく機能します。</span><span class="sxs-lookup"><span data-stu-id="31726-166">In the cases where bots work better in a channel also work better in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="31726-167">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="31726-167">In a one-to-one chat</span></span>

<span data-ttu-id="31726-168">1 対 1 のチャットは、会話ボットがユーザーと対話する従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="31726-168">One-to-one chat is a traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="31726-169">1 対 1 の会話型ボットの例としては、Q&ボット、他のシステムでワークフローを開始するボット、ジョークを伝えるボット、メモを取るボットがあります。</span><span class="sxs-lookup"><span data-stu-id="31726-169">A few examples of one-to-one conversational bots are Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes.</span></span> <span data-ttu-id="31726-170">1 対 1 のチャットボットを作成する前に、会話ベースのインターフェイスが機能を提示する最適な方法であるかどうかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="31726-170">Before creating one-to-one chatbots, consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="disadvantages-of-bots"></a><span data-ttu-id="31726-171">ボットの欠点</span><span class="sxs-lookup"><span data-stu-id="31726-171">Disadvantages of bots</span></span>

<span data-ttu-id="31726-172">ボットとユーザーの間の広範なダイアログは、タスクを完了するための低速で複雑な方法です。</span><span class="sxs-lookup"><span data-stu-id="31726-172">An extensive dialog between your bot and the user is a slow and complex way to get a task completed.</span></span> <span data-ttu-id="31726-173">過剰なコマンド、特に広範なコマンドをサポートするボットは、ユーザーが成功または肯定的に表示されません。</span><span class="sxs-lookup"><span data-stu-id="31726-173">A bot that supports excessive commands, especially a broad range of commands, is not successful or viewed positively by users.</span></span>

### <a name="have-multi-turn-experiences-in-chat"></a><span data-ttu-id="31726-174">チャットでのマルチターン エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="31726-174">Have multi-turn experiences in chat</span></span>

<span data-ttu-id="31726-175">広範なダイアログでは、開発者が状態を維持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31726-175">An extensive dialog requires the developer to maintain state.</span></span> <span data-ttu-id="31726-176">この状態を終了するには、ユーザーがタイム アウトするか、[キャンセル] を選択する **必要があります**。</span><span class="sxs-lookup"><span data-stu-id="31726-176">To exit this state a user must either time-out or select **Cancel**.</span></span> <span data-ttu-id="31726-177">また、このプロセスは時間のかかっています。</span><span class="sxs-lookup"><span data-stu-id="31726-177">Also, the process is tedious.</span></span> <span data-ttu-id="31726-178">たとえば、次の会話シナリオを参照してください。</span><span class="sxs-lookup"><span data-stu-id="31726-178">For example, see the following conversation scenario:</span></span>

<span data-ttu-id="31726-179">ユーザー: Megan との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="31726-179">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="31726-180">ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。</span><span class="sxs-lookup"><span data-stu-id="31726-180">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="31726-181">ユーザー: Megan Bowen との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="31726-181">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="31726-182">ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?</span><span class="sxs-lookup"><span data-stu-id="31726-182">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="31726-183">ユーザー: 午後 1 時に。</span><span class="sxs-lookup"><span data-stu-id="31726-183">USER: 1:00 pm.</span></span>

<span data-ttu-id="31726-184">ボット: 何日のですか?</span><span class="sxs-lookup"><span data-stu-id="31726-184">BOT: On which day?</span></span>

### <a name="support-too-many-commands"></a><span data-ttu-id="31726-185">多くのコマンドをサポートする</span><span class="sxs-lookup"><span data-stu-id="31726-185">Support too many commands</span></span>

<span data-ttu-id="31726-186">現在のボット メニューには 6 つのコマンドしか表示されないので、それ以上のコマンドを頻度で使用する可能性は低い。</span><span class="sxs-lookup"><span data-stu-id="31726-186">As there are only six visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="31726-187">幅広いアシスタントの仕事と運賃を向上させようとするのではなく、特定の領域に深く入り込むボット。</span><span class="sxs-lookup"><span data-stu-id="31726-187">Bots that go deep into a specific area rather than trying to be a broad assistant work and fare better.</span></span>

### <a name="maintain-a-large-knowledge-base"></a><span data-ttu-id="31726-188">大規模なナレッジ ベースを維持する</span><span class="sxs-lookup"><span data-stu-id="31726-188">Maintain a large knowledge base</span></span>

<span data-ttu-id="31726-189">ボットの欠点の 1 つは、応答が未確認の大規模な取得ナレッジ ベースを維持することは困難である点です。</span><span class="sxs-lookup"><span data-stu-id="31726-189">One of the disadvantages of bots is that it is difficult to maintain a large retrieval knowledge base with unranked responses.</span></span> <span data-ttu-id="31726-190">ボットは、短く迅速なやり取りに最適で、回答を探している長いリストをふるいにかけない。</span><span class="sxs-lookup"><span data-stu-id="31726-190">Bots are best suited for short, quick interactions, and not sifting through long lists looking for an answer.</span></span>

## <a name="code-sample"></a><span data-ttu-id="31726-191">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="31726-191">Code sample</span></span>

|<span data-ttu-id="31726-192">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="31726-192">Sample name</span></span> | <span data-ttu-id="31726-193">説明</span><span class="sxs-lookup"><span data-stu-id="31726-193">Description</span></span> | <span data-ttu-id="31726-194">.NETCore</span><span class="sxs-lookup"><span data-stu-id="31726-194">.NETCore</span></span> | <span data-ttu-id="31726-195">Node.js</span><span class="sxs-lookup"><span data-stu-id="31726-195">Node.js</span></span> |
|----------------|-----------------|--------------|----------------|
| <span data-ttu-id="31726-196">Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="31726-196">Teams conversation bot</span></span> | <span data-ttu-id="31726-197">メッセージングおよび会話イベントの処理。</span><span class="sxs-lookup"><span data-stu-id="31726-197">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="31726-198">View</span><span class="sxs-lookup"><span data-stu-id="31726-198">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="31726-199">View</span><span class="sxs-lookup"><span data-stu-id="31726-199">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a><span data-ttu-id="31726-200">次の手順</span><span class="sxs-lookup"><span data-stu-id="31726-200">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="31726-201">ボットのアクティビティ ハンドラー</span><span class="sxs-lookup"><span data-stu-id="31726-201">Bot activity handlers</span></span>](~/bots/bot-basics.md)
