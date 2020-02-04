---
title: ユースケースをアプリ機能にマッピングする
author: clearab
description: アプリの配布方法を決定する
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5ebfa73df9b4f2c83533a33fbc6366c2c0ccffb4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674951"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="70001-103">ユースケースを teams アプリの機能にマッピングする</span><span class="sxs-lookup"><span data-stu-id="70001-103">Map your use cases to teams app capabilities</span></span>

<span data-ttu-id="70001-104">まだ使用していない場合は、その[ユースケース](~/concepts/design/map-use-cases.md)を慎重に検討してください。</span><span class="sxs-lookup"><span data-stu-id="70001-104">If you haven't already, make sure you've [considered your use cases](~/concepts/design/map-use-cases.md) carefully.</span></span> <span data-ttu-id="70001-105">また、アプリで使用できる[機能拡張ポイントと UI 要素](~/concepts/extensibility-points.md)について十分に理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="70001-105">You should also have a good understanding of the [extensibility points and UI elements](~/concepts/extensibility-points.md) available for your app.</span></span> <span data-ttu-id="70001-106">何を解決*しようとし*ている*か*を把握したら、その解決*方法*について考え始めます。</span><span class="sxs-lookup"><span data-stu-id="70001-106">Once you've figured out *what* your trying to solve, and *who* you're solving it for, it is time to start thinking about *how*.</span></span>

<span data-ttu-id="70001-107">以下に、一般的なシナリオと、それらを使用して正常に機能する機能および UI 要素をいくつか紹介します。</span><span class="sxs-lookup"><span data-stu-id="70001-107">Below you'll find some common scenarios, and a selection of extensibility points and UI elements that work well with them.</span></span> <span data-ttu-id="70001-108">これは、ユーザーや Teams プラットフォームで利用できる可能性の一部を理解するための完全なリストではありません。</span><span class="sxs-lookup"><span data-stu-id="70001-108">It isn't intended to be an exhaustive list, just to help you think through some of the possibilities available to you and the Teams platform.</span></span>

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a><span data-ttu-id="70001-109">外部システムのアイテムを作成、共有、および共同作業する</span><span class="sxs-lookup"><span data-stu-id="70001-109">Create, share and collaborate on items in an external system</span></span>

<span data-ttu-id="70001-110">Microsoft Teams 用アプリは、データを操作するための最適な方法であり、さまざまな統合ポイントから選択できます。</span><span class="sxs-lookup"><span data-stu-id="70001-110">App for Microsoft Teams are a great way to interact with your data, and there are a variety of integration points to choose from.</span></span>

* <span data-ttu-id="70001-111">検索コマンドを使用したメッセージング拡張機能-外部システムを検索し、結果を対話形式のカードとして共有します。</span><span class="sxs-lookup"><span data-stu-id="70001-111">Messaging extensions with search commands - Search external systems and share the results as an interactive card.</span></span>

* <span data-ttu-id="70001-112">アクションコマンドを含むメッセージング拡張機能-データストアに挿入する情報を収集するか、高度な検索を実行します。</span><span class="sxs-lookup"><span data-stu-id="70001-112">Messaging extensions with action commands - Collect information to insert into a data store or perform advanced searches.</span></span>

* <span data-ttu-id="70001-113">タブ-データを表示、操作、および共有するための組み込み web エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="70001-113">Tabs - Create embedded web experiences to view, work with, and share data.</span></span>

* <span data-ttu-id="70001-114">コネクタと web フック-データをにプッシュし、Teams クライアントからデータを送信するための簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="70001-114">Connectors and webhooks - A simple way to push data into, and send data out of the Teams client.</span></span>

* <span data-ttu-id="70001-115">タスクモジュール-対話型のモーダルフォーム。情報を収集または表示するために必要な場所。</span><span class="sxs-lookup"><span data-stu-id="70001-115">Task modules - Interactive modal forms from wherever you need them to collect or display information.</span></span>

## <a name="initiate-workflows-and-processes"></a><span data-ttu-id="70001-116">ワークフローとプロセスを開始する</span><span class="sxs-lookup"><span data-stu-id="70001-116">Initiate workflows and processes</span></span>

<span data-ttu-id="70001-117">外部システムでプロセスまたはワークフローをすばやく開始する方法が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="70001-117">Sometimes you just need a quick way to start a process or workflow in an external system.</span></span>

* <span data-ttu-id="70001-118">メッセージング拡張機能アクションコマンド-メッセージからトリガーし、ユーザーが web サービスにメッセージの内容をすばやく送信できるようにします。</span><span class="sxs-lookup"><span data-stu-id="70001-118">Messaging extensions action commands - Trigger from messages, allowing your users to quickly send the contents of a message to your web services.</span></span>

* <span data-ttu-id="70001-119">タスクモジュール-ワークフローを開始する前に情報を収集するタブ、ボット、またはメッセージング拡張機能から開きます。</span><span class="sxs-lookup"><span data-stu-id="70001-119">Task modules - Open them from a tab, a bot, or a messaging extension to collect information before initiating a workflow.</span></span>

* <span data-ttu-id="70001-120">話し言葉の bot-テキストとリッチカードを使用してユーザーと対話します。</span><span class="sxs-lookup"><span data-stu-id="70001-120">Conversational bots - Interact with your users through text and rich cards.</span></span>

* <span data-ttu-id="70001-121">送信 web フック-会話 bot 全体をビルドする必要がない場合に、単純なバック and 操作に適した選択。</span><span class="sxs-lookup"><span data-stu-id="70001-121">Outgoing webhooks - A good choice for a simple back-and-forth interaction when you don't need to build an entire conversational bot.</span></span>

## <a name="send-notifications-and-alerts"></a><span data-ttu-id="70001-122">通知と通知を送信する</span><span class="sxs-lookup"><span data-stu-id="70001-122">Send notifications and alerts</span></span>

<span data-ttu-id="70001-123">チーム内のユーザーに非同期通知と通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="70001-123">Send asynchronous notifications and alerts to your users in Teams.</span></span> <span data-ttu-id="70001-124">インタラクティブカードを使用して、よく使用される操作にすばやくアクセスし、追加情報へのリンクを提供します。</span><span class="sxs-lookup"><span data-stu-id="70001-124">Use interactive cards to provide quick access to commonly used actions and links to additional information.</span></span>

* <span data-ttu-id="70001-125">話し言葉のボット-グループ、チャネル、または個々のユーザーに予防的なメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="70001-125">Conversational bots - Send proactive messages to groups, channels, or individual users.</span></span>

* <span data-ttu-id="70001-126">受信 web フック & コネクタは、チャネルが受信メッセージをサブスクライブすることを許可します。</span><span class="sxs-lookup"><span data-stu-id="70001-126">Connectors & incoming webhooks - Allow a channel to subscribe to receive messages.</span></span> <span data-ttu-id="70001-127">コネクタを使用すると、ユーザーは構成ページを使用してサブスクリプションを調整できます。</span><span class="sxs-lookup"><span data-stu-id="70001-127">With a connector let users tailor the subscription with a configuration page.</span></span>

## <a name="ask-questions-and-get-answers"></a><span data-ttu-id="70001-128">質問と回答を得る</span><span class="sxs-lookup"><span data-stu-id="70001-128">Ask questions and get answers</span></span>

<span data-ttu-id="70001-129">ユーザーに質問があります。</span><span class="sxs-lookup"><span data-stu-id="70001-129">People have questions.</span></span> <span data-ttu-id="70001-130">多くの場合、他の場所に格納されている多くの回答があります。</span><span class="sxs-lookup"><span data-stu-id="70001-130">You've probably got a lot of the answers stored away somewhere.</span></span> <span data-ttu-id="70001-131">残念ながら、この2つを互いに接続することは非常に困難です。</span><span class="sxs-lookup"><span data-stu-id="70001-131">Unfortunately, its often quite difficult to connect the two together.</span></span>

* <span data-ttu-id="70001-132">話し言葉の bot-自然言語処理、AI、machine learning、すべての buzzwords。</span><span class="sxs-lookup"><span data-stu-id="70001-132">Conversational bots - Natural language processing, AI, machine learning, all the buzzwords.</span></span> <span data-ttu-id="70001-133">インテリジェントクラウドで提供される bot を使用して、ユーザーが必要な答えに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="70001-133">Use a bot powered by the intelligent cloud to connect your users to the answers they need.</span></span>

* <span data-ttu-id="70001-134">タブ-既存の web ポータルを Teams に埋め込む、または追加機能用のチーム固有のバージョンを作成する。</span><span class="sxs-lookup"><span data-stu-id="70001-134">Tabs - Embed your existing web portal in Teams, or create a Teams-specific version for added functionality.</span></span>

## <a name="get-social"></a><span data-ttu-id="70001-135">ソーシャルの取得</span><span class="sxs-lookup"><span data-stu-id="70001-135">Get social</span></span>

<span data-ttu-id="70001-136">コラボレーションプラットフォームは、本質的にソーシャルプラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="70001-136">A collaboration platform is inherently a social platform.</span></span> <span data-ttu-id="70001-137">クリエイティブ・サイドを無料にして、自分のワークプレースにおもしろいものを追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="70001-137">Let your creative side be free, and add some fun into your workplace.</span></span>

* <span data-ttu-id="70001-138">すべてとして、冗談を送信したり、称賛を与えたり、いくつかの絵文字を捨てたり、何らかの凝ったものを捨てたりします。</span><span class="sxs-lookup"><span data-stu-id="70001-138">All of them - Send jokes, give kudos, get some memes, toss out some emoji's or whatever else strikes your fancy.</span></span>

## <a name="anything-you-can-do-in-a-single-page-app-spa"></a><span data-ttu-id="70001-139">単一ページアプリ (SPA) で可能なすべての操作</span><span class="sxs-lookup"><span data-stu-id="70001-139">Anything you can do in a Single Page App (SPA)</span></span>

<span data-ttu-id="70001-140">タブは、埋め込み web ページです。</span><span class="sxs-lookup"><span data-stu-id="70001-140">Tabs are embedded web pages.</span></span> <span data-ttu-id="70001-141">SPA で可能なことはほぼすべて、Teams のタブで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="70001-141">Pretty much anything you can do in a SPA, you can do in a tab in Teams.</span></span> <span data-ttu-id="70001-142">[スコープグループ] タブと [チャネル] タブが共有エクスペリエンス用であることに注意してください。個人用タブは、個人のエクスペリエンス。</span><span class="sxs-lookup"><span data-stu-id="70001-142">Just be sure to pay attention to scope - group and channel tabs are for shared experiences, personal tabs are for ... personal experiences.</span></span> <span data-ttu-id="70001-143">チームの目的の一覧は [チャネル] タブに表示されます。ユーザーの一覧は [個人用] タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="70001-143">The team's list of stuff goes on the channel tab, the list of your stuff goes in the personal tab.</span></span>

## <a name="start-small"></a><span data-ttu-id="70001-144">開始 (小)</span><span class="sxs-lookup"><span data-stu-id="70001-144">Start small</span></span>

<span data-ttu-id="70001-145">どこから始めるかがわからない場合</span><span class="sxs-lookup"><span data-stu-id="70001-145">Not sure where to start?</span></span> <span data-ttu-id="70001-146">利用可能なすばらしいさまざまなオプションを使用することによって、多少の負荷がかかっていませんか。</span><span class="sxs-lookup"><span data-stu-id="70001-146">Feeling a bit overwhelmed with the awesome variety of options available to you?</span></span> <span data-ttu-id="70001-147">Fret しないでください。アプリのコア機能を選択し、そこで開始します。</span><span class="sxs-lookup"><span data-stu-id="70001-147">Don't fret, choose a core feature of your app and start there.</span></span> <span data-ttu-id="70001-148">Teams のさまざまなコンテキストを通じて情報の流れについての感じが得られると、より複雑な対話を図にする方がはるかに簡単になります。</span><span class="sxs-lookup"><span data-stu-id="70001-148">Once you get a feel for the flow of information through the various contexts in Teams, it will be a lot simpler to picture a more complex interaction.</span></span>

## <a name="putting-it-all-together"></a><span data-ttu-id="70001-149">すべてをまとめる</span><span class="sxs-lookup"><span data-stu-id="70001-149">Putting it all together</span></span>

<span data-ttu-id="70001-150">そのため、最適なアプリは、通常、複数の機能を組み合わせ、適切なコンテキストのユーザーに適切な機能を適切なタイミングで移行するアプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="70001-150">That being said, the best apps usually combine multiple features, creating an app that engages users in the right context with the right functionality at the right time.</span></span> <span data-ttu-id="70001-151">適切なワンツーワンの会話があるとしても、その機能をチームに追加する必要があるとは限らないため、そのような場所には機能を強制しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="70001-151">Don't try to force functionality into a place it doesn't belong - just because you've got a good one-to-one conversational bot doesn't mean you should just add it to a team.</span></span> <span data-ttu-id="70001-152">さまざまな機能拡張ポイントはさまざまな点に適しています。その強みに対してプレイすることで、アプリが輝きます。</span><span class="sxs-lookup"><span data-stu-id="70001-152">Different extensibility points are good for different things; play to their strengths and your app will shine.</span></span>
