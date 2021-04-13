---
title: 使用例を Teams アプリの機能にマップする
author: clearab
description: 適切なアプリスコープを選択する
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3ade254d4042e80ea13201bd5936fd6bd326a0b2
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654301"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="150ca-103">使用例を Teams アプリの機能にマップする</span><span class="sxs-lookup"><span data-stu-id="150ca-103">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="150ca-104">ユーザーが *誰で、* どのような問題を解決するかが特定された後、問題を解決する *方法を決定* する必要があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-104">After you have identified *who* the user is and *what* problem you will solve, it is time to decide *how* to solve the problem.</span></span> <span data-ttu-id="150ca-105">使用 *例* を *理解* し、Teams アプリの機能にマッピングするプロセスを完了するユーザー、処理、処理方法。 </span><span class="sxs-lookup"><span data-stu-id="150ca-105">The *who*, *what*, and *how* completes the process of understanding and mapping your use cases to Teams app capabilities.</span></span> <span data-ttu-id="150ca-106">ユーザーからクエリに対して受け取った応答に基づいてアプリの範囲を定義し、アプリの構築に最適な機能を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-106">You need to define the scope of the app based on the responses you have received from the user to your queries, and then decide which capability is best suited to build your app.</span></span>

> [!NOTE]
> <span data-ttu-id="150ca-107">アプリで使用できるエントリ ポイントと [UI](../../concepts/extensibility-points.md) 要素について理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-107">You must have a good understanding of the [entry points and UI elements](../../concepts/extensibility-points.md) available for your app.</span></span> <span data-ttu-id="150ca-108">また、使用例を慎重に [検討する必要](../../concepts/design/understand-use-cases.md) があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-108">You must also make sure that you [considered your use cases](../../concepts/design/understand-use-cases.md) carefully.</span></span>

## <a name="choose-the-correct-scope-for-your-app"></a><span data-ttu-id="150ca-109">アプリの正しいスコープを選択する</span><span class="sxs-lookup"><span data-stu-id="150ca-109">Choose the correct scope for your app</span></span>

<span data-ttu-id="150ca-110">アプリのスコープを選択する際は、次の点を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="150ca-110">While choosing the app scope, consider the following:</span></span>

* <span data-ttu-id="150ca-111">アプリはスコープ間で存在できます。</span><span class="sxs-lookup"><span data-stu-id="150ca-111">An app can exist across scopes.</span></span>
* <span data-ttu-id="150ca-112">メッセージング拡張機能などのアプリ機能は、スコープ間でユーザーをフォローします。</span><span class="sxs-lookup"><span data-stu-id="150ca-112">App capabilities, such as messaging extensions, follow users across scopes.</span></span>
* <span data-ttu-id="150ca-113">多くの場合、ユーザーは Teams またはチャネルにアプリを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-113">Users are often hesitant to add apps to Teams or channels.</span></span>
* <span data-ttu-id="150ca-114">ゲスト ユーザーは、Teams またはチャネルで公開されているコンテンツにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="150ca-114">Guest users can access content exposed in Teams or channels.</span></span>

<span data-ttu-id="150ca-115">次の内容に応じて、アプリの個人用スコープとチームスコープまたはチャネル スコープを選択できます。</span><span class="sxs-lookup"><span data-stu-id="150ca-115">You can choose between personal scope and team or channel scope for your app depending on the following:</span></span>

* <span data-ttu-id="150ca-116">個人範囲を選択する場合は、次のような質問に答えます。</span><span class="sxs-lookup"><span data-stu-id="150ca-116">For selecting personal scope, answer questions, such as:</span></span>
  * <span data-ttu-id="150ca-117">プライバシーなどの理由で必要なアプリとの 1 対 1 のやり取りはありますか?</span><span class="sxs-lookup"><span data-stu-id="150ca-117">Are there one-on-one interactions with the app required for privacy or other reasons?</span></span> <span data-ttu-id="150ca-118">たとえば、休暇残高などの個人情報を確認します。</span><span class="sxs-lookup"><span data-stu-id="150ca-118">For example, checking leave balance or other private information.</span></span>
  * <span data-ttu-id="150ca-119">一般的な Teams を持てない可能性があるユーザー間で共同作業を行う必要がありますか?</span><span class="sxs-lookup"><span data-stu-id="150ca-119">Is there going to be collaboration among users who might not have any common Teams?</span></span> <span data-ttu-id="150ca-120">たとえば、会社で今後の組織全体のイベントを見つけるなどです。</span><span class="sxs-lookup"><span data-stu-id="150ca-120">For example, finding upcoming organization wide events in a company.</span></span>
  * <span data-ttu-id="150ca-121">Teams アプリエクスペリエンス全体を通じてユーザーに送信する必要がある、カスタマイズされた通知やメッセージはありますか?</span><span class="sxs-lookup"><span data-stu-id="150ca-121">Are there any personalized notifications or messages that will need to be sent to a user throughout the Teams app experience?</span></span> <span data-ttu-id="150ca-122">たとえば、承認または登録のリマインダーです。</span><span class="sxs-lookup"><span data-stu-id="150ca-122">For example, reminders for approvals or registrations.</span></span>

* <span data-ttu-id="150ca-123">チームまたはチャネルの範囲を選択する場合は、次のような質問に答えます。</span><span class="sxs-lookup"><span data-stu-id="150ca-123">For selecting team or channel scope, answer questions, such as:</span></span> 
  * <span data-ttu-id="150ca-124">タブまたはボットを介してアプリによって提示される情報は、チーム内のほとんどのメンバーにとって関連性が高く有用ですか?</span><span class="sxs-lookup"><span data-stu-id="150ca-124">Is the information presented by the app, either in tab or through a bot, relevant and useful for most members in a Team?</span></span> <span data-ttu-id="150ca-125">たとえば、Scrum アプリです。</span><span class="sxs-lookup"><span data-stu-id="150ca-125">For example, Scrum app.</span></span>
  * <span data-ttu-id="150ca-126">アプリのコンテキストは、追加するチームによって変わる可能性がありますか?</span><span class="sxs-lookup"><span data-stu-id="150ca-126">Could the app’s context change depending on the team in which it is added to?</span></span> <span data-ttu-id="150ca-127">たとえば、Planner のタスクは、チームごとに異なります。</span><span class="sxs-lookup"><span data-stu-id="150ca-127">For example, Planner’s tasks are different in different teams.</span></span> 
  * <span data-ttu-id="150ca-128">共同作業が必要なペルサのすべてのメンバーが 1 つのチームの一部である可能性はありますか?</span><span class="sxs-lookup"><span data-stu-id="150ca-128">Is it possible that all members in a persona who need to collaborate are a part of a single team?</span></span> <span data-ttu-id="150ca-129">たとえば、チケットで作業しているエージェントなどです。</span><span class="sxs-lookup"><span data-stu-id="150ca-129">For example, agents working on a ticket.</span></span>

<span data-ttu-id="150ca-130">次のシナリオでは、Teams アプリの機能に合ったエントリ ポイントと UI 要素の選択について説明します。</span><span class="sxs-lookup"><span data-stu-id="150ca-130">The following scenarios will guide you in understanding the selection of entry points and UI elements that work well with Teams app capabilities:</span></span>

> [!NOTE]
> <span data-ttu-id="150ca-131">これは網羅的なリストではありません。しかし、利用可能な可能性の一部を考えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="150ca-131">It is not an exhaustive list, but will help you think through some of the possibilities available to you.</span></span>

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a><span data-ttu-id="150ca-132">外部システムのアイテムを作成、共有、および共同作業する</span><span class="sxs-lookup"><span data-stu-id="150ca-132">Create, share, and collaborate on items in an external system</span></span>

<span data-ttu-id="150ca-133">Microsoft Teams 用アプリは、データを操作するための最適な方法であり、さまざまな統合ポイントから選択できます。</span><span class="sxs-lookup"><span data-stu-id="150ca-133">App for Microsoft Teams is a great way to interact with your data and there are a variety of integration points to choose from.</span></span>

* <span data-ttu-id="150ca-134">**検索コマンドを使用したメッセージング拡張機能**: 外部システムを検索し、結果を対話型カードとして共有します。</span><span class="sxs-lookup"><span data-stu-id="150ca-134">**Messaging extensions with search commands**: Search external systems and share the results as an interactive card.</span></span>

* <span data-ttu-id="150ca-135">**アクション コマンドを使用したメッセージング拡張機能**: データ ストアに挿入する情報を収集するか、高度な検索を実行します。</span><span class="sxs-lookup"><span data-stu-id="150ca-135">**Messaging extensions with action commands**: Collect information to insert into a data store or perform advanced searches.</span></span>

* <span data-ttu-id="150ca-136">**タブ**: データを表示、処理、共有する埋め込み Web エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="150ca-136">**Tabs**: Create embedded web experiences to view, work with and share data.</span></span>

* <span data-ttu-id="150ca-137">**コネクタと Webhook:** Teams クライアントからデータをプッシュしてデータを送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="150ca-137">**Connectors and webhooks**: A simple way to push data and send data out of the Teams client.</span></span>

* <span data-ttu-id="150ca-138">**タスク モジュール**: 対話型モーダル フォームは、情報を収集または表示するために必要な場所から提供されます。</span><span class="sxs-lookup"><span data-stu-id="150ca-138">**Task modules**: Interactive modal forms from wherever you need them to collect or display information.</span></span>

## <a name="initiate-workflows-and-processes"></a><span data-ttu-id="150ca-139">ワークフローとプロセスの開始</span><span class="sxs-lookup"><span data-stu-id="150ca-139">Initiate workflows and processes</span></span>

<span data-ttu-id="150ca-140">場合によっては、外部システムでプロセスまたはワークフローを簡単に開始する方法が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-140">Sometimes you just need a quick way to start a process or workflow in an external system.</span></span>

* <span data-ttu-id="150ca-141">**メッセージング拡張機能アクション コマンド**: メッセージからトリガーし、ユーザーはメッセージの内容をすばやく Web サービスに送信できます。</span><span class="sxs-lookup"><span data-stu-id="150ca-141">**Messaging extensions action commands**: Trigger from messages, allowing your users to quickly send the contents of a message to your web services.</span></span>

* <span data-ttu-id="150ca-142">**タスク モジュール**: タブ、ボット、またはメッセージング拡張機能から開き、ワークフローを開始する前に情報を収集します。</span><span class="sxs-lookup"><span data-stu-id="150ca-142">**Task modules**: Open them from a tab, a bot, or a messaging extension to collect information before initiating a workflow.</span></span>

* <span data-ttu-id="150ca-143">**会話型ボット**: テキストとリッチ カードを使用してユーザーと対話します。</span><span class="sxs-lookup"><span data-stu-id="150ca-143">**Conversational bots**: Interact with your users through text and rich cards.</span></span>

* <span data-ttu-id="150ca-144">**送信 webhooks**: 会話型ボット全体を構築する必要がない場合に、簡単なやり取りを行う場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="150ca-144">**Outgoing webhooks**: A good choice for a simple back-and-forth interaction when you don't need to build an entire conversational bot.</span></span>

## <a name="send-notifications-and-alerts"></a><span data-ttu-id="150ca-145">通知と通知の送信</span><span class="sxs-lookup"><span data-stu-id="150ca-145">Send notifications and alerts</span></span>

<span data-ttu-id="150ca-146">Teams のユーザーに非同期通知と通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="150ca-146">Send asynchronous notifications and alerts to your users in Teams.</span></span> <span data-ttu-id="150ca-147">対話型カードを使用して、一般的に使用されるアクションや追加情報へのリンクにすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="150ca-147">Use interactive cards to provide quick access to commonly used actions and links to additional information.</span></span>

* <span data-ttu-id="150ca-148">**会話型ボット**: グループ、チャネル、または個々のユーザーにプロアクティブ メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="150ca-148">**Conversational bots**: Send proactive messages to groups, channels, or individual users.</span></span>

* <span data-ttu-id="150ca-149">**コネクタと受信 Webhooks**: チャネルがメッセージを受信するためにサブスクライブを許可します。</span><span class="sxs-lookup"><span data-stu-id="150ca-149">**Connectors and incoming webhooks**: Permit a channel to subscribe to receive messages.</span></span> <span data-ttu-id="150ca-150">コネクタを使用すると、ユーザーは構成ページを使用してサブスクリプションを調整できます。</span><span class="sxs-lookup"><span data-stu-id="150ca-150">A connector lets users tailor the subscription with a configuration page.</span></span>

## <a name="ask-questions-and-get-answers"></a><span data-ttu-id="150ca-151">質問をして答えを得る</span><span class="sxs-lookup"><span data-stu-id="150ca-151">Ask questions and get answers</span></span>

<span data-ttu-id="150ca-152">人々は質問を持っているし、おそらくどこかに保存された答えの多くを得た。</span><span class="sxs-lookup"><span data-stu-id="150ca-152">People have questions and you probably got a lot of the answers stored away somewhere.</span></span> <span data-ttu-id="150ca-153">残念ながら、多くの場合、この 2 つを接続するのは非常に困難です。</span><span class="sxs-lookup"><span data-stu-id="150ca-153">Unfortunately, it's often quite difficult to connect the two.</span></span>

* <span data-ttu-id="150ca-154">**会話ボット**: 自然言語処理、AI、機械学習、およびすべての流行語。</span><span class="sxs-lookup"><span data-stu-id="150ca-154">**Conversational bots**: Natural language processing, AI, machine learning, and all the buzzwords.</span></span> <span data-ttu-id="150ca-155">インテリジェント クラウドを搭載したボットを使用して、ユーザーを必要な回答に接続します。</span><span class="sxs-lookup"><span data-stu-id="150ca-155">Use a bot powered by the intelligent cloud to connect your users to the answers they need.</span></span>

* <span data-ttu-id="150ca-156">**タブ**: Teams に既存の Web ポータルを埋め込むか、追加機能用に Teams 固有のバージョンを作成します。</span><span class="sxs-lookup"><span data-stu-id="150ca-156">**Tabs**: Embed your existing web portal in Teams or create a Teams-specific version for added functionality.</span></span>

## <a name="get-social"></a><span data-ttu-id="150ca-157">ソーシャルを取得する</span><span class="sxs-lookup"><span data-stu-id="150ca-157">Get social</span></span>

<span data-ttu-id="150ca-158">コラボレーション プラットフォームは、本質的にソーシャル プラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="150ca-158">A collaboration platform is inherently a social platform.</span></span> <span data-ttu-id="150ca-159">クリエイティブな側面を自由にし、職場に楽しい時間を過ごしましょう。</span><span class="sxs-lookup"><span data-stu-id="150ca-159">Let your creative side be free and add some fun into your workplace.</span></span> <span data-ttu-id="150ca-160">すべてのユーザーは、ジョークを送信したり、クドスを与え、ミームを取得したり、絵文字を使い切ったり、その他の何かがあなたの空想を打ち消したりできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-160">All users must be able to send jokes, give kudos, get some memes, toss out some emojis, or anything else that strikes your fancy.</span></span>

## <a name="think-in-terms-of-a-single-page-app"></a><span data-ttu-id="150ca-161">1 ページのアプリについて考える</span><span class="sxs-lookup"><span data-stu-id="150ca-161">Think in terms of a single-page app</span></span>

<span data-ttu-id="150ca-162">タブは埋め込み Web ページです。</span><span class="sxs-lookup"><span data-stu-id="150ca-162">Tabs are embedded web pages.</span></span> <span data-ttu-id="150ca-163">SPA で実行できる操作は、Teams のタブで行えます。</span><span class="sxs-lookup"><span data-stu-id="150ca-163">Pretty much anything you can do in a SPA, you can do in a tab in Teams.</span></span> <span data-ttu-id="150ca-164">スコープに注意を払う必要があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-164">Just be sure to pay attention to scope.</span></span> <span data-ttu-id="150ca-165">グループタブとチャネル タブは共有エクスペリエンス用で、個人用タブは個人的なエクスペリエンス用です。</span><span class="sxs-lookup"><span data-stu-id="150ca-165">Group and channel tabs are for shared experiences and personal tabs are for personal experiences.</span></span> <span data-ttu-id="150ca-166">チームの一覧が [チャネル] タブに表示され、自分のリストが個人用タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="150ca-166">The team's list of stuff goes on the channel tab and the list of your stuff goes in the personal tab.</span></span>

## <a name="start-small"></a><span data-ttu-id="150ca-167">小さく開始する</span><span class="sxs-lookup"><span data-stu-id="150ca-167">Start small</span></span>

<span data-ttu-id="150ca-168">どこから始めるのか分からないでしょうか?</span><span class="sxs-lookup"><span data-stu-id="150ca-168">Not sure where to start?</span></span> <span data-ttu-id="150ca-169">利用可能なオプションの素晴らしい種類に少し圧倒された感じ?</span><span class="sxs-lookup"><span data-stu-id="150ca-169">Feeling a bit overwhelmed with the awesome variety of options available to you?</span></span> <span data-ttu-id="150ca-170">アプリのコア機能を選択し、そこで開始する必要があります。</span><span class="sxs-lookup"><span data-stu-id="150ca-170">You must choose a core feature of your app and start there.</span></span> <span data-ttu-id="150ca-171">Teams のさまざまなコンテキストを通じて情報の流れを感じたら、より複雑なやり取りを見る方が非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="150ca-171">After you get a feel for the flow of information through the various contexts in Teams, it is a lot simpler to picture a more complex interaction.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="150ca-172">すべてまとめる</span><span class="sxs-lookup"><span data-stu-id="150ca-172">Put it all together</span></span>

<span data-ttu-id="150ca-173">つまり、最適なアプリは通常、複数の機能を組み合わせて、適切なコンテキストでユーザーと適切な機能を適切な時点で関与するアプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="150ca-173">That being said, the best apps usually combine multiple features, creating an app that engages users in the right context with the right functionality at the right time.</span></span> <span data-ttu-id="150ca-174">機能を、その機能が属していない場所に強制的に挿入しなけれ。</span><span class="sxs-lookup"><span data-stu-id="150ca-174">You must not force any functionality into a place it does not belong.</span></span> <span data-ttu-id="150ca-175">1 対 1 の会話ボットが優れたからといって、どのチームにも追加できるという意味ではありません。</span><span class="sxs-lookup"><span data-stu-id="150ca-175">Just because you have a good one-to-one conversational bot does not mean you add it to any team.</span></span> <span data-ttu-id="150ca-176">さまざまな機能拡張ポイントは、成功したアプリを作成するための長所を果たして、さまざまなものに優れた機能です。</span><span class="sxs-lookup"><span data-stu-id="150ca-176">Different extensibility points are good for different things, play to their strengths for creating a successful app.</span></span>

## <a name="see-also"></a><span data-ttu-id="150ca-177">関連項目</span><span class="sxs-lookup"><span data-stu-id="150ca-177">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="150ca-178">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="150ca-178">Build apps for Microsoft Teams</span></span>](../../overview.md)
 

