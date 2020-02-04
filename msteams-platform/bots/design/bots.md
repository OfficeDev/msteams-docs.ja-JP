---
title: ボットの設計ガイドライン
description: Bot を作成するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワークの bot トーク
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675040"
---
# <a name="start-talking-with-bots"></a><span data-ttu-id="eca84-104">Bot との会話を開始する</span><span class="sxs-lookup"><span data-stu-id="eca84-104">Start talking with bots</span></span>

<span data-ttu-id="eca84-105">Bot は、特定のタスクセットを実行する会話アプリです。</span><span class="sxs-lookup"><span data-stu-id="eca84-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="eca84-106">これにより、ユーザーとのコミュニケーションが可能になり、質問に回答して、変更について事前に通知する機会が得られます。</span><span class="sxs-lookup"><span data-stu-id="eca84-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="eca84-107">これらは、お客に到達するための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="eca84-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="eca84-108">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="eca84-108">Guidelines</span></span>

### <a name="avatars"></a><span data-ttu-id="eca84-109">アバター</span><span class="sxs-lookup"><span data-stu-id="eca84-109">Avatars</span></span>

<span data-ttu-id="eca84-110">Teams のボットアバターは、六角形のようになっているため、ユーザーはユーザーではなく bot に話しかけていることがすぐにわかります。</span><span class="sxs-lookup"><span data-stu-id="eca84-110">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="eca84-111">アバターを正方形として送信し、自分でトリミングします。</span><span class="sxs-lookup"><span data-stu-id="eca84-111">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="eca84-112">アバターに関しては、2フィート離れて高いコントラストを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="eca84-112">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="eca84-113">ボタン</span><span class="sxs-lookup"><span data-stu-id="eca84-113">Buttons</span></span>

<span data-ttu-id="eca84-114">カードごとに最大6つのボタンをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="eca84-114">We support up to six buttons per card.</span></span> <span data-ttu-id="eca84-115">ボタンテキストを記述する場合は簡潔にする必要があります。ほとんどのボタンは、自分のタスクにのみ対処する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="eca84-115">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="eca84-116">グラフィックス</span><span class="sxs-lookup"><span data-stu-id="eca84-116">Graphics</span></span>

<span data-ttu-id="eca84-117">グラフィックスはストーリーを伝えるのに適した方法ですが、すべての bot がグラフィックスを必要とするわけではないため、これらを使用して最大の影響を受けることができます。</span><span class="sxs-lookup"><span data-stu-id="eca84-117">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="eca84-118">ユーザーに応答して、正常にエラーを発生させる</span><span class="sxs-lookup"><span data-stu-id="eca84-118">Responding to users and failing gracefully</span></span>

<span data-ttu-id="eca84-119">Bot は、一般的なスペルミスと口語を考慮しながら、' Hi '、' Help '、' どうも ' などに応答することもできます。</span><span class="sxs-lookup"><span data-stu-id="eca84-119">Your bot should also be able to respond to things like 'Hi', 'Help', and 'Thanks' while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="eca84-120">例:</span><span class="sxs-lookup"><span data-stu-id="eca84-120">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="eca84-121">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="eca84-121">&#x2713; Hello</span></span>

<span data-ttu-id="eca84-122">`Hi` `how are you` `howdy`</span><span class="sxs-lookup"><span data-stu-id="eca84-122">`Hi` `how are you` `howdy`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="eca84-123">&#x2713; のヘルプ</span><span class="sxs-lookup"><span data-stu-id="eca84-123">&#x2713; Help</span></span>

<span data-ttu-id="eca84-124">`What do you do?` `How does this work?` `What the heck?`</span><span class="sxs-lookup"><span data-stu-id="eca84-124">`What do you do?` `How does this work?` `What the heck?`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="eca84-125">&#x2713; よろしくお願いいたします。</span><span class="sxs-lookup"><span data-stu-id="eca84-125">&#x2713; Thanks</span></span>

<span data-ttu-id="eca84-126">`Thank you` `thankyou` `thx`</span><span class="sxs-lookup"><span data-stu-id="eca84-126">`Thank you` `thankyou` `thx`</span></span>

<span data-ttu-id="eca84-127">Bot は、次の種類のクエリと入力を処理できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="eca84-127">Your bot should be able to handle the following types of queries and inputs:</span></span>

* <span data-ttu-id="eca84-128">**認識**される質問: これらは、ユーザーから予想される "ベストケースのシナリオ" 質問です。</span><span class="sxs-lookup"><span data-stu-id="eca84-128">**Recognized questions**: These are the “best case scenario” questions you’d anticipate from users.</span></span>
* <span data-ttu-id="eca84-129">**認識されない問題**: サポートされていない機能、ランダムな情報、またはユーザーが bot で curse を希望する場合についてのクエリ。</span><span class="sxs-lookup"><span data-stu-id="eca84-129">**Recognized non-questions**: Queries about unsupported functionality, random pieces of information, or when someone wants to curse at your bot.</span></span>
* <span data-ttu-id="eca84-130">**認識されない質問**: 判読不能な入力 (つまり、不自然)。</span><span class="sxs-lookup"><span data-stu-id="eca84-130">**Unrecognized questions**: Unintelligible inputs (i.e., gibberish).</span></span>

<span data-ttu-id="eca84-131">Bot のパーソナリティと応答の種類の例:</span><span class="sxs-lookup"><span data-stu-id="eca84-131">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="eca84-132">Bot スクリプトを記述するときは、「応答が画面にキャプチャおよび共有されている場合は会社の embarrassed になりますか?」という質問をします。</span><span class="sxs-lookup"><span data-stu-id="eca84-132">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="eca84-133">ユーザーが発言しようとしていることを理解する</span><span class="sxs-lookup"><span data-stu-id="eca84-133">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="eca84-134">類義語辞典を使用する</span><span class="sxs-lookup"><span data-stu-id="eca84-134">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="eca84-135">バリエーションを使用している場合は、シソーラスを使用して、各クエリのさまざまな解釈を生成するのに役立つように、できるだけ多くの背景からユーザーを取得します。</span><span class="sxs-lookup"><span data-stu-id="eca84-135">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="eca84-136">テレメトリとインタビューを利用する</span><span class="sxs-lookup"><span data-stu-id="eca84-136">Make use of telemetry and interviews</span></span>

<span data-ttu-id="eca84-137">ユーザーが何を言っているか、ボットを照会する際にどのような意図があるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="eca84-137">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="eca84-138">これは、さまざまな場所や企業の種類でユーザーを取得するときに、継続的なプロセスになります。</span><span class="sxs-lookup"><span data-stu-id="eca84-138">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="eca84-139">言語を使用した言語認識と意図的なマッピングを微調整することができます ([LUIS](/azure/cognitive-services/luis/what-is-luis))。</span><span class="sxs-lookup"><span data-stu-id="eca84-139">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="eca84-140">ボットを使用してユーザーに連絡する頻度を指定します。</span><span class="sxs-lookup"><span data-stu-id="eca84-140">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="eca84-141">状態が変更されたときの &#x2713;</span><span class="sxs-lookup"><span data-stu-id="eca84-141">&#x2713; When a state has changed</span></span>

<span data-ttu-id="eca84-142">たとえば、割り当てが完了としてマークされている場合、バグが変更された場合、新しいソーシャルメディアが利用可能になった場合、またはポーリングが完了した場合などです。</span><span class="sxs-lookup"><span data-stu-id="eca84-142">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="eca84-143">タイミングが正しい場合の &#x2713;</span><span class="sxs-lookup"><span data-stu-id="eca84-143">&#x2713; When the timing is right</span></span>

<span data-ttu-id="eca84-144">Bot は、特定の頻度でユーザーまたはチャネルに通知を送信して、デイリーダイジェストのように機能することができます。</span><span class="sxs-lookup"><span data-stu-id="eca84-144">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="eca84-145">ユーザーをコントロールのままにします。</span><span class="sxs-lookup"><span data-stu-id="eca84-145">Leave the user in control.</span></span> <span data-ttu-id="eca84-146">頻度と優先度を含む通知設定を提供します。</span><span class="sxs-lookup"><span data-stu-id="eca84-146">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="eca84-147">タブの使用</span><span class="sxs-lookup"><span data-stu-id="eca84-147">Using tabs</span></span>

<span data-ttu-id="eca84-148">タブを使用すると、ボットの機能が向上します。</span><span class="sxs-lookup"><span data-stu-id="eca84-148">Tabs make your bot much more functional.</span></span> <span data-ttu-id="eca84-149">タブでは、次のものを作成できます。</span><span class="sxs-lookup"><span data-stu-id="eca84-149">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="eca84-150">サバイバルクエリをホストする場所を &#x2713;</span><span class="sxs-lookup"><span data-stu-id="eca84-150">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="eca84-151">Bot と1人のユーザーの個人的な会話では、タブでユーザー固有の情報やリストを格納できます。</span><span class="sxs-lookup"><span data-stu-id="eca84-151">In personal conversations between a bot and a single person, tabs can house user-specific information and lists.</span></span> <span data-ttu-id="eca84-152">また、よく寄せられる質問 (Faq) に対してボットへの回答を維持するための適切な場所でもあります。そのため、ユーザーがたずねる必要はありません。</span><span class="sxs-lookup"><span data-stu-id="eca84-152">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="eca84-153">会話を終了するための場所の &#x2713;</span><span class="sxs-lookup"><span data-stu-id="eca84-153">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="eca84-154">カードからタブにリンクすることができます。</span><span class="sxs-lookup"><span data-stu-id="eca84-154">You can link to a tab from a card.</span></span> <span data-ttu-id="eca84-155">Bot が応答を提供し、さらにいくつかの手順が必要な場合は、タブにリンクしてタスクまたはフローを完了できます。</span><span class="sxs-lookup"><span data-stu-id="eca84-155">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="eca84-156">いくつかのヘルプを提供する場所を &#x2713;</span><span class="sxs-lookup"><span data-stu-id="eca84-156">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="eca84-157">Bot との通信方法をユーザーに伝えるタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="eca84-157">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="eca84-158">何らかの状況や Faq を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="eca84-158">You can provide some context for what it does or FAQs.</span></span>

![ヘルプの提供](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="eca84-160">サイトのパーツをタブに埋め込むと、ユーザーがサービスを使用するときに会話のコンテキストを維持するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="eca84-160">Embedding parts of your site in a tab will help someone maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="eca84-161">ブラウザーでサービスを起動して、アプリ間で切り替えを行う必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="eca84-161">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="best-practices"></a><span data-ttu-id="eca84-162">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="eca84-162">Best practices</span></span>

### <a name="x2713-bots-arent-assistants"></a><span data-ttu-id="eca84-163">&#x2713; Bot がアシスタントでない</span><span class="sxs-lookup"><span data-stu-id="eca84-163">&#x2713; Bots aren’t assistants</span></span>

<span data-ttu-id="eca84-164">Cortana や bot などのエージェントとは異なり、スペシャリストとして機能します。</span><span class="sxs-lookup"><span data-stu-id="eca84-164">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="eca84-165">&#x2713; 防ぐ chitchat</span><span class="sxs-lookup"><span data-stu-id="eca84-165">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="eca84-166">Bot が会話用に構築されていない場合は、chitchat をタスク完了にリダイレクトする方法を検索します。</span><span class="sxs-lookup"><span data-stu-id="eca84-166">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="eca84-167">&#x2713; を紹介します。</span><span class="sxs-lookup"><span data-stu-id="eca84-167">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="eca84-168">お客様の bot の個性を製品の声と同じにしておきます。</span><span class="sxs-lookup"><span data-stu-id="eca84-168">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="eca84-169">お客様の企業の bot と考えてください。</span><span class="sxs-lookup"><span data-stu-id="eca84-169">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="eca84-170">トーンを維持 &#x2713;</span><span class="sxs-lookup"><span data-stu-id="eca84-170">&#x2713; Maintain tone</span></span>

<span data-ttu-id="eca84-171">トーンがわかりやすく、明るいかどうかを判断するために、"ファクトのみ"、または super quirky を使用します。</span><span class="sxs-lookup"><span data-stu-id="eca84-171">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="eca84-172">簡単なタスクフローを促す &#x2713;</span><span class="sxs-lookup"><span data-stu-id="eca84-172">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="eca84-173">完全な形式の質問を引き続き許可しながら、複数ターンの対話をサポートします。</span><span class="sxs-lookup"><span data-stu-id="eca84-173">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="eca84-174">次の手順を予測することで、ユーザーはタスクフローをより簡単に理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="eca84-174">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="eca84-175">ユーザーがタスクを完了するためにいくつかの手順を実行する場合は、各手順を通じて bot に対して実行を許可し、より迅速なパスを提案することによって終了します。</span><span class="sxs-lookup"><span data-stu-id="eca84-175">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="eca84-176">たとえば、ユーザーがいくつかの会話を行って会議を設定した場合 (最初に会議を指定し、次にその人物との識別を行い、時刻を指定して、その日を示す場合)、次の提案に従って会話を終了します。「1:00 明日で Bob を使用して会議をスケジュールすることができます。</span><span class="sxs-lookup"><span data-stu-id="eca84-176">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>