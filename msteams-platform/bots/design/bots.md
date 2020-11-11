---
title: ボットの設計ガイドライン
description: Bot を作成するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワークの bot トーク
ms.openlocfilehash: 0691c483d12e537772b74abc015d71e1704f88c8
ms.sourcegitcommit: fdb53284a20285f7e8a7daf25e85cb5d06c52b95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "48992639"
---
# <a name="start-talking-with-bots"></a><span data-ttu-id="9c593-104">Bot との会話を開始する</span><span class="sxs-lookup"><span data-stu-id="9c593-104">Start talking with bots</span></span>

<span data-ttu-id="9c593-105">Bot は、特定のタスクセットを実行する会話アプリです。</span><span class="sxs-lookup"><span data-stu-id="9c593-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="9c593-106">これにより、ユーザーとのコミュニケーションが可能になり、質問に回答して、変更について事前に通知する機会が得られます。</span><span class="sxs-lookup"><span data-stu-id="9c593-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="9c593-107">これらは、お客に到達するための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="9c593-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="9c593-108">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="9c593-108">Guidelines</span></span>

### <a name="bot-design-guidelines"></a><span data-ttu-id="9c593-109">Bot 設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="9c593-109">Bot design guidelines</span></span>

* <span data-ttu-id="9c593-110">アクティビティがある場合は、ボットが関連する通知を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-110">Bots should provide relevant notifications when there has been activity.</span></span>
* <span data-ttu-id="9c593-111">Bot は、データを表示しない対象ユーザーに対して、チーム、グループチャット、または1:1 会話に機密データをプッシュすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9c593-111">Bots must not push sensitive data to a team, group chat, or 1:1 conversation to an audience that should not view that data.</span></span>
* <span data-ttu-id="9c593-112">Bot 通知には、通知の関連性をユーザーに通知するための意味のあるデータが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-112">Bot notifications should include meaningful data to inform the relevance of the notification to users.</span></span>
* <span data-ttu-id="9c593-113">この bot の雰囲気は、ガイドラインに定義されているように、Teams の音声を反映している必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-113">The bot's tone should reflect the Teams voice, as defined in the guidelines.</span></span>
* <span data-ttu-id="9c593-114">Bot は、ボットの値とその主な機能を強調する最初の実行時のウェルカムメッセージを提供する必要があります。これは、「ツアーを開始する」、カルーセルを使用した対話式チュートリアル、または「お試しください」のような形式になっている場合があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-114">Bots should provide an first-run-experience welcome message that highlights the value of the bot and what its primary functions are, this might be in the form of "take a tour", an interactive tutorial with carousel cards, or "try it" buttons.</span></span>
* <span data-ttu-id="9c593-115">Bot テキストにスペルミスまたは文法上の誤りを含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="9c593-115">Bot text must not have any spelling mistakes or grammatical errors.</span></span>
* <span data-ttu-id="9c593-116">Bot は、実行可能な一連の bot コマンドを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-116">Bots must provide a set of predefined bot commands that are actionable.</span></span>
* <span data-ttu-id="9c593-117">ボットメッセージは、わかりやすく、操作が容易である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-117">Bot messages should be easy to understand and actionable.</span></span>
* <span data-ttu-id="9c593-118">Bot は、メッセージが認識されない場合に、フォールバックヘルプコマンドを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-118">Bots must provide fallback help commands when a message is not understood.</span></span>
* <span data-ttu-id="9c593-119">Bot によって送信されるフォームは、シーケンシャル更新を必要としない確定的な入力を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-119">Forms, embedded in cards, sent by a bot should provide deterministic inputs that do not require sequential updating.</span></span>
* <span data-ttu-id="9c593-120">Bot 通知は、対象ユーザーの関連コンテンツを含むチーム、グループチャット、または1:1 会話にスコープされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-120">Bot notifications should be scoped to a team, group chat, or 1:1 conversation with relevant content for the audience.</span></span>

### <a name="avatars"></a><span data-ttu-id="9c593-121">アバター</span><span class="sxs-lookup"><span data-stu-id="9c593-121">Avatars</span></span>

<span data-ttu-id="9c593-122">Teams のボットアバターは、六角形のようになっているため、ユーザーはユーザーではなく bot に話しかけていることがすぐにわかります。</span><span class="sxs-lookup"><span data-stu-id="9c593-122">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="9c593-123">アバターを正方形として送信し、自分でトリミングします。</span><span class="sxs-lookup"><span data-stu-id="9c593-123">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="9c593-124">アバターに関しては、2フィート離れて高いコントラストを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9c593-124">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="9c593-125">ボタン</span><span class="sxs-lookup"><span data-stu-id="9c593-125">Buttons</span></span>

<span data-ttu-id="9c593-126">カードごとに最大6つのボタンをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="9c593-126">We support up to six buttons per card.</span></span> <span data-ttu-id="9c593-127">ボタンテキストを記述する場合は簡潔にする必要があります。ほとんどのボタンは、自分のタスクにのみ対処する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9c593-127">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="9c593-128">グラフィックス</span><span class="sxs-lookup"><span data-stu-id="9c593-128">Graphics</span></span>

<span data-ttu-id="9c593-129">グラフィックスはストーリーを伝えるのに適した方法ですが、すべての bot がグラフィックスを必要とするわけではないため、これらを使用して最大の影響を受けることができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-129">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="onboarding-users"></a><span data-ttu-id="9c593-130">オンボードユーザー</span><span class="sxs-lookup"><span data-stu-id="9c593-130">Onboarding users</span></span>

<span data-ttu-id="9c593-131">Bot が自分を紹介し、ユーザーが実行できることを伝えることが重要です。</span><span class="sxs-lookup"><span data-stu-id="9c593-131">It is critical that bots introduce themselves and convey what they can do for users.</span></span> <span data-ttu-id="9c593-132">この *値* を使用すると、ユーザーは bot との関係を理解しやすくなり、制限がある場合には、ユーザーが実際のユーザーほど直観的ではないコンピューターとの相互作用を許容できるようになります。</span><span class="sxs-lookup"><span data-stu-id="9c593-132">This *value exchange* helps users understand what to do with the bot, where the limitations may lie, and, most importantly, helps users tolerate the interaction with a machine that won’t be as intuitive as a real person .</span></span> <span data-ttu-id="9c593-133">さらに、サービスによって提供される実際の値に対する exchange のユーザーデータへのアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="9c593-133">Additionally, it grants permission to user data in exchange for the real value the service provides.</span></span>

#### <a name="welcome-messages"></a><span data-ttu-id="9c593-134">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="9c593-134">Welcome messages</span></span>

<span data-ttu-id="9c593-135">ウェルカムメッセージは、ボットの雰囲気を設定するための最適な方法であり、個人およびチームまたはグループのシナリオで使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-135">Welcome messages are the best way to set your bot's tone and should be used in personal and team or group scenarios.</span></span> <span data-ttu-id="9c593-136">このメッセージは、bot が何をしているか、およびそれと対話するための一般的な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9c593-136">The message states what the bot does and some common ways to interact with it.</span></span> <span data-ttu-id="9c593-137">" *お問い合わせ* ください" などの特定の機能の例を使用します。</span><span class="sxs-lookup"><span data-stu-id="9c593-137">Use specific capability examples like,  “ *Try asking ….* ”</span></span> <span data-ttu-id="9c593-138">記号付きリスト。</span><span class="sxs-lookup"><span data-stu-id="9c593-138">in a bulleted list.</span></span> <span data-ttu-id="9c593-139">可能な限り、これらの提案は、保存された応答を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-139">Whenever possible, these suggestions should return stored responses.</span></span> <span data-ttu-id="9c593-140">機能の例は、ユーザーにサインインを求めることなく動作することが重要です。</span><span class="sxs-lookup"><span data-stu-id="9c593-140">It's critical that the capability examples work without requiring users to sign in.</span></span>
<span data-ttu-id="9c593-141">追加のガイダンスについては、 *「* [ウェルカムメッセージの要件](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-personal-bots-must-always-send-a-welcome-message-on-first-launch) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9c593-141">Please *see* [welcome message requirements](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-personal-bots-must-always-send-a-welcome-message-on-first-launch) for additional guidance.</span></span>

#### <a name="tours"></a><span data-ttu-id="9c593-142">ガイド</span><span class="sxs-lookup"><span data-stu-id="9c593-142">Tours</span></span>

<span data-ttu-id="9c593-143">ウェルカムメッセージと、" *help* " に相当するユーザー入力への応答を含む *ツアー* 属性を用意します。</span><span class="sxs-lookup"><span data-stu-id="9c593-143">Include a *Take a tour* attribute with welcome messages and responses to user input equivalent to “ *help* ”.</span></span> <span data-ttu-id="9c593-144">これは、ユーザーが bot が実行できることを理解させる最も効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="9c593-144">This is the most effective way to let users learn what a bot can do.</span></span> <span data-ttu-id="9c593-145">1対1のエクスペリエンスでの Carousels は、考えられる応答の例にリンクするように、このストーリーをわかり *やすく* する優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="9c593-145">Carousels in one-to-one experiences are an excellent way to tell this story and including *Try it* buttons linking to  examples of possible responses is encouraged.</span></span> <span data-ttu-id="9c593-146">ツアーでは、アプリの他の機能についても説明します。</span><span class="sxs-lookup"><span data-stu-id="9c593-146">Tours are also great places to talk about an app’s other features.</span></span> <span data-ttu-id="9c593-147">たとえば、メッセージング拡張機能と Teams タブのスクリーンショットを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-147">For example, you can include screenshots of messaging extensions and Teams tabs.</span></span>  <span data-ttu-id="9c593-148">ユーザーが、ツアーにアクセスして使用するためにサインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9c593-148">Users shouldn't have to sign in to access and use a tour.</span></span>

<span data-ttu-id="9c593-149">チームまたはグループのシナリオでツアーを使用する場合は、ユーザー間の進行中の会話にカードのノイズを追加しないように、タスクモジュールで開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-149">When tours are used in team or group scenarios, they should open in a task module so as not to add more card noise to the ongoing conversations between users.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="9c593-150">ユーザーに応答して、正常にエラーを発生させる</span><span class="sxs-lookup"><span data-stu-id="9c593-150">Responding to users and failing gracefully</span></span>

<span data-ttu-id="9c593-151">また、bot は、よくあるスペルミスと口語を考慮しながら、" *Hi* "、" *Help* "、" *どうもありがとう* " などに応答できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-151">Your bot should also be able to respond to things like " *Hi* ", " *Help* ", and " *Thanks* " while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="9c593-152">以下に例を示します。</span><span class="sxs-lookup"><span data-stu-id="9c593-152">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="9c593-153">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="9c593-153">&#x2713; Hello</span></span>

<span data-ttu-id="9c593-154">`"Hi"`  `"How are you"`  `"Howdy"`</span><span class="sxs-lookup"><span data-stu-id="9c593-154">`"Hi"`  `"How are you"`  `"Howdy"`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="9c593-155">&#x2713; のヘルプ</span><span class="sxs-lookup"><span data-stu-id="9c593-155">&#x2713; Help</span></span>

<span data-ttu-id="9c593-156">`"What do you do?"`  `"How does this work?"`  `"What the heck?"`</span><span class="sxs-lookup"><span data-stu-id="9c593-156">`"What do you do?"`  `"How does this work?"`  `"What the heck?"`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="9c593-157">&#x2713; よろしくお願いいたします。</span><span class="sxs-lookup"><span data-stu-id="9c593-157">&#x2713; Thanks</span></span>

<span data-ttu-id="9c593-158">`"Thank you"`  `"Thankyou"`  `"Thx"`</span><span class="sxs-lookup"><span data-stu-id="9c593-158">`"Thank you"`  `"Thankyou"`  `"Thx"`</span></span>

<span data-ttu-id="9c593-159">Bot は、次の種類のクエリと入力を処理できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-159">Your bot should be able to handle the following types of queries and inputs:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9c593-160">**認識** された質問。</span><span class="sxs-lookup"><span data-stu-id="9c593-160">**Recognized questions**.</span></span> <span data-ttu-id="9c593-161">ユーザーから期待される "ベストケースのシナリオ" についての質問を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="9c593-161">These are the “best case scenario” questions you would expect from users.</span></span>
> * <span data-ttu-id="9c593-162">**認識されない不明な質問** 。</span><span class="sxs-lookup"><span data-stu-id="9c593-162">**Recognized non-questions**.</span></span> <span data-ttu-id="9c593-163">サポートされていない機能、またはランダム、無関係、または profane エントリに関するクエリ。</span><span class="sxs-lookup"><span data-stu-id="9c593-163">Queries about unsupported functionality and/or random, unrelated , or profane entries.</span></span>
> * <span data-ttu-id="9c593-164">**認識できない質問** : 判読不能、無意味、または無意味な入力またはエントリ。</span><span class="sxs-lookup"><span data-stu-id="9c593-164">**Unrecognized questions** : Input or entries that are unintelligible, meaningless, or nonsense.</span></span>

<span data-ttu-id="9c593-165">Bot のパーソナリティと応答の種類の例:</span><span class="sxs-lookup"><span data-stu-id="9c593-165">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="9c593-166">Bot スクリプトを記述するときは、「応答が画面にキャプチャおよび共有されている場合は会社の embarrassed になりますか?」という質問をします。</span><span class="sxs-lookup"><span data-stu-id="9c593-166">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="9c593-167">ユーザーが発言しようとしていることを理解する</span><span class="sxs-lookup"><span data-stu-id="9c593-167">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="9c593-168">類義語辞典を使用する</span><span class="sxs-lookup"><span data-stu-id="9c593-168">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="9c593-169">バリエーションを使用している場合は、シソーラスを使用して、各クエリのさまざまな解釈を生成するのに役立つように、できるだけ多くの背景からユーザーを取得します。</span><span class="sxs-lookup"><span data-stu-id="9c593-169">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="9c593-170">テレメトリとインタビューを利用する</span><span class="sxs-lookup"><span data-stu-id="9c593-170">Make use of telemetry and interviews</span></span>

<span data-ttu-id="9c593-171">ユーザーが何を言っているか、ボットを照会する際にどのような意図があるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="9c593-171">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="9c593-172">これは、さまざまな場所や企業の種類でユーザーを取得するときに、継続的なプロセスになります。</span><span class="sxs-lookup"><span data-stu-id="9c593-172">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="9c593-173">言語を使用した言語認識と意図的なマッピングを微調整することができます ([LUIS](/azure/cognitive-services/luis/what-is-luis))。</span><span class="sxs-lookup"><span data-stu-id="9c593-173">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="9c593-174">ボットを使用してユーザーに連絡する頻度を指定します。</span><span class="sxs-lookup"><span data-stu-id="9c593-174">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="9c593-175">状態が変更されたときの &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-175">&#x2713; When a state has changed</span></span>

<span data-ttu-id="9c593-176">たとえば、割り当てが完了としてマークされている場合、バグが変更された場合、新しいソーシャルメディアが利用可能になった場合、またはポーリングが完了した場合などです。</span><span class="sxs-lookup"><span data-stu-id="9c593-176">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="9c593-177">タイミングが正しい場合の &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-177">&#x2713; When the timing is right</span></span>

<span data-ttu-id="9c593-178">Bot は、特定の頻度でユーザーまたはチャネルに通知を送信して、デイリーダイジェストのように機能することができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-178">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="9c593-179">ユーザーをコントロールのままにします。</span><span class="sxs-lookup"><span data-stu-id="9c593-179">Leave the user in control.</span></span> <span data-ttu-id="9c593-180">頻度と優先度を含む通知設定を提供します。</span><span class="sxs-lookup"><span data-stu-id="9c593-180">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="9c593-181">タブの使用</span><span class="sxs-lookup"><span data-stu-id="9c593-181">Using tabs</span></span>

<span data-ttu-id="9c593-182">タブを使用すると、ボットの機能が向上します。</span><span class="sxs-lookup"><span data-stu-id="9c593-182">Tabs make your bot much more functional.</span></span> <span data-ttu-id="9c593-183">タブでは、次のものを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9c593-183">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="9c593-184">サバイバルクエリをホストする場所を &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-184">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="9c593-185">Bot と1人のユーザーの個人用会話で、タブにはユーザー固有の情報とリストを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-185">In personal conversations between a bot and a single person, tabs can contain user-specific information and lists.</span></span> <span data-ttu-id="9c593-186">また、よく寄せられる質問 (Faq) に対してボットへの回答を維持するための適切な場所でもあります。そのため、ユーザーがたずねる必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9c593-186">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="9c593-187">会話を終了するための場所の &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-187">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="9c593-188">カードからタブにリンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-188">You can link to a tab from a card.</span></span> <span data-ttu-id="9c593-189">Bot が応答を提供し、さらにいくつかの手順が必要な場合は、タブにリンクしてタスクまたはフローを完了できます。</span><span class="sxs-lookup"><span data-stu-id="9c593-189">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span> <span data-ttu-id="9c593-190">たとえば、"iPhone を書式設定するにはどうすればよいですか" に対応していますが、適切な応答としては、 *最初のいくつ* かの手順を概説するカードがあり、それを *表示* するボタンがあります。</span><span class="sxs-lookup"><span data-stu-id="9c593-190">For instance, in response to, "How do I format my iPhone?", a good response might be a card which outlines the first few steps and has a button for *Show more* that then takes the user to the bot's *Help* tab and deep links to the specific instructions.</span></span>

### <a name="x2713-a-place-to-host-a-settings-page"></a><span data-ttu-id="9c593-191">設定ページをホストする場所を &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-191">&#x2713; A place to host a settings page</span></span>

<span data-ttu-id="9c593-192">Bot にはユーザーコントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="9c593-192">Bots should have some user control.</span></span> <span data-ttu-id="9c593-193">多くの bot については、チャットインターフェイスを通じて許可されます。ただし、これらの設定を覚えておくことは困難です。</span><span class="sxs-lookup"><span data-stu-id="9c593-193">For many bots it is allowed through a chat interface; however, it's hard to remember those settings.</span></span> <span data-ttu-id="9c593-194">[設定] タブでは、ユーザー設定を表示し、ユーザーが一度にすべての設定を変更できるようにすることができます。また、より複雑な bot カスタム動作に対して適切な手持在庫ポイントになる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="9c593-194">A settings tab can display users settings, allow users to change them all at once, and may also be a good hand-off point for more complex bot custom behaviors.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="9c593-195">いくつかのヘルプを提供する場所を &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-195">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="9c593-196">Bot との通信方法をユーザーに伝えるタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="9c593-196">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="9c593-197">何らかの状況や Faq を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-197">You can provide some context for what it does or FAQs.</span></span>

![ヘルプの提供](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="9c593-199">サイトのパーツをタブに埋め込むと、ユーザーはサービスを使用するときに会話のコンテキストを維持できます。</span><span class="sxs-lookup"><span data-stu-id="9c593-199">Embedding parts of your site in a tab will help users maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="9c593-200">ブラウザーでサービスを起動して、アプリ間で切り替えを行う必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="9c593-200">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="bots-in-channels"></a><span data-ttu-id="9c593-201">チャネル内のボット</span><span class="sxs-lookup"><span data-stu-id="9c593-201">Bots in channels</span></span>

<span data-ttu-id="9c593-202">チャネル内の bot を呼び出すことができ `@mention` ます。</span><span class="sxs-lookup"><span data-stu-id="9c593-202">Invoking a bot in a channel can be accomplished by `@mention`.</span></span> <span data-ttu-id="9c593-203">Bot ダイアログは、チャネルとグループの間で一意である必要があります。一般的に、個別のアプローチを検討することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9c593-203">Bot dialog should be unique in channels and groups vs. one-to-one scenarios and it's generally a good idea to consider separate approaches.</span></span> <span data-ttu-id="9c593-204">これは、次のような場合に特に当てはまります。</span><span class="sxs-lookup"><span data-stu-id="9c593-204">This is especially true in the following cases:</span></span>

### <a name="sensitive-data-sent-by-a-bot"></a><span data-ttu-id="9c593-205">Bot が送信する機密データ</span><span class="sxs-lookup"><span data-stu-id="9c593-205">Sensitive data sent by a bot</span></span>

<span data-ttu-id="9c593-206">チーム内のユーザーはサービスに対して認識されますが、実際のユーザーの役割はできません。</span><span class="sxs-lookup"><span data-stu-id="9c593-206">While the users in a team can be known to the service, the actual user roles cannot.</span></span> <span data-ttu-id="9c593-207">このことは、たとえば、文書に関する情報が含まれている場合に、親と受講者の連絡先情報をチーム設定で共有できないということです。</span><span class="sxs-lookup"><span data-stu-id="9c593-207">This means that, for example, in an education scenario involving bullying, parent and student contact information wouldn't be shared in a team setting.</span></span> <span data-ttu-id="9c593-208">Bot のメッセージは、詳細を表示するためのボタンと共に "現在、2つの非文書インシデントが発生しました" ということになります。</span><span class="sxs-lookup"><span data-stu-id="9c593-208">Instead the bot's message might be,"Two bullying incidents occurred today" along with a button to show details.</span></span>

<span data-ttu-id="9c593-209">Web ページで詳細を起動するか、タスクモジュールでユーザーの資格情報の入力を求めたり、AAD アカウントとペアになっているユーザーロールのインデックスに対してクエリを実行したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-209">Launching details in a web page, or a task module can prompt for user credentials or query against an index for user roles paired with AAD accounts.</span></span> <span data-ttu-id="9c593-210">どちらのオプションでも、データはプライベートビュースコープ内にあり、データ漏洩はありません。</span><span class="sxs-lookup"><span data-stu-id="9c593-210">In both of these options the data is in a private view scope and there will be no data leakage.</span></span> <span data-ttu-id="9c593-211">ユーザーと bot の間の1対1のチャットで同じデータが送信される場合、データはそのコンテキストのユーザーにのみ表示されるため、安全に bot が bot メッセージに完全に表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c593-211">If the same data is sent in a one-to-one chat between a user and the bot, the data is only visible to the user in that context and is, therefore safe, to fully display in the bot message.</span></span> <span data-ttu-id="9c593-212">チャネルから1対1のチャットへのユーザーの移動は、強制された移動が非常に中断されるため、回避する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-212">Taking users from a channel to a one-to-one chat should be avoided however as that forced navigation is highly disruptive.</span></span>

### <a name="sending-cards-as-a-response-to-interactions"></a><span data-ttu-id="9c593-213">相互作用への対応としてカードを送信する</span><span class="sxs-lookup"><span data-stu-id="9c593-213">Sending cards as a response to interactions</span></span>

<span data-ttu-id="9c593-214">一対一のチャットで *ツアーを実行* するために、カルーセルのカードを送信する際には、同じパターンを使用すると、多数のユーザーが含まれるアクティブなチャネルで数十台または数百種類の *ツアー carousels* を生成できます。</span><span class="sxs-lookup"><span data-stu-id="9c593-214">While sending a carousel card in response to *Take a tour* in a one-to-one chat is perfectly acceptable, the same pattern could yield tens or hundreds of *tour carousels* in an active channel with lots of users.</span></span> <span data-ttu-id="9c593-215">これを回避するには、セカンダリカードをタスクモジュールでホストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c593-215">To avoid this, secondary cards should be hosted in a task module.</span></span> <span data-ttu-id="9c593-216">このパターンを使用すると、ユーザーはチャネルに対してコンテキストで保持され、そのチャネルは長い bot 応答のままになり、必要に応じて *ツアー* が表示されたときに異なるユーザーの役割を考慮することができます。</span><span class="sxs-lookup"><span data-stu-id="9c593-216">This pattern keeps users in context with the channel, keeps the channel clean of excessive bot responses, and can optionally consider different user roles when the *tour* is shown.</span></span>

## <a name="useful-tips"></a><span data-ttu-id="9c593-217">役に立つヒント</span><span class="sxs-lookup"><span data-stu-id="9c593-217">Useful tips</span></span>

### <a name="x2713-remember-bots-arent-assistants"></a><span data-ttu-id="9c593-218">&#x2713; を覚えておくことはできません。</span><span class="sxs-lookup"><span data-stu-id="9c593-218">&#x2713; Remember, bots aren’t assistants</span></span>

<span data-ttu-id="9c593-219">Cortana や bot などのエージェントとは異なり、スペシャリストとして機能します。</span><span class="sxs-lookup"><span data-stu-id="9c593-219">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="9c593-220">&#x2713; 防ぐ chitchat</span><span class="sxs-lookup"><span data-stu-id="9c593-220">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="9c593-221">Bot が会話用に構築されていない場合は、chitchat をタスク完了にリダイレクトする方法を検索します。</span><span class="sxs-lookup"><span data-stu-id="9c593-221">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="9c593-222">&#x2713; を紹介します。</span><span class="sxs-lookup"><span data-stu-id="9c593-222">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="9c593-223">お客様の bot の個性を製品の声と同じにしておきます。</span><span class="sxs-lookup"><span data-stu-id="9c593-223">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="9c593-224">お客様の企業の bot と考えてください。</span><span class="sxs-lookup"><span data-stu-id="9c593-224">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="9c593-225">トーンを維持 &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-225">&#x2713; Maintain tone</span></span>

<span data-ttu-id="9c593-226">トーンがわかりやすく、明るいかどうかを判断するために、"ファクトのみ"、または super quirky を使用します。</span><span class="sxs-lookup"><span data-stu-id="9c593-226">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="9c593-227">簡単なタスクフローを促す &#x2713;</span><span class="sxs-lookup"><span data-stu-id="9c593-227">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="9c593-228">完全な形式の質問を引き続き許可しながら、複数ターンの対話をサポートします。</span><span class="sxs-lookup"><span data-stu-id="9c593-228">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="9c593-229">次の手順を予測することで、ユーザーはタスクフローをより簡単に理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="9c593-229">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="9c593-230">ユーザーがタスクを完了するためにいくつかの手順を実行する場合は、各手順を通じて bot に対して実行を許可し、より迅速なパスを提案することによって終了します。</span><span class="sxs-lookup"><span data-stu-id="9c593-230">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="9c593-231">たとえば、ユーザーがいくつかの会話を行って会議を設定した場合 (最初に会議を指定し、次にその人物を特定して、その日を示す時刻を指定した場合)、次の提案で会話を終了します。次回は、「1:00 明日で Bob を使用して会議をスケジュールする」を試してみます。</span><span class="sxs-lookup"><span data-stu-id="9c593-231">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>
