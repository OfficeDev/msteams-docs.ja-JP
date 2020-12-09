---
title: Bot の設計
description: Teams bot を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605494"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="96b27-103">Microsoft Teams bot の設計</span><span class="sxs-lookup"><span data-stu-id="96b27-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="96b27-104">Bot は、特定のタスクセットを実行する会話アプリです。</span><span class="sxs-lookup"><span data-stu-id="96b27-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="96b27-105">Bot は、 <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot フレームワーク</a>に基づいてユーザーと通信し、質問に応答して、変更やその他のイベントについて事前に通知します。</span><span class="sxs-lookup"><span data-stu-id="96b27-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="96b27-106">これらは、お客に到達するための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="96b27-106">They're a great way to reach out.</span></span>

<span data-ttu-id="96b27-107">アプリの設計をガイドするには、次の情報を参照してください。 Teams でボットを追加、使用、管理する方法について説明しています。</span><span class="sxs-lookup"><span data-stu-id="96b27-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="96b27-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="96b27-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="96b27-109">Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、より包括的な bot 設計ガイドラインを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="96b27-110">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="96b27-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="96b27-111">Bot を追加する</span><span class="sxs-lookup"><span data-stu-id="96b27-111">Add a bot</span></span>

<span data-ttu-id="96b27-112">Bot は、チャット、チャネル、および個人用アプリで利用できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="96b27-113">Bot を追加するには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="96b27-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="96b27-114">Teams ストア (AppSource) から。</span><span class="sxs-lookup"><span data-stu-id="96b27-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="96b27-115">Teams の左側にある [ **その他** ] アイコンを選択して、アプリのポップアップを使用します。</span><span class="sxs-lookup"><span data-stu-id="96b27-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="96b27-116">新しいチャットまたは新規作成ボックスに @mention します (次の例は、グループチャットでこの操作を実行する方法を示しています)。</span><span class="sxs-lookup"><span data-stu-id="96b27-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="例は、@mention を使用してグループチャットに bot を追加する方法を示しています。" border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="96b27-118">Bot を導入する</span><span class="sxs-lookup"><span data-stu-id="96b27-118">Introduce a bot</span></span>

<span data-ttu-id="96b27-119">Bot が自らを導入し、その機能について説明していることが重要です。</span><span class="sxs-lookup"><span data-stu-id="96b27-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="96b27-120">この最初の exchange は、ユーザーが bot との関係を理解し、制限事項を確認します。</span><span class="sxs-lookup"><span data-stu-id="96b27-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="96b27-121">ワンワンチャットでのウェルカムメッセージ</span><span class="sxs-lookup"><span data-stu-id="96b27-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="96b27-122">個人のコンテキストでは、ウェルカムメッセージに bot の雰囲気が設定されます。</span><span class="sxs-lookup"><span data-stu-id="96b27-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="96b27-123">メッセージには、案内応答、bot が実行できること、および操作方法に関するいくつかの提案が含まれています (たとえば、「質問してください...」)。</span><span class="sxs-lookup"><span data-stu-id="96b27-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact (for example, “Try asking me about …”).</span></span> <span data-ttu-id="96b27-124">可能であれば、これらの提案は、サインインせずに、保存された応答を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-124">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="例は、個人アプリでの bot の紹介を示しています。" border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="96b27-126">グループチャットとチャネルでの紹介</span><span class="sxs-lookup"><span data-stu-id="96b27-126">Introductions in group chats and channels</span></span>

<span data-ttu-id="96b27-127">Bot の紹介は、個人のコンテキスト (個人のアプリなど) と比較して、グループのチャットとチャネルにおいて少し異なるものにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-127">Your bot's introduction should be slightly little different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="96b27-128">実際には、入室したチャットルームがある場合は、「人」と入力します。既にあるすべてのユーザーを歓迎するのではなく、自分で紹介します。</span><span class="sxs-lookup"><span data-stu-id="96b27-128">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="96b27-129">Bot 設計に対してそのような考えを行います。</span><span class="sxs-lookup"><span data-stu-id="96b27-129">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="例は、共同作業コンテキストでの bot の紹介を示しています。" border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="96b27-131">シングルサインオンを使用した Bot 認証</span><span class="sxs-lookup"><span data-stu-id="96b27-131">Bot authentication with single sign-on</span></span>

<span data-ttu-id="96b27-132">ユーザーが bot にメッセージを送信すると、サインインが必要になる場合があります。そのすべての機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="96b27-132">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="96b27-133">シングルサインオン (SSO) を使用して認証プロセスを簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-133">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="96b27-134">忘れることはありません。 bot のコマンドメニュー (**何ができますか**) で、サインアウトするコマンドも提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-134">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="例は、[サインイン] ボタンがある bot を示しています。" border="false":::

### <a name="tours"></a><span data-ttu-id="96b27-136">ガイド</span><span class="sxs-lookup"><span data-stu-id="96b27-136">Tours</span></span>

<span data-ttu-id="96b27-137">ウェルカムメッセージにツアーを含めることができます。また、bot が "help" コマンドのように応答します。</span><span class="sxs-lookup"><span data-stu-id="96b27-137">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="96b27-138">ツアーは、bot が実行できることを理解するための最も効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="96b27-138">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="96b27-139">また、必要に応じて、アプリのその他の機能 (たとえば、メッセージング内線番号のスクリーンショットを含む) を記述するのにも適しています。</span><span class="sxs-lookup"><span data-stu-id="96b27-139">If applicable, they’re also great for describing your app’s other features (for example, include screenshots of your messaging extension).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96b27-140">ツアーは、サインインしなくてもアクセス可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-140">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="96b27-141">1対1のチャット</span><span class="sxs-lookup"><span data-stu-id="96b27-141">One-on-one chats</span></span>

<span data-ttu-id="96b27-142">個人アプリでは、カルーセルを使用して、ボットとアプリのその他の機能の効果的な概要を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-142">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="96b27-143">ボタンを含む [ユーザーに **タスクを実行する**] コマンドを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="96b27-143">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="例は、1対1のチャットでの bot ツアーを示しています。" border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="96b27-145">チャネルとグループのチャット</span><span class="sxs-lookup"><span data-stu-id="96b27-145">Channels and group chats</span></span>

<span data-ttu-id="96b27-146">チャネルおよびグループチャットでは、進行中の会話を中断しないように、ツアーはモーダル ( [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) とも呼ばれます) で開きます。</span><span class="sxs-lookup"><span data-stu-id="96b27-146">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="96b27-147">これにより、ツアーの役割ベースのビューを実装するオプションも提供されます。</span><span class="sxs-lookup"><span data-stu-id="96b27-147">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="例は、チャネル内の bot ツアーを示しています。" border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="96b27-149">Bot とのチャット</span><span class="sxs-lookup"><span data-stu-id="96b27-149">Chat with a bot</span></span>

<span data-ttu-id="96b27-150">Bot は、チームのメッセージングフレームワークに直接統合されます。</span><span class="sxs-lookup"><span data-stu-id="96b27-150">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="96b27-151">ユーザーは bot とチャットすることで、疑問を解決したり、コマンドを入力して、小または特定の一連のタスクを実行したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-151">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="96b27-152">Bot は、チャット経由でアプリの変更や更新に関するユーザーに積極的な通知を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-152">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="96b27-153">異なるコンテキストにある bot とのチャット</span><span class="sxs-lookup"><span data-stu-id="96b27-153">Chat with a bot in different contexts</span></span>

<span data-ttu-id="96b27-154">Bot は、次のコンテキストで使用できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-154">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="96b27-155">**個人アプリ**: 個人アプリでは、ボットには専用のチャットタブがあります。</span><span class="sxs-lookup"><span data-stu-id="96b27-155">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="96b27-156">**ワンワンチャット**: ユーザーはボットでプライベート会話を開始できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-156">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="96b27-157">個人アプリで bot を使用した場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="96b27-157">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="96b27-158">**グループチャット**: ユーザーは bot を @mentioning ことで、グループチャットの bot と対話できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-158">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="96b27-159">**チャネル**: ユーザーはチャネル内の bot と対話できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-159">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="96b27-160">[新規作成] ボックスに bot 名を @mentioning します。</span><span class="sxs-lookup"><span data-stu-id="96b27-160">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="96b27-161">このコンテキストでは、ボットはチャネルだけでなく、チーム全体で利用可能であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="96b27-161">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="96b27-162">構造</span><span class="sxs-lookup"><span data-stu-id="96b27-162">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="例は、bot の構造的な構造を示しています。" border="false":::

|<span data-ttu-id="96b27-164">カウンター</span><span class="sxs-lookup"><span data-stu-id="96b27-164">Counter</span></span>|<span data-ttu-id="96b27-165">説明</span><span class="sxs-lookup"><span data-stu-id="96b27-165">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="96b27-166">1</span><span class="sxs-lookup"><span data-stu-id="96b27-166">1</span></span>|<span data-ttu-id="96b27-167">**アプリの名前とアイコン**</span><span class="sxs-lookup"><span data-stu-id="96b27-167">**App name and icon**</span></span>|
|<span data-ttu-id="96b27-168">2 </span><span class="sxs-lookup"><span data-stu-id="96b27-168">2</span></span>|<span data-ttu-id="96b27-169">**[チャット] タブ**: bot と会話するためのスペースを開きます (個人アプリにのみ適用されます)。</span><span class="sxs-lookup"><span data-stu-id="96b27-169">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="96b27-170">3 </span><span class="sxs-lookup"><span data-stu-id="96b27-170">3</span></span>|<span data-ttu-id="96b27-171">**カスタムタブ**: アプリに関連するその他のコンテンツを開きます。</span><span class="sxs-lookup"><span data-stu-id="96b27-171">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="96b27-172">4 </span><span class="sxs-lookup"><span data-stu-id="96b27-172">4</span></span>|<span data-ttu-id="96b27-173">**[バージョン情報] タブ**: アプリに関する基本情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="96b27-173">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="96b27-174">5 </span><span class="sxs-lookup"><span data-stu-id="96b27-174">5</span></span>|<span data-ttu-id="96b27-175">**チャットバブル**: ボット会話は Teams メッセージングフレームワークを使用します。</span><span class="sxs-lookup"><span data-stu-id="96b27-175">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="96b27-176">6 </span><span class="sxs-lookup"><span data-stu-id="96b27-176">6</span></span>|<span data-ttu-id="96b27-177">**アダプティブカード**: bot の応答に適応カードが含まれている場合、カードはチャットのバブルの幅全体を占めます。</span><span class="sxs-lookup"><span data-stu-id="96b27-177">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="96b27-178">7 </span><span class="sxs-lookup"><span data-stu-id="96b27-178">7</span></span>|<span data-ttu-id="96b27-179">**コマンドメニュー**: bot の標準コマンド (ユーザーが定義) を表示します。</span><span class="sxs-lookup"><span data-stu-id="96b27-179">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="96b27-180">コマンドメニュー</span><span class="sxs-lookup"><span data-stu-id="96b27-180">Command menu</span></span>

<span data-ttu-id="96b27-181">コマンドメニューには、ボットに常に応答する単語または語句の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="96b27-181">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="96b27-182">ユーザーが bot に conversing ている場合は、[新規作成] ボックスの上にコマンドメニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="96b27-182">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="96b27-183">コマンドが選択されている場合は、メッセージに挿入します。</span><span class="sxs-lookup"><span data-stu-id="96b27-183">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="96b27-184">コマンドの一覧は、短くする必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-184">The list of commands should be brief.</span></span> <span data-ttu-id="96b27-185">このメニューは、bot の主要な機能を強調表示することのみを目的としています。</span><span class="sxs-lookup"><span data-stu-id="96b27-185">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="96b27-186">コマンドは簡潔にしてください。</span><span class="sxs-lookup"><span data-stu-id="96b27-186">Keep commands concise, too.</span></span> <span data-ttu-id="96b27-187">たとえば **、ヘルプというコマンド** を **作成します。**</span><span class="sxs-lookup"><span data-stu-id="96b27-187">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="96b27-188">[コマンド] メニューは、会話の状態に関係なく、常に使用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-188">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="例は bot のコマンドメニューを示しています。" border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="96b27-190">ユーザーが何を言っているかを理解する</span><span class="sxs-lookup"><span data-stu-id="96b27-190">Understand what people are saying</span></span>

<span data-ttu-id="96b27-191">シソーラスを使用して、標準クエリのさまざまな解釈を生成できるように、できるだけ多くの背景からユーザーを取得します。</span><span class="sxs-lookup"><span data-stu-id="96b27-191">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Bot が ' Hello ' を解釈する方法を示す図" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Bot が ' Help ' を解釈する方法を示す図" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Bot が ' 感謝 ' を解釈する方法を示す図" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="96b27-195">メッセージから意図的およびデータを抽出する</span><span class="sxs-lookup"><span data-stu-id="96b27-195">Extract intent and data from messages</span></span>

<span data-ttu-id="96b27-196">意図を認識するように bot を設計し、メッセージまたはクエリに対する応答で bot からの要望を取得します。</span><span class="sxs-lookup"><span data-stu-id="96b27-196">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="96b27-197">インテントは、メッセージまたはクエリを、アクションによって影響を受ける1つ以上のデータオブジェクトを使用して1つのアクションとして分類します。</span><span class="sxs-lookup"><span data-stu-id="96b27-197">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="96b27-198">次の例は、ボットに送信されたメッセージのユーザーの意図とデータの概要を示しています。</span><span class="sxs-lookup"><span data-stu-id="96b27-198">The following examples outline the user intent and data in messages sent to bots.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="「シアトルへのフライトを予約する」という文の例では、ユーザーの目的は「予約」で、データは「シアトル」です。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="例は、「ストアを開いている場合」という文で示されています。ユーザーの意図は ' when ' で、データが ' open ' です。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="「1pm での会議の予約」という文の表示例、ユーザーの目的は ' 1pm ' と ' Bob in Distribution ' のようになっています。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="96b27-202">分析と改善</span><span class="sxs-lookup"><span data-stu-id="96b27-202">Analyze and improve</span></span>

<span data-ttu-id="96b27-203">ユーザーが bot とチャットするときに読み上げられる内容について説明します。</span><span class="sxs-lookup"><span data-stu-id="96b27-203">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="96b27-204">これは、ユーザーベースがさまざまな場所および orgs で増加している間、継続的に反復的なプロセスになります。</span><span class="sxs-lookup"><span data-stu-id="96b27-204">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="96b27-205">Bot の言語認識と意図的なマッピングを Microsoft 言語理解 (LUIS) で調整することができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-205">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="96b27-206">[LUIS につい](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence)て: LUIS が AI を使用してアプリデータに自然言語の理解 (nlu) を提供する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="96b27-206">[Understanding LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="96b27-207">[LUIS との統合](https://www.luis.ai/): コンピューター学習モデルを作成する複雑なプロセスを使用せずに、bot に自然言語機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="96b27-207">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="96b27-208">ユース ケース</span><span class="sxs-lookup"><span data-stu-id="96b27-208">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="96b27-209">単純なクエリ</span><span class="sxs-lookup"><span data-stu-id="96b27-209">Simple queries</span></span>

<span data-ttu-id="96b27-210">Bot は、あいまいさを解決するために、クエリまたは関連する一連の一致項目のグループに正確に一致するものを提供できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-210">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="96b27-211">一致するものがある場合は、リストカードを使用してコンテンツをグループ化します。</span><span class="sxs-lookup"><span data-stu-id="96b27-211">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="例は、bot との簡単なクエリ操作を示しています。" border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="96b27-213">複数ターンの相互作用</span><span class="sxs-lookup"><span data-stu-id="96b27-213">Multi-turn interactions</span></span>

<span data-ttu-id="96b27-214">Bot は完全な要求と質問をサポートできますが、複数ターンの対話を処理できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-214">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="96b27-215">考えられる次の手順により、ユーザーは、包括的な要求を作成することを期待するのではなく、完全なタスクフローを行うことが容易になります。</span><span class="sxs-lookup"><span data-stu-id="96b27-215">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="96b27-216">次の例では、bot は、次に実行する必要のあるオプションを使用して、各メッセージに応答します。</span><span class="sxs-lookup"><span data-stu-id="96b27-216">In the following example, the bot responds to each message with options for what might want to do next.</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="例は、ボットとの相互作用を示しています。" border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="96b27-218">ユーザーに連絡する</span><span class="sxs-lookup"><span data-stu-id="96b27-218">Reach out to users</span></span>

<span data-ttu-id="96b27-219">事前メッセージングでは、bot は、個人、グループチャット、またはチャネルに関連する通知を特定の頻度で送信するダイジェストとして機能することができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-219">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="96b27-220">文書内の内容が変更されたとき、または作業項目が閉じられたときに、bot がメッセージを送信することがあります。</span><span class="sxs-lookup"><span data-stu-id="96b27-220">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="96b27-221">次の例では、ユーザーは、bot が別のチャネルで伝達したトースト通知を取得します。</span><span class="sxs-lookup"><span data-stu-id="96b27-221">In the following example, a user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="例は、bot が別のチャネルからユーザーに対して事前にメッセージングを行うことを示しています。" border="false":::

<span data-ttu-id="96b27-223">これで、そのチャネルでユーザーは bot から自分のメッセージを読むことができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-223">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="例は、bot の事前メッセージを見ているユーザーを示しています。" border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="96b27-225">Bot でタブを使用する</span><span class="sxs-lookup"><span data-stu-id="96b27-225">Use tabs with bots</span></span>

<span data-ttu-id="96b27-226">タブを使用すると、ボットを使いやすくすることができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-226">A tab can make your bot easier to use.</span></span> <span data-ttu-id="96b27-227">たとえば、ボットで作業項目を作成できる場合は、すべてのアイテムを1つのタブ内の中央の場所に表示することをお勧めします。 [タブのデザイン](../../tabs/design/tabs.md)に関する詳細を参照してください。</span><span class="sxs-lookup"><span data-stu-id="96b27-227">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="例は、タブを使用して bot コンテンツを整理する方法を示しています。" border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="96b27-229">Bot を管理する</span><span class="sxs-lookup"><span data-stu-id="96b27-229">Manage a bot</span></span>

<span data-ttu-id="96b27-230">ユーザーは bot の設定を変更できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-230">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="96b27-231">この機能は bot コマンドで提供できますが、通常は、すべての設定を [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) に含めることをお勧めします (次の例を参照)。</span><span class="sxs-lookup"><span data-stu-id="96b27-231">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="例は、bot の設定を構成するためのタスクモジュールを示しています。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="96b27-233">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="96b27-233">Best practices</span></span>

### <a name="content"></a><span data-ttu-id="96b27-234">コンテンツ</span><span class="sxs-lookup"><span data-stu-id="96b27-234">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="96b27-236">Do: 明快なペルソナを設定する</span><span class="sxs-lookup"><span data-stu-id="96b27-236">Do: Establish a clear persona</span></span>

<span data-ttu-id="96b27-237">Bot の雰囲気をよく理解しているかどうか、「ファクトのみ」、またはスーパー quirky?</span><span class="sxs-lookup"><span data-stu-id="96b27-237">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="96b27-238">さまざまなシナリオでどのように対応する必要があるか。</span><span class="sxs-lookup"><span data-stu-id="96b27-238">How should it respond in different scenarios?</span></span> <span data-ttu-id="96b27-239">Bot のペルソナを計画および文書化することで、自然で凝集しているように見える応答を簡単に記述できるようになります。</span><span class="sxs-lookup"><span data-stu-id="96b27-239">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="96b27-240">詳細については、「 <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft TEAMS UI Kit (Figma)</a> 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="96b27-240">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="96b27-242">Do: bot が実行できることを明確に伝える</span><span class="sxs-lookup"><span data-stu-id="96b27-242">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="96b27-243">ウェルカムメッセージとツアーは、ユーザーが bot に対して何ができるかを理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="96b27-243">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="96b27-245">しない: bot の機能を不明瞭にする</span><span class="sxs-lookup"><span data-stu-id="96b27-245">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="96b27-246">最初のインプレッションの問題。</span><span class="sxs-lookup"><span data-stu-id="96b27-246">First impressions matter.</span></span> <span data-ttu-id="96b27-247">Nondescript サインインメッセージが表示された場合、ユーザーが混乱したり疑わしいことがあります。</span><span class="sxs-lookup"><span data-stu-id="96b27-247">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="96b27-249">Do: 質問以外の項目を認識する</span><span class="sxs-lookup"><span data-stu-id="96b27-249">Do: Recognize non-questions</span></span>

<span data-ttu-id="96b27-250">Bot は、よくあるスペルミスと口語を考慮しながら、"Hi"、"Help"、"ありがとうございます" などのメッセージに応答できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-250">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="96b27-252">成功へのチャンスを見逃さないようにします。</span><span class="sxs-lookup"><span data-stu-id="96b27-252">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="96b27-253">ユーザーによっては、実際の人物のような会話を自然に流すことが予想されます。</span><span class="sxs-lookup"><span data-stu-id="96b27-253">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="96b27-254">単純なメッセージへの clumsy 応答を避けるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="96b27-254">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="96b27-255">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="96b27-255">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="96b27-257">Do: ヘルプを提供する</span><span class="sxs-lookup"><span data-stu-id="96b27-257">Do: Provide help</span></span>

<span data-ttu-id="96b27-258">Bot が要求を満たすことができない場合は、ユーザーが bot との対話について自分で教育する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="96b27-258">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="96b27-260">いいえ: ユーザーを残されたままにします</span><span class="sxs-lookup"><span data-stu-id="96b27-260">Don't: Leave users stranded</span></span>

<span data-ttu-id="96b27-261">問題のトラブルシューティングができない場合、ユーザーは bot をすぐに放棄します。</span><span class="sxs-lookup"><span data-stu-id="96b27-261">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="96b27-262">複雑な相互作用</span><span class="sxs-lookup"><span data-stu-id="96b27-262">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="96b27-264">Do: タスクモジュールまたはタブを使用する</span><span class="sxs-lookup"><span data-stu-id="96b27-264">Do: Use task modules or tabs</span></span>

<span data-ttu-id="96b27-265">Bot が応答を提供し、さらにいくつかの手順が必要な場合は、タスクモジュールまたはタブにリンクして、タスクまたはフローを完了できます。</span><span class="sxs-lookup"><span data-stu-id="96b27-265">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="96b27-267">いいえ: 複数ターンの対話を面倒にする</span><span class="sxs-lookup"><span data-stu-id="96b27-267">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="96b27-268">1つのタスクを完了するための広範な会話は、遅く、過度に複雑です。</span><span class="sxs-lookup"><span data-stu-id="96b27-268">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="96b27-269">また、開発者は、状態の変更 (会話のタイムアウト、"キャンセル" メッセージの送信など) を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-269">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="96b27-270">プライバシー</span><span class="sxs-lookup"><span data-stu-id="96b27-270">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="96b27-272">Do: 個人のコンテキストに機密情報のみを表示する</span><span class="sxs-lookup"><span data-stu-id="96b27-272">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="96b27-273">Bot がグループチャットまたはチャネルにある場合は、機密情報を表示するためにユーザーをプライベートな場所 (タスクモジュール、タブ、ブラウザーなど) に送ることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="96b27-273">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="96b27-275">いいえ: 一部のコンテンツは、すべてのユーザーに表示されることを意図したものではありません</span><span class="sxs-lookup"><span data-stu-id="96b27-275">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="96b27-276">Bot は、ユーザーのグループに機密情報を公開することはできません。</span><span class="sxs-lookup"><span data-stu-id="96b27-276">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a><span data-ttu-id="96b27-277">詳細情報</span><span class="sxs-lookup"><span data-stu-id="96b27-277">Learn more</span></span>

<span data-ttu-id="96b27-278">このような他のガイドラインは、ボット設計に役立てることができます。</span><span class="sxs-lookup"><span data-stu-id="96b27-278">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="96b27-279">個人用アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="96b27-279">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="96b27-280">アダプティブカードの設計</span><span class="sxs-lookup"><span data-stu-id="96b27-280">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="96b27-281">タスクモジュールを設計する</span><span class="sxs-lookup"><span data-stu-id="96b27-281">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a><span data-ttu-id="96b27-282">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="96b27-282">Validate your design</span></span>

<span data-ttu-id="96b27-283">アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="96b27-283">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="96b27-284">設計検証ガイドラインの確認</span><span class="sxs-lookup"><span data-stu-id="96b27-284">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
