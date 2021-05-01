---
title: ボットをデザインする
description: Teams のボットをデザインして、Microsoft Teams UI Kit を取得するする方法をご紹介します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: d2967abdc6c0055eca8c94ed4e4a7fdf1bdba322
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101696"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="d1adb-103">Microsoft Teams のボットをデザインする</span><span class="sxs-lookup"><span data-stu-id="d1adb-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="d1adb-104">ボットは、特定のタスクを実行する会話型アプリです。</span><span class="sxs-lookup"><span data-stu-id="d1adb-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="d1adb-105"><a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a> をベースに、ボットはユーザーと通信し、ユーザーの質問に答え、変更などのイベントをプロアクティブに通知します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="d1adb-106">ボットは、連絡を取るのに最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-106">They're a great way to reach out.</span></span>

<span data-ttu-id="d1adb-107">アプリのデザインに役立てるために、次の情報では、Teams でユーザーがどのようにボットを追加、使用、管理できるかを説明、図解しています。</span><span class="sxs-lookup"><span data-stu-id="d1adb-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d1adb-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="d1adb-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d1adb-109">Microsoft Teams UI Kit には、必要に応じて変更できる要素を含む、より包括的なボット デザインのガイドラインが掲載されています。</span><span class="sxs-lookup"><span data-stu-id="d1adb-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1adb-110">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="d1adb-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="d1adb-111">ボットの追加</span><span class="sxs-lookup"><span data-stu-id="d1adb-111">Add a bot</span></span>

<span data-ttu-id="d1adb-112">ボットは、チャット、チャネル、個人用アプリで利用できます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="d1adb-113">ボットの追加は、次の方法のいずれかで実現できます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="d1adb-114">Teams ストア (AppSource) から。</span><span class="sxs-lookup"><span data-stu-id="d1adb-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="d1adb-115">Teams の左側にある **[詳細]** アイコンを選択してアプリのフライアウトを使用する。</span><span class="sxs-lookup"><span data-stu-id="d1adb-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="d1adb-116">新規チャットや作成ボックスに@メンションを使用する (次の例ではグループ チャットでのやり方を示しています)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="例では、@メンションを使用してグループ チャットにボットを追加する方法をご紹介します。" border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="d1adb-118">ボットの導入</span><span class="sxs-lookup"><span data-stu-id="d1adb-118">Introduce a bot</span></span>

<span data-ttu-id="d1adb-119">ボットが自己紹介し、何ができるのかを説明することが重要です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="d1adb-120">この最初のやり取りによって、ユーザーはボットで何ができるかを理解し、その制限事項を知り、そして最も重要なことは、ボットとの対話を快適に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="d1adb-121">1 対 1 のチャットでのウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="d1adb-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="d1adb-122">個人的なコンテキストでは、ウェルカム メッセージはボットのトーンを決めるものです。</span><span class="sxs-lookup"><span data-stu-id="d1adb-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="d1adb-123">メッセージには、挨拶、ボットができること、対話方法の提案 (「...　について聞いてみてください」など) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact (for example, “Try asking me about …”).</span></span> <span data-ttu-id="d1adb-124">可能であれば、これらの提案は、サインインしなくても保存された応答を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-124">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="個人アプリでのボット導入例を示します。" border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="d1adb-126">グループ チャットやチャネルでの自己紹介</span><span class="sxs-lookup"><span data-stu-id="d1adb-126">Introductions in group chats and channels</span></span>

<span data-ttu-id="d1adb-127">グループ チャットやチャネルでのボットの紹介は、個人的なコンテキスト (個人用アプリなど) とは多少異なる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-127">Your bot's introduction should be slightly different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="d1adb-128">実生活では、大勢の人がいる部屋に入った場合に、既にいる人を歓迎するのではなく、自己紹介をするはずです。</span><span class="sxs-lookup"><span data-stu-id="d1adb-128">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="d1adb-129">その考え方は、ボットのデザインにも生かされています。</span><span class="sxs-lookup"><span data-stu-id="d1adb-129">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="共同作業コンテキストでのボット導入例を示します。" border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="d1adb-131">シングル サインオンを使用したボット認証</span><span class="sxs-lookup"><span data-stu-id="d1adb-131">Bot authentication with single sign-on</span></span>

<span data-ttu-id="d1adb-132">ユーザーがボットにメッセージを送る場合、そのボットのすべての機能を利用するにはサインインが必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-132">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="d1adb-133">シングル サインオン (SSO) を使用することで認証プロセスを簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-133">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="d1adb-134">忘れてはいけないのが、ボットのコマンド メニュー (**可能な対処**) では、サインアウトするためのコマンドも用意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-134">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="サインイン ボタンのあるボットの例を示します。" border="false":::

### <a name="tours"></a><span data-ttu-id="d1adb-136">ツアー</span><span class="sxs-lookup"><span data-stu-id="d1adb-136">Tours</span></span>

<span data-ttu-id="d1adb-137">ウェルカム メッセージや "ヘルプ "コマンドのようなものにボットが応答する場合にツアーを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-137">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="d1adb-138">ボットにできることを説明するには、ツアーが最も効果的です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-138">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="d1adb-139">必要に応じて、アプリのその他の機能を説明するのにも最適です (メッセージング拡張機能のスクリーンショットを掲載するなど)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-139">If applicable, they’re also great for describing your app’s other features (for example, include screenshots of your messaging extension).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1adb-140">ログインしなくてもツアーに参加できることが必要です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-140">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="d1adb-141">1 対 1 のチャット</span><span class="sxs-lookup"><span data-stu-id="d1adb-141">One-on-one chats</span></span>

<span data-ttu-id="d1adb-142">個人用アプリでは、カルーセルでボットやお使いのアプリのその他の機能の概要を効果的に伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-142">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="d1adb-143">ユーザーがボットのコマンドを試すことができるボタンを含めることが推奨されます (例：**タスクを作成する**)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-143">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="1 対 1 のチャットでのボット ツアーの例を示します。" border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="d1adb-145">チャネルとグループ チャット</span><span class="sxs-lookup"><span data-stu-id="d1adb-145">Channels and group chats</span></span>

<span data-ttu-id="d1adb-146">チャネルやグループ チャットでは、ツアーはモーダル ([タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)とも呼ばれます) で開き、現在進行中の会話に干渉しないようにします。</span><span class="sxs-lookup"><span data-stu-id="d1adb-146">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="d1adb-147">また、ツアーにロール ベースのビューを実装することも可能です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-147">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="チャネルでのボット ツアーの例を示します。" border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="d1adb-149">ボットとチャットする</span><span class="sxs-lookup"><span data-stu-id="d1adb-149">Chat with a bot</span></span>

<span data-ttu-id="d1adb-150">ボットは、Teams のメッセージング フレームワークに直接統合されます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-150">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="d1adb-151">ユーザーはボットとチャットして質問に回答してもらったり、コマンドを入力して特定のタスクを実行してもらったりすることができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-151">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="d1adb-152">ボットは、お使いのアプリへのチャットを介してユーザーに変更や更新をプロアクティブに通知することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-152">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="d1adb-153">さまざまなコンテキストでボットを使用したチャット</span><span class="sxs-lookup"><span data-stu-id="d1adb-153">Chat with a bot in different contexts</span></span>

<span data-ttu-id="d1adb-154">ボットは次のような場面で使用できます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-154">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="d1adb-155">**個人用アプリ**: 個人用アプリでは、ボットには専用のチャット タブがあります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-155">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="d1adb-156">**1 対 1 のチャット**: ユーザーがボットとプライベートな会話を開始することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-156">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="d1adb-157">個人用アプリでボットを使うのと同様のエクスペリエンスです。</span><span class="sxs-lookup"><span data-stu-id="d1adb-157">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="d1adb-158">**グループ チャット**: グループ チャットでは、ボットを @メンションすることで、ボットと対話することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-158">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="d1adb-159">**チャネル**: ユーザーは、チャネルでボットと対話することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-159">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="d1adb-160">作成ボックスでボット名を　@メンションします。</span><span class="sxs-lookup"><span data-stu-id="d1adb-160">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="d1adb-161">このコンテキストでは、ボットはチャネルだけでなく、チーム全体で使用できることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="d1adb-161">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="d1adb-162">構造</span><span class="sxs-lookup"><span data-stu-id="d1adb-162">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="ボットの構造的な例を示します。" border="false":::

|<span data-ttu-id="d1adb-164">カウンター</span><span class="sxs-lookup"><span data-stu-id="d1adb-164">Counter</span></span>|<span data-ttu-id="d1adb-165">説明</span><span class="sxs-lookup"><span data-stu-id="d1adb-165">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d1adb-166">1</span><span class="sxs-lookup"><span data-stu-id="d1adb-166">1</span></span>|<span data-ttu-id="d1adb-167">**アプリ名とアイコン**</span><span class="sxs-lookup"><span data-stu-id="d1adb-167">**App name and icon**</span></span>|
|<span data-ttu-id="d1adb-168">2</span><span class="sxs-lookup"><span data-stu-id="d1adb-168">2</span></span>|<span data-ttu-id="d1adb-169">**[チャット] タブ**: ボットと会話するための空間を開きます (個人用アプリのみ該当)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-169">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="d1adb-170">3</span><span class="sxs-lookup"><span data-stu-id="d1adb-170">3</span></span>|<span data-ttu-id="d1adb-171">**[カスタム] タブ**: アプリに関連するその他のコンテンツを開きます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-171">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="d1adb-172">4</span><span class="sxs-lookup"><span data-stu-id="d1adb-172">4</span></span>|<span data-ttu-id="d1adb-173">**[バージョン情報] タブ**: アプリの基本情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-173">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="d1adb-174">5</span><span class="sxs-lookup"><span data-stu-id="d1adb-174">5</span></span>|<span data-ttu-id="d1adb-175">**チャット バブル**: ボットの会話は、Teams のメッセージング フレームワークを使用しています。</span><span class="sxs-lookup"><span data-stu-id="d1adb-175">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="d1adb-176">6</span><span class="sxs-lookup"><span data-stu-id="d1adb-176">6</span></span>|<span data-ttu-id="d1adb-177">**アダプティブ カード**: ボットの応答にアダプティブ カードが含まれる場合、カードはチャット バブルの幅いっぱいに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-177">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="d1adb-178">7</span><span class="sxs-lookup"><span data-stu-id="d1adb-178">7</span></span>|<span data-ttu-id="d1adb-179">**コマンド メニュー**: ボットの標準コマンド (ユーザーによる定義) を表示します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-179">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="d1adb-180">コマンド メニュー</span><span class="sxs-lookup"><span data-stu-id="d1adb-180">Command menu</span></span>

<span data-ttu-id="d1adb-181">コマンド メニューには、ボットが常に応答するようにする単語や語句のリストが用意されています。</span><span class="sxs-lookup"><span data-stu-id="d1adb-181">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="d1adb-182">ボットと会話しているときに、作成ボックスの上にコマンド メニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-182">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="d1adb-183">コマンドを選択した場合に、そのコマンドがメッセージに挿入されます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-183">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="d1adb-184">コマンドのリストは簡潔である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-184">The list of commands should be brief.</span></span> <span data-ttu-id="d1adb-185">メニューは、ボットの主要な機能を強調するためだけのものです。</span><span class="sxs-lookup"><span data-stu-id="d1adb-185">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="d1adb-186">また、コマンドも簡潔に保持します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-186">Keep commands concise, too.</span></span> <span data-ttu-id="d1adb-187">例えば、**手伝ってもらえますか?** の代わりに **ヘルプ** というコマンドを作成します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-187">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="d1adb-188">会話の状態に関係なく、コマンド メニューは常に使用可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-188">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="ボットのコマンド メニューの例を示します。" border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="d1adb-190">ユーザーの話を理解する</span><span class="sxs-lookup"><span data-stu-id="d1adb-190">Understand what people are saying</span></span>

<span data-ttu-id="d1adb-191">シソーラスを使ったり、できるだけ多くの異なるバックグラウンドを持つユーザーの協力を得て、標準的な質問に対するさまざまな解釈を生成します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-191">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="ボットが ‘こんにちは’ を解釈する方法を示す図。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="ボットが ‘ヘルプ’ を解釈する方法を示す図。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="ボットが ‘ありがとう’ を解釈する方法を示す図。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="d1adb-195">メッセージから意図やデータを抽出</span><span class="sxs-lookup"><span data-stu-id="d1adb-195">Extract intent and data from messages</span></span>

<span data-ttu-id="d1adb-196">メッセージやクエリに応じて、相手がボットに何を求めているかをキャプチャする、意図の認識を目指してボットをデザインします。</span><span class="sxs-lookup"><span data-stu-id="d1adb-196">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="d1adb-197">意図は、メッセージやクエリを、アクションの影響を受ける 1 つ以上のデータ オブジェクトのある単一のアクションとして分類します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-197">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="d1adb-198">次の例は、ボットに送信されるメッセージに含まれるユーザーの意図とデータの概要です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-198">The following examples outline the user intent and data in messages sent to bots.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="‘シアトル行きの航空券を予約する’ という文の場合、ユーザーの意図は ‘航空券の予約’ であり、データは ‘シアトル’ であることを示す例。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="‘何時に店が開くか’ という文の場合、ユーザーの意図は ‘何時’ であり、データは ‘開く’ です。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="‘配送のボブと午後 1 時に会議をスケジュールする’ という文の場合、ユーザーの意図は ‘会議のスケジュール’ であり、データは ‘午後 1 時’ と ‘配送のボブ’ です。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="d1adb-202">分析と機能強化</span><span class="sxs-lookup"><span data-stu-id="d1adb-202">Analyze and improve</span></span>

<span data-ttu-id="d1adb-203">ボットとのチャットでのユーザーの発言をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-203">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="d1adb-204">これは、さまざまな場所や組織でユーザーが増えていく中で、継続的で反復的な手順です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-204">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="d1adb-205">Microsoft Language Understanding (LUIS) を使用して、ボットの言語認識や意図のマッピングを調節することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-205">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="d1adb-206">[LUIS を理解する](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): LUIS が AI を使用してアプリのデータに自然言語理解 (NLU) を提供する方法をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-206">[Understanding LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="d1adb-207">[LUIS との統合](https://www.luis.ai/): 機械学習モデルを作成する複雑な手順を通すことなく、ボットに自然言語機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-207">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="d1adb-208">使用例</span><span class="sxs-lookup"><span data-stu-id="d1adb-208">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="d1adb-209">単純なクエリ</span><span class="sxs-lookup"><span data-stu-id="d1adb-209">Simple queries</span></span>

<span data-ttu-id="d1adb-210">ボットは、クエリと完全に一致する内容や関連して一致するグループを配信して、曖昧さを解消することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-210">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="d1adb-211">関連する一致については、リスト カードを使用してコンテンツをグループ化します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-211">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="ボットとの単純なクエリの対話を示す例。" border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="d1adb-213">複数回の対話</span><span class="sxs-lookup"><span data-stu-id="d1adb-213">Multi-turn interactions</span></span>

<span data-ttu-id="d1adb-214">ボットは、完全な要求や質問をサポートすることができますが、複数回の対話を処理することもできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-214">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="d1adb-215">次の手順の可能性を予測することで、ユーザーは (包括的な要求を作成することを想定するのではなく) 完全なタスク フローをより簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-215">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="d1adb-216">次の例では、ボットはそれぞれのメッセージに対して、次にしたいことのオプションを応答します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-216">In the following example, the bot responds to each message with options for what might want to do next.</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="ボットとの複数回の対話を示す例。" border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="d1adb-218">ユーザーへの働きかけ</span><span class="sxs-lookup"><span data-stu-id="d1adb-218">Reach out to users</span></span>

<span data-ttu-id="d1adb-219">プロアクティブなメッセージングでは、ボットは個人、グループ チャット、またはチャネルに関連する通知を特定の頻度で送信するダイジェストのように機能します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-219">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="d1adb-220">ボットは、ドキュメントに何か変更があった場合や、作業項目を閉じた場合に、メッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-220">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="d1adb-221">ユーザーが、ボットが別のチャネルでメッセージを送ってきたことをトースト通知で受け取る例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-221">In the following example, a user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="ボットが他のチャネルからユーザーにプロアクティブにメッセージを送るトーストを示す例。" border="false":::

<span data-ttu-id="d1adb-223">そのチャネルでは、ユーザーはボットからのメッセージを読むことができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-223">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="ユーザーがボットのプロアクティブなメッセージを見ている様子を示す例。" border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="d1adb-225">ボットでタブを使用する</span><span class="sxs-lookup"><span data-stu-id="d1adb-225">Use tabs with bots</span></span>

<span data-ttu-id="d1adb-226">タブがあることで、ボットをより使いやすくすることができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-226">A tab can make your bot easier to use.</span></span> <span data-ttu-id="d1adb-227">たとえば、ボットが作業項目を作成できる場合、それらのアイテムをタブ内の中心的な場所に表示できると良いでしょう。詳細については、[タブのデザイン](../../tabs/design/tabs.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d1adb-227">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="タブを使用してボットのコンテンツを整理する方法を示す例。" border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="d1adb-229">ボットの管理</span><span class="sxs-lookup"><span data-stu-id="d1adb-229">Manage a bot</span></span>

<span data-ttu-id="d1adb-230">ユーザーがボットの設定を変更できるようにします。</span><span class="sxs-lookup"><span data-stu-id="d1adb-230">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="d1adb-231">この機能をボット コマンドで提供することもできますが、通常は [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) にすべての設定を含める方が効率的です (次に例を示します)。</span><span class="sxs-lookup"><span data-stu-id="d1adb-231">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="ボットの設定を構成するタスク モジュールを示す例。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="d1adb-233">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="d1adb-233">Best practices</span></span>

<span data-ttu-id="d1adb-234">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-234">Use these recommendations to create a quality app experience.</span></span>

### <a name="content"></a><span data-ttu-id="d1adb-235">コンテンツ</span><span class="sxs-lookup"><span data-stu-id="d1adb-235">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="明確なペルサを確立するためのボットのベスト プラクティスを示す例。" border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="d1adb-237">するべきこと: 明確なペルソナの設定</span><span class="sxs-lookup"><span data-stu-id="d1adb-237">Do: Establish a clear persona</span></span>

<span data-ttu-id="d1adb-238">お使いのボットのトーンは、親しみやすく軽快なものか、”事実だけを伝える” ものか、それとも超気まぐれか。</span><span class="sxs-lookup"><span data-stu-id="d1adb-238">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="d1adb-239">さまざまなシナリオでどのように対応すべきか。</span><span class="sxs-lookup"><span data-stu-id="d1adb-239">How should it respond in different scenarios?</span></span> <span data-ttu-id="d1adb-240">ボットのペルソナを計画して文書化することで、自然でまとまりのある応答を簡単に記述することができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-240">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="d1adb-241">ボット向けの記述の詳細については、「<a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma)</a>」参照してください。</span><span class="sxs-lookup"><span data-stu-id="d1adb-241">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="ボットが実行できる操作を明確に伝える例。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="d1adb-243">するべきこと: ボットにできることを明確に伝達する</span><span class="sxs-lookup"><span data-stu-id="d1adb-243">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="d1adb-244">ウェルカム メッセージやツアーでは、お使いのボットでできることを理解してもらいます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-244">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="ボットの機能をあいまいにしない例。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="d1adb-246">してはいけないこと: ボットの機能をぼかす</span><span class="sxs-lookup"><span data-stu-id="d1adb-246">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="d1adb-247">第一印象は大切です。</span><span class="sxs-lookup"><span data-stu-id="d1adb-247">First impressions matter.</span></span> <span data-ttu-id="d1adb-248">何の変哲もないサインイン メッセージが表示されると、ユーザーは混乱したり疑ったりするでしょう。</span><span class="sxs-lookup"><span data-stu-id="d1adb-248">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="ボットを表示する例は、質問以外を認識する必要があります。" border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="d1adb-250">するべきこと: ノンクエスチョンを認識する</span><span class="sxs-lookup"><span data-stu-id="d1adb-250">Do: Recognize non-questions</span></span>

<span data-ttu-id="d1adb-251">ボットは、"やあ"、"ヘルプ"、"ありがとう" などのメッセージに対応し、一般的なスペルミスや口語表現にも対応できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-251">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="単純なボット メッセージに対する不器用な応答を回避する必要がある例。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="d1adb-253">してはいけないこと: 喜ぶチャンスを逃す</span><span class="sxs-lookup"><span data-stu-id="d1adb-253">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="d1adb-254">ユーザーの中には、実際の人間との会話のような自然な流れを期待する人もいます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-254">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="d1adb-255">シンプルなメッセージには無難な返答を心がけましょう。</span><span class="sxs-lookup"><span data-stu-id="d1adb-255">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="d1adb-256">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="d1adb-256">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="ボットを表示する例は、ユーザーがボットの使い方を理解するのに役立ちます。" border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="d1adb-258">するべきこと: ヘルプを用意する</span><span class="sxs-lookup"><span data-stu-id="d1adb-258">Do: Provide help</span></span>

<span data-ttu-id="d1adb-259">ボットが要求を満たせない場合は、ボットとの対話についてボット自身を教育するための方法をユーザーが用意します。</span><span class="sxs-lookup"><span data-stu-id="d1adb-259">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="ボットを表示する例では、ユーザーを立ち往生してはならない。" border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="d1adb-261">してはいけないこと: ユーザーを立ち往生させる</span><span class="sxs-lookup"><span data-stu-id="d1adb-261">Don't: Leave users stranded</span></span>

<span data-ttu-id="d1adb-262">問題を解決できなければ、ユーザーはすぐにボットを放棄してしまいます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-262">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="d1adb-263">複雑な相互作用</span><span class="sxs-lookup"><span data-stu-id="d1adb-263">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="複雑な操作のためにボットでタスク モジュールまたはタブを使用できる例を示します。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="d1adb-265">するべきこと: タスク モジュールやタブの使用</span><span class="sxs-lookup"><span data-stu-id="d1adb-265">Do: Use task modules or tabs</span></span>

<span data-ttu-id="d1adb-266">ボットが答えを出しても、さらにいくつかの手順が必要な場合は、タスク モジュールやタブにリンクして、タスクやフローを完成させることができます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-266">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="ボットがマルチターン操作を回避する方法を示す例。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="d1adb-268">してはいけないこと: 複数回の対話を面倒にする</span><span class="sxs-lookup"><span data-stu-id="d1adb-268">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="d1adb-269">単一のタスクを完了するのに膨大な量の会話をするのは時間がかかり、複雑すぎます。</span><span class="sxs-lookup"><span data-stu-id="d1adb-269">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="d1adb-270">また、開発者は、状態の変化 (会話がタイムアウトしたり、”キャンセル” メッセージを送信するなど) を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-270">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="d1adb-271">プライバシー</span><span class="sxs-lookup"><span data-stu-id="d1adb-271">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="ボットが個人のコンテキストで個人情報のみを表示する方法を示す例。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="d1adb-273">するべきこと: 機密情報を個人的なコンテキストでのみ表示する</span><span class="sxs-lookup"><span data-stu-id="d1adb-273">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="d1adb-274">ボットがグループ チャットやチャネル内にある場合は、機密情報を閲覧するために、ユーザーをプライベートな場所 (タスク モジュール、タブ、ブラウザなど) に誘導することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d1adb-274">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="ボットがグループまたはユーザーに機密情報を表示しない方法を示す例。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="d1adb-276">してはいけないこと: すべてのユーザーが閲覧できないコンテンツがある</span><span class="sxs-lookup"><span data-stu-id="d1adb-276">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="d1adb-277">お使いのボットでは、機密情報をグループに公開してはいけません。</span><span class="sxs-lookup"><span data-stu-id="d1adb-277">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="d1adb-278">関連項目</span><span class="sxs-lookup"><span data-stu-id="d1adb-278">See also</span></span>

<span data-ttu-id="d1adb-279">以下のガイドラインは、ボット デザインに役立つ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d1adb-279">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="d1adb-280">個人用アプリをデザインする</span><span class="sxs-lookup"><span data-stu-id="d1adb-280">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="d1adb-281">アダプティブ カードをデザインする</span><span class="sxs-lookup"><span data-stu-id="d1adb-281">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="d1adb-282">タスク モジュールをデザインする</span><span class="sxs-lookup"><span data-stu-id="d1adb-282">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
