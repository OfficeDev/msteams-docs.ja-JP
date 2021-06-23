---
title: ボットと SDK
author: surbhigupta
description: ボットと SDK は、Microsoft Teams。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: b1b8f18a457c45a7b0be6ccf6a1d7328d9c50027
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069023"
---
# <a name="bots-and-sdks"></a><span data-ttu-id="0a9e7-103">ボットと SDK</span><span class="sxs-lookup"><span data-stu-id="0a9e7-103">Bots and SDKs</span></span>

<span data-ttu-id="0a9e7-104">このページで動作するボットをMicrosoft Teams、次のいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-104">To create a bot that works in Microsoft Teams, you can use one of the following:</span></span>
* <span data-ttu-id="0a9e7-105">SDK に基Microsoft Bot Frameworkボット。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-105">An existing bot built on the Microsoft Bot Framework SDK.</span></span>
* <span data-ttu-id="0a9e7-106">Power Virtual Agentsチャットボット サービス。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-106">Power Virtual Agents chatbot service.</span></span>
* <span data-ttu-id="0a9e7-107">Webhooks とコネクタ。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-107">Webhooks and connectors.</span></span>

## <a name="bots-and-the-microsoft-bot-framework"></a><span data-ttu-id="0a9e7-108">ボットとMicrosoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="0a9e7-108">Bots and the Microsoft Bot Framework</span></span>

<span data-ttu-id="0a9e7-109">ボットTeamsは、次の 3 つの要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-109">Your Teams bot consists of the following three elements:</span></span>

* <span data-ttu-id="0a9e7-110">お客様がホストし、公開している Web サービス。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-110">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="0a9e7-111">Bot Framework へのボットの登録。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-111">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="0a9e7-112">アプリ マニフェストを含む Teams アプリ パッケージ。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-112">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="0a9e7-113">これは、ユーザーがボット サービス経由でルーティングTeamsクライアントをインストールして Web サービスに接続する方法です。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-113">This is what your users install and connect the Teams client to your web service, routed through the bot service.</span></span>

<span data-ttu-id="0a9e7-114">ボット [フレームワークは、](https://dev.botframework.com/) カスタム スクリプト、C#、Python、および JavaScript をJavaボットを作成するために使用される豊富な SDK です。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-114">The [Bot Framework](https://dev.botframework.com/) is a rich SDK used to create bots using C#, Java, Python, and JavaScript.</span></span> <span data-ttu-id="0a9e7-115">ボット フレームワークに基づくボットが既に存在する場合は、ボットフレームワークで動作Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-115">If you already have a bot that is based on the Bot Framework, you can easily modify it to work in Microsoft Teams.</span></span> <span data-ttu-id="0a9e7-116">SDK を利用C#またはNode.jsを使用 [します](/microsoftteams/platform/#pivot=sdk-tools)。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-116">Use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="0a9e7-117">これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-117">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="0a9e7-118">コネクタ カードのような特殊なカードOffice 365使用します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-118">Use specialized card types like the Office 365 connector card.</span></span>
* <span data-ttu-id="0a9e7-119">アクティビティTeams固有のチャネル データを設定します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-119">Set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="0a9e7-120">メッセージング拡張要求を処理する。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-120">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a9e7-121">任意の web プログラミング Teamsアプリを開発し[、Bot Framework REST API を直接呼び出](/bot-framework/rest-api/bot-framework-rest-overview)します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-121">You can develop Teams apps in any web programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly.</span></span> <span data-ttu-id="0a9e7-122">ただし、すべてのケースでトークン処理を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-122">But you must perform token handling in all cases.</span></span>

> [!TIP]
> <span data-ttu-id="0a9e7-123">TeamsApp Studio を使用すると、アプリ マニフェストを作成および構成し、ボット フレームワークで Web サービスをボットとして登録できます。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-123">Teams App Studio helps you create and configure your app manifest, and register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="0a9e7-124">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-124">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="0a9e7-125">詳細については、「アプリ Studio[の使用Teams」を参照してください](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-125">For more information, see [getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="bots-and-the-microsoft-power-virtual-agents"></a><span data-ttu-id="0a9e7-126">ボットと Microsoft Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="0a9e7-126">Bots and the Microsoft Power Virtual Agents</span></span>

<span data-ttu-id="0a9e7-127">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft Power プラットフォームとボット フレームワーク上に構築されたチャットボット サービスです。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-127">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a chatbot service built on the Microsoft Power platform and Bot Framework.</span></span> <span data-ttu-id="0a9e7-128">Power Virtual Agent 開発プロセスでは、ガイド付き、コードなし、グラフィカル インターフェイスのアプローチを使用して、チーム メンバーがインテリジェントな仮想エージェントを簡単に作成および維持できます。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-128">The Power Virtual Agent development process uses a guided, no-code, and graphical interface approach that empowers your team members to easily create and maintain an intelligent virtual agent.</span></span> <span data-ttu-id="0a9e7-129">ポータルでチャットボットを作成[Power Virtual Agents、](https://powervirtualagents.microsoft.com)チャットボットとチャットボットを簡単に統合[Teams。](how-to/add-power-virtual-agents-bot-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="0a9e7-129">After creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate it with Teams](how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="0a9e7-130">開始方法の詳細については、「ドキュメント」[をPower Virtual Agentsしてください](/power-virtual-agents)。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-130">For more information on getting started, see [Power Virtual Agents documentation](/power-virtual-agents).</span></span>

## <a name="bots-and-webhooks-and-connectors"></a><span data-ttu-id="0a9e7-131">ボットと Webhooks とコネクタ</span><span class="sxs-lookup"><span data-stu-id="0a9e7-131">Bots and webhooks and connectors</span></span>

<span data-ttu-id="0a9e7-132">Webhooks とコネクタは、ボットを Web サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-132">Webhooks and connectors connect your bot to your web services.</span></span> <span data-ttu-id="0a9e7-133">Webhooks とコネクタを使用すると、ワークフローや他の簡単なコマンドの作成など、基本的な操作を行う簡単なボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-133">Using webhooks and connectors, you can create a simple bot for basic interaction, such as creating a workflow or other simple commands.</span></span> <span data-ttu-id="0a9e7-134">これらは、作成したチームでのみ使用できます。会社のワークフローに固有の単純なプロセスを対象とします。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-134">They are available only in the team where you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="0a9e7-135">詳細については [、「webhooks とコネクタについて」を参照してください](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-135">For more information, see [what are webhooks and connectors](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="advantages-of-bots"></a><span data-ttu-id="0a9e7-136">ボットの利点</span><span class="sxs-lookup"><span data-stu-id="0a9e7-136">Advantages of bots</span></span>

<span data-ttu-id="0a9e7-137">Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-137">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a team.</span></span> <span data-ttu-id="0a9e7-138">各スコープは、会話ボットに固有の機会と課題を提供します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-138">Each scope provides unique opportunities and challenges for your conversational bot.</span></span>

| <span data-ttu-id="0a9e7-139">チャネル</span><span class="sxs-lookup"><span data-stu-id="0a9e7-139">In a channel</span></span> | <span data-ttu-id="0a9e7-140">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="0a9e7-140">In a group chat</span></span> | <span data-ttu-id="0a9e7-141">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="0a9e7-141">In a one-to-one chat</span></span> |
| :-- | :-- | :-- |
| <span data-ttu-id="0a9e7-142">大規模なリーチ</span><span class="sxs-lookup"><span data-stu-id="0a9e7-142">Massive reach</span></span> | <span data-ttu-id="0a9e7-143">メンバーの数が少ない</span><span class="sxs-lookup"><span data-stu-id="0a9e7-143">Fewer members</span></span> | <span data-ttu-id="0a9e7-144">従来の方法</span><span class="sxs-lookup"><span data-stu-id="0a9e7-144">Traditional way</span></span> |
| <span data-ttu-id="0a9e7-145">個々の対話を簡潔に</span><span class="sxs-lookup"><span data-stu-id="0a9e7-145">Concise individual interactions</span></span> | <span data-ttu-id="0a9e7-146">@mentionボットへのアクセス</span><span class="sxs-lookup"><span data-stu-id="0a9e7-146">@mention to bot</span></span>  | <span data-ttu-id="0a9e7-147">Q&ボット</span><span class="sxs-lookup"><span data-stu-id="0a9e7-147">Q&A bots</span></span> |
| <span data-ttu-id="0a9e7-148">@mentionボットへのアクセス</span><span class="sxs-lookup"><span data-stu-id="0a9e7-148">@mention to bot</span></span> | <span data-ttu-id="0a9e7-149">チャネルに似ている</span><span class="sxs-lookup"><span data-stu-id="0a9e7-149">Similar to channel</span></span> | <span data-ttu-id="0a9e7-150">ジョークを伝え、メモを取るボット</span><span class="sxs-lookup"><span data-stu-id="0a9e7-150">Bots that tell jokes and take notes</span></span> |

### <a name="in-a-channel"></a><span data-ttu-id="0a9e7-151">チャネル</span><span class="sxs-lookup"><span data-stu-id="0a9e7-151">In a channel</span></span>

<span data-ttu-id="0a9e7-152">チャネルには、最大 2,000 人までの複数のユーザー間のスレッド会話が含まれる。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-152">Channels contain threaded conversations between multiple people even up to two thousand.</span></span> <span data-ttu-id="0a9e7-153">これにより、ボットに大量のリーチが生まれる可能性がありますが、個々のやり取りは簡潔である必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-153">This potentially gives your bot massive reach, but individual interactions must be concise.</span></span> <span data-ttu-id="0a9e7-154">従来のマルチターン操作は機能しません。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-154">Traditional multi-turn interactions do not work.</span></span> <span data-ttu-id="0a9e7-155">代わりに、対話型カードまたはタスク モジュールを使用するか、会話を 1 対 1 の会話に移動して多くの情報を収集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-155">Instead, you must look to use interactive cards or task modules, or move the conversation to a one-to-one conversation to collect lots of information.</span></span> <span data-ttu-id="0a9e7-156">ボットにはメッセージへのアクセスのみ許可されます `@mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-156">Your bot only has access to messages where it is `@mentioned`.</span></span> <span data-ttu-id="0a9e7-157">会話から追加のメッセージを取得するには、Microsoft Graphおよび組織レベルのアクセス許可を使用します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-157">You can retrieve additional messages from the conversation using Microsoft Graph and organization-level permissions.</span></span>

<span data-ttu-id="0a9e7-158">ボットは、次の場合にチャネルで優れた機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-158">Bots work better in a channel in the following cases:</span></span>

* <span data-ttu-id="0a9e7-159">通知: ユーザーが追加情報を取得する対話型カードを提供します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-159">Notifications, where you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="0a9e7-160">アンケートやアンケートなどのフィードバック シナリオ。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-160">Feedback scenarios, such as polls and surveys.</span></span>
* <span data-ttu-id="0a9e7-161">単一の要求または応答サイクルは対話を解決し、結果は会話の複数のメンバーに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-161">Single request or response cycle resolves interactions and the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="0a9e7-162">ソーシャルボットや楽しいボット。素晴らしい猫の画像を取得し、ランダムに勝者を選ぶなどです。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-162">Social or fun bots, where you get an awesome cat image, randomly pick a winner, and so on.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="0a9e7-163">グループ チャット</span><span class="sxs-lookup"><span data-stu-id="0a9e7-163">In a group chat</span></span>

<span data-ttu-id="0a9e7-164">グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-164">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="0a9e7-165">チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-165">They tend to have fewer members than a channel and are more transient.</span></span> <span data-ttu-id="0a9e7-166">チャネルと同様に、ボットはメッセージに直接アクセスできる `@mentioned` のみです。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-166">Similar to a channel, your bot only has access to messages where it is `@mentioned` directly.</span></span>

<span data-ttu-id="0a9e7-167">チャネルでボットがうまく機能する場合は、グループ チャットの方がうまく機能します。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-167">In the cases where bots work better in a channel also work better in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="0a9e7-168">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="0a9e7-168">In a one-to-one chat</span></span>

<span data-ttu-id="0a9e7-169">1 対 1 のチャットは、会話ボットがユーザーと対話する従来の方法です。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-169">One-to-one chat is a traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="0a9e7-170">1 対 1 の会話型ボットの例としては、Q&ボット、他のシステムでワークフローを開始するボット、ジョークを伝えるボット、メモを取るボットがあります。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-170">A few examples of one-to-one conversational bots are Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes.</span></span> <span data-ttu-id="0a9e7-171">1 対 1 のチャットボットを作成する前に、会話ベースのインターフェイスが機能を提示する最適な方法であるかどうかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-171">Before creating one-to-one chatbots, consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="disadvantages-of-bots"></a><span data-ttu-id="0a9e7-172">ボットの欠点</span><span class="sxs-lookup"><span data-stu-id="0a9e7-172">Disadvantages of bots</span></span>

<span data-ttu-id="0a9e7-173">ボットとユーザーの間の広範なダイアログは、タスクを完了するための低速で複雑な方法です。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-173">An extensive dialog between your bot and the user is a slow and complex way to get a task completed.</span></span> <span data-ttu-id="0a9e7-174">過剰なコマンド、特に広範なコマンドをサポートするボットは、ユーザーが成功または肯定的に表示されません。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-174">A bot that supports excessive commands, especially a broad range of commands, is not successful or viewed positively by users.</span></span>

### <a name="have-multi-turn-experiences-in-chat"></a><span data-ttu-id="0a9e7-175">チャットでのマルチターン エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="0a9e7-175">Have multi-turn experiences in chat</span></span>

<span data-ttu-id="0a9e7-176">広範なダイアログでは、開発者が状態を維持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-176">An extensive dialog requires the developer to maintain state.</span></span> <span data-ttu-id="0a9e7-177">この状態を終了するには、ユーザーがタイム アウトするか、[キャンセル] を選択する **必要があります**。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-177">To exit this state a user must either time-out or select **Cancel**.</span></span> <span data-ttu-id="0a9e7-178">また、このプロセスは時間のかかっています。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-178">Also, the process is tedious.</span></span> <span data-ttu-id="0a9e7-179">たとえば、次の会話シナリオを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-179">For example, see the following conversation scenario:</span></span>

<span data-ttu-id="0a9e7-180">ユーザー: Megan との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-180">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="0a9e7-181">ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-181">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="0a9e7-182">ユーザー: Megan Bowen との会議をスケジュールして。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-182">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="0a9e7-183">ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?</span><span class="sxs-lookup"><span data-stu-id="0a9e7-183">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="0a9e7-184">ユーザー: 午後 1 時に。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-184">USER: 1:00 pm.</span></span>

<span data-ttu-id="0a9e7-185">ボット: 何日のですか?</span><span class="sxs-lookup"><span data-stu-id="0a9e7-185">BOT: On which day?</span></span>

### <a name="support-too-many-commands"></a><span data-ttu-id="0a9e7-186">多くのコマンドをサポートする</span><span class="sxs-lookup"><span data-stu-id="0a9e7-186">Support too many commands</span></span>

<span data-ttu-id="0a9e7-187">現在のボット メニューには 6 つのコマンドしか表示されないので、それ以上のコマンドを頻度で使用する可能性は低い。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-187">As there are only six visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="0a9e7-188">幅広いアシスタントの仕事と運賃を向上させようとするのではなく、特定の領域に深く入り込むボット。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-188">Bots that go deep into a specific area rather than trying to be a broad assistant work and fare better.</span></span>

### <a name="maintain-a-large-knowledge-base"></a><span data-ttu-id="0a9e7-189">大規模なナレッジ ベースを維持する</span><span class="sxs-lookup"><span data-stu-id="0a9e7-189">Maintain a large knowledge base</span></span>

<span data-ttu-id="0a9e7-190">ボットの欠点の 1 つは、応答が未確認の大規模な取得ナレッジ ベースを維持することは困難である点です。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-190">One of the disadvantages of bots is that it is difficult to maintain a large retrieval knowledge base with unranked responses.</span></span> <span data-ttu-id="0a9e7-191">ボットは、短く迅速なやり取りに最適で、回答を探している長いリストをふるいにかけない。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-191">Bots are best suited for short, quick interactions, and not sifting through long lists looking for an answer.</span></span>

## <a name="code-sample"></a><span data-ttu-id="0a9e7-192">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="0a9e7-192">Code sample</span></span>

|<span data-ttu-id="0a9e7-193">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="0a9e7-193">Sample name</span></span> | <span data-ttu-id="0a9e7-194">説明</span><span class="sxs-lookup"><span data-stu-id="0a9e7-194">Description</span></span> | <span data-ttu-id="0a9e7-195">.NETCore</span><span class="sxs-lookup"><span data-stu-id="0a9e7-195">.NETCore</span></span> | <span data-ttu-id="0a9e7-196">Node.js</span><span class="sxs-lookup"><span data-stu-id="0a9e7-196">Node.js</span></span> |
|----------------|-----------------|--------------|----------------|
| <span data-ttu-id="0a9e7-197">Teams 会話ボット</span><span class="sxs-lookup"><span data-stu-id="0a9e7-197">Teams conversation bot</span></span> | <span data-ttu-id="0a9e7-198">メッセージングおよび会話イベントの処理。</span><span class="sxs-lookup"><span data-stu-id="0a9e7-198">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="0a9e7-199">View</span><span class="sxs-lookup"><span data-stu-id="0a9e7-199">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="0a9e7-200">View</span><span class="sxs-lookup"><span data-stu-id="0a9e7-200">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a><span data-ttu-id="0a9e7-201">次の手順</span><span class="sxs-lookup"><span data-stu-id="0a9e7-201">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a9e7-202">ボットのアクティビティ ハンドラー</span><span class="sxs-lookup"><span data-stu-id="0a9e7-202">Bot activity handlers</span></span>](~/bots/bot-basics.md)
