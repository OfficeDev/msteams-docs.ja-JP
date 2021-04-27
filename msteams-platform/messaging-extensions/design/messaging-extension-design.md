---
title: メッセージング拡張機能の設計
description: Teams メッセージング拡張機能を設計し、Microsoft Teams UI キットを取得する方法について説明します。
keywords: teams の設計ガイドラインは、メッセージング拡張機能のヒントのベスト プラクティスを参照します。
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: e3e4197e461f6d13f0c45ba2ce8bfb93b01b5e0f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020724"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="17de9-104">Microsoft Teams メッセージング拡張機能の設計</span><span class="sxs-lookup"><span data-stu-id="17de9-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="17de9-105">メッセージング拡張機能は、アプリコンテンツを挿入したり、会話から離れることなくメッセージに作用するためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="17de9-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="17de9-106">アプリの設計をガイドするために、次の情報は、Teams でユーザーがメッセージング拡張機能を追加、使用、および管理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="17de9-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="17de9-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="17de9-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="17de9-108">Microsoft Teams UI Kit には、必要に応じて取得および変更できる要素を含む、包括的なメッセージング拡張機能の設計ガイドラインがあります。</span><span class="sxs-lookup"><span data-stu-id="17de9-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="17de9-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="17de9-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="17de9-110">メッセージング拡張機能の追加</span><span class="sxs-lookup"><span data-stu-id="17de9-110">Add a messaging extension</span></span>

<span data-ttu-id="17de9-111">メッセージング拡張機能は、次の Teams コンテキストに追加できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="17de9-112">Teams ストア (AppSource) から。</span><span class="sxs-lookup"><span data-stu-id="17de9-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="17de9-113">作成ボックスの近くのチャネル、チャット、または会議 (前、中、および後)。</span><span class="sxs-lookup"><span data-stu-id="17de9-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="17de9-114">これらの場所の 1 つでメッセージング拡張機能を追加する場合は、そのコンテキストでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="17de9-115">次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="17de9-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="17de9-117">メッセージング拡張機能を設定する</span><span class="sxs-lookup"><span data-stu-id="17de9-117">Set up a messaging extension</span></span>

<span data-ttu-id="17de9-118">認証は必須ではありませんが、アプリがチケット追跡ツールのようなものである場合は、メッセージング拡張機能を使用するためにサインインするユーザーが必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="17de9-119">Teams アプリ全体で一貫性を保つには、サインイン画面をカスタマイズできない。</span><span class="sxs-lookup"><span data-stu-id="17de9-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="17de9-120">シングル サインオン (SSO) 認証を使用する場合、ユーザーは自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="17de9-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="例では、サインイン ボタンを使用してメッセージング拡張機能のセットアップ画面を表示します。" border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="17de9-122">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="17de9-122">Types of messaging extensions</span></span>

<span data-ttu-id="17de9-123">メッセージング拡張機能には、検索コマンド、アクション コマンド、または両方を指定できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="17de9-124">コマンドは、アプリの機能と Teams の使用例に適合する方法によって異なっています。</span><span class="sxs-lookup"><span data-stu-id="17de9-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="17de9-125">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="17de9-125">Search commands</span></span>

<span data-ttu-id="17de9-126">検索コマンドを使用すると、ユーザーはメッセージング拡張機能を使用して外部コンテンツをすばやく検索し、メッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="17de9-127">検索コマンドは、通常、作成ボックスで使用できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="17de9-128">たとえば、Teams を離れることなく、コンテンツを共有することでディスカッションを開始または追加できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例は、作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="17de9-130">作成ボックスのレイアウト オプション</span><span class="sxs-lookup"><span data-stu-id="17de9-130">Compose box layout options</span></span>

<span data-ttu-id="17de9-131">リストビューやグリッド ビューなど、メッセージング拡張機能の検索結果を表示 [するためのいくつかのオプションがあります](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。</span><span class="sxs-lookup"><span data-stu-id="17de9-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能の検索結果のレイアウト オプションを示す図。" border="false":::

### <a name="action-commands"></a><span data-ttu-id="17de9-133">操作コマンド</span><span class="sxs-lookup"><span data-stu-id="17de9-133">Action commands</span></span>

<span data-ttu-id="17de9-134">アクション コマンドを使用すると、ユーザーは Teams 内の外部サービスでアクションをトリガーし、要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="17de9-135">たとえば、アプリで注文を追跡する場合、ユーザーはチャット内から同僚のメッセージの内容を使用して新しい注文を作成できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="17de9-136">アクション ベースのメッセージング拡張機能では、多くの場合、モーダル内でフォームまたは他の種類の構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="17de9-137">これらのエクスペリエンスは、タスク モジュールで [作成できます](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="17de9-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="17de9-138">メッセージング拡張機能を開く</span><span class="sxs-lookup"><span data-stu-id="17de9-138">Open a messaging extension</span></span>

<span data-ttu-id="17de9-139">作成ボックスとメッセージ/投稿は、ユーザーがメッセージング拡張機能を使用する主要なコンテキストです。</span><span class="sxs-lookup"><span data-stu-id="17de9-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="17de9-140">作成ボックスから</span><span class="sxs-lookup"><span data-stu-id="17de9-140">From the compose box</span></span>

<span data-ttu-id="17de9-141">追加すると、ユーザーは作成ボックスの下にあるアプリ アイコンを選択して、メッセージング拡張機能を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="17de9-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="17de9-142">この例では、拡張機能に検索コマンドとアクション コマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="17de9-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="17de9-144">チャット メッセージまたはチャネル投稿から</span><span class="sxs-lookup"><span data-stu-id="17de9-144">From a chat message or channel post</span></span>

追加すると、ユーザーはチャット メッセージまたはチャネル投稿の [その他] アイコンを選択して、拡張機能の :::image type="icon" source="../../assets/icons/teams-client-more.png"::: アクション コマンドを見つけることができます。 <span data-ttu-id="17de9-146">拡張機能が [使用状況に基づくその他 **のアクション] の下** に表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="17de9-147">Microsoft Teams モバイル プラットフォームでは、チャット メッセージまたはチャネル投稿からのその他のアクションのサポートは利用できません。</span><span class="sxs-lookup"><span data-stu-id="17de9-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="17de9-148">チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="17de9-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャット メッセージからメッセージング拡張機能を開く方法を示しています。" border="false":::

#### <a name="channel-post"></a><span data-ttu-id="17de9-150">チャネル投稿</span><span class="sxs-lookup"><span data-stu-id="17de9-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="例は、チャネル投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="17de9-152">メッセージング拡張機能を使用する</span><span class="sxs-lookup"><span data-stu-id="17de9-152">Use a messaging extension</span></span>

<span data-ttu-id="17de9-153">次のシナリオは、ユーザーがメッセージング拡張機能を使用する主な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="17de9-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="17de9-154">メッセージにコンテンツを挿入する</span><span class="sxs-lookup"><span data-stu-id="17de9-154">Insert content into a message</span></span>

<span data-ttu-id="17de9-155">**1. メッセージング拡張機能を選択します**。</span><span class="sxs-lookup"><span data-stu-id="17de9-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="17de9-156">ユーザーは、作成ボックスから共有するコンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="例は、作成ボックスから挿入するコンテンツを検索しているユーザーを示しています。" border="false":::

<span data-ttu-id="17de9-158">**2. コンテンツを挿入します**。</span><span class="sxs-lookup"><span data-stu-id="17de9-158">**2. Insert content**.</span></span> <span data-ttu-id="17de9-159">投稿後、他のユーザーはコンテンツに返信または選択して、アプリの詳細を表示できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="例は、チャネル会話にコンテンツを投稿するユーザーを示しています。" border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="17de9-161">メッセージに対してアクションを実行する</span><span class="sxs-lookup"><span data-stu-id="17de9-161">Take action on a message</span></span>

<span data-ttu-id="17de9-162">**1. メッセージング拡張機能を選択します**。</span><span class="sxs-lookup"><span data-stu-id="17de9-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="17de9-163">アプリには、1 つ以上のアクション コマンドを含めできます。</span><span class="sxs-lookup"><span data-stu-id="17de9-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="例は、メッセージング拡張機能アクション コマンドを選択しているユーザーを示しています。" border="false":::

<span data-ttu-id="17de9-165">**2. アクションを完了します**。</span><span class="sxs-lookup"><span data-stu-id="17de9-165">**2. Complete the action**.</span></span> <span data-ttu-id="17de9-166">アプリは、メッセージ アクションによって送信されたコンテンツまたはデータを受信および処理できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="17de9-167">これにより、ユーザーは会話を続け、次の例では、アプリに直接情報を入力する心配はありません。</span><span class="sxs-lookup"><span data-stu-id="17de9-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="メッセージに対してアクションを実行する方法の例。" border="false":::

### <a name="preview-links"></a><span data-ttu-id="17de9-169">リンクのプレビュー</span><span class="sxs-lookup"><span data-stu-id="17de9-169">Preview links</span></span>

<span data-ttu-id="17de9-170">メッセージング拡張機能を使用すると、認識された URL からメッセージにリッチ リンクを挿入することもできます (この機能はリンク解除と [呼ばれる](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="17de9-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="17de9-171">**1. 作成ボックスに認識されたリンク** を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="17de9-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="例では、ユーザーがコンポスト ボックスにリンクを貼り付けする例を示します。" border="false":::

<span data-ttu-id="17de9-173">**2. コンテンツを挿入します**。</span><span class="sxs-lookup"><span data-stu-id="17de9-173">**2. Insert content**.</span></span> <span data-ttu-id="17de9-174">アプリが作成ボックス内の URL を認識すると、リンクは、Web コンテンツのコンテンツリッチ プレビューを提供するカードとしてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="17de9-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="17de9-175">(詳細 [については、「アダプティブ カードの設計ガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="17de9-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="例は、URL がアプリによって認識されるので、作成ボックスにリッチ コンテンツを含む方法を示しています。" border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="17de9-177">メッセージング拡張機能の管理</span><span class="sxs-lookup"><span data-stu-id="17de9-177">Manage a messaging extension</span></span>

<span data-ttu-id="17de9-178">アイコンを右クリックすると、ユーザーはメッセージング拡張機能をピン留め、削除、または構成できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="17de9-179">構造</span><span class="sxs-lookup"><span data-stu-id="17de9-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="17de9-180">作成ボックスのメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="17de9-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="17de9-181">次の例は、作成ボックスから開いたメッセージング拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="17de9-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="作成ボックスのメッセージング拡張機能の UI 構造を示す図。" border="false":::

|<span data-ttu-id="17de9-183">カウンター</span><span class="sxs-lookup"><span data-stu-id="17de9-183">Counter</span></span>|<span data-ttu-id="17de9-184">説明</span><span class="sxs-lookup"><span data-stu-id="17de9-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="17de9-185">1</span><span class="sxs-lookup"><span data-stu-id="17de9-185">1</span></span>|<span data-ttu-id="17de9-186">**アプリのロゴ**: アプリのロゴの色のアイコン。</span><span class="sxs-lookup"><span data-stu-id="17de9-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="17de9-187">2</span><span class="sxs-lookup"><span data-stu-id="17de9-187">2</span></span>|<span data-ttu-id="17de9-188">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="17de9-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="17de9-189">3</span><span class="sxs-lookup"><span data-stu-id="17de9-189">3</span></span>|<span data-ttu-id="17de9-190">**[アクション コマンド] メニュー アイコン (オプション)**: メッセージング拡張機能のアクション コマンドの一覧を開きます (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="17de9-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="17de9-191">4</span><span class="sxs-lookup"><span data-stu-id="17de9-191">4</span></span>|<span data-ttu-id="17de9-192">**[検索]** ボックス : ユーザーが挿入するアプリ コンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="17de9-193">5</span><span class="sxs-lookup"><span data-stu-id="17de9-193">5</span></span>|<span data-ttu-id="17de9-194">**タブ メニュー (オプション)**: 複数のコンテンツ カテゴリを提供します。</span><span class="sxs-lookup"><span data-stu-id="17de9-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="17de9-195">6</span><span class="sxs-lookup"><span data-stu-id="17de9-195">6</span></span>|<span data-ttu-id="17de9-196">**[アクション コマンド] メニュー (オプション)**: アクション コマンドの一覧を表示します (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="17de9-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="17de9-197">7</span><span class="sxs-lookup"><span data-stu-id="17de9-197">7</span></span>|<span data-ttu-id="17de9-198">**アプリのコンテンツ**: 主に検索結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="17de9-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="17de9-199">この例では、リスト レイアウトを使用しています (グリッド レイアウトは別のオプションです)。</span><span class="sxs-lookup"><span data-stu-id="17de9-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="17de9-200">8</span><span class="sxs-lookup"><span data-stu-id="17de9-200">8</span></span>|<span data-ttu-id="17de9-201">**アプリのロゴ**: アプリロゴのアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="17de9-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="17de9-202">メッセージング拡張機能の管理メニュー</span><span class="sxs-lookup"><span data-stu-id="17de9-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能管理メニューの UI 構造を示す図。" border="false":::

|<span data-ttu-id="17de9-204">カウンター</span><span class="sxs-lookup"><span data-stu-id="17de9-204">Counter</span></span>|<span data-ttu-id="17de9-205">説明</span><span class="sxs-lookup"><span data-stu-id="17de9-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="17de9-206">1</span><span class="sxs-lookup"><span data-stu-id="17de9-206">1</span></span>|<span data-ttu-id="17de9-207">**[ピン留め** 解除] : ユーザーがアプリをピン留めしている場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="17de9-208">2</span><span class="sxs-lookup"><span data-stu-id="17de9-208">2</span></span>|<span data-ttu-id="17de9-209">**削除**: チャネル、チャット、または会議からメッセージング拡張機能を削除します。</span><span class="sxs-lookup"><span data-stu-id="17de9-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="17de9-210">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="17de9-210">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="17de9-211">セットアップと一般的な使用方法</span><span class="sxs-lookup"><span data-stu-id="17de9-211">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="セットアップと一般的な使用方法の例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="17de9-213">Do: シングル サインオンとの統合</span><span class="sxs-lookup"><span data-stu-id="17de9-213">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="17de9-214">SSO を使用すると、サインイン プロセスが簡単、高速、およびセキュリティで保護されます。</span><span class="sxs-lookup"><span data-stu-id="17de9-214">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="17de9-215">また、ユーザーが個人用アプリに既にサインインしている場合は、メッセージング拡張機能にアクセスするためにもう一度サインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="17de9-215">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="シングル サインオンとの統合の例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="17de9-217">[しない]: ユーザーを会話から離す</span><span class="sxs-lookup"><span data-stu-id="17de9-217">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="17de9-218">メッセージング拡張機能は、コンテキストの切り替えを減らすことが想定されるショートカットです。</span><span class="sxs-lookup"><span data-stu-id="17de9-218">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="17de9-219">拡張機能は、たとえば、Teams の外部の Web ページにユーザーを指示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-219">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="17de9-220">Do: メッセージング拡張機能を強調表示する</span><span class="sxs-lookup"><span data-stu-id="17de9-220">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="17de9-221">メッセージング拡張機能は、必ずしも簡単に見つけることができるとは限らない。</span><span class="sxs-lookup"><span data-stu-id="17de9-221">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="17de9-222">アプリの詳細ページに、その使い方のスクリーンショットを含める。</span><span class="sxs-lookup"><span data-stu-id="17de9-222">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="17de9-223">アプリにボットも含まれる場合は、ボットウェルカム ツアーにメッセージング拡張機能のヘルプ ドキュメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="17de9-223">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="17de9-224">テンプレート</span><span class="sxs-lookup"><span data-stu-id="17de9-224">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="テンプレートの例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="17de9-226">Do: 可能であれば、Teams が設計作業の一部を処理する</span><span class="sxs-lookup"><span data-stu-id="17de9-226">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="17de9-227">使用例に合う場合は、検索ベースのメッセージング拡張機能の作成を検討してください。</span><span class="sxs-lookup"><span data-stu-id="17de9-227">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="17de9-228">Teams は、これらの種類の拡張機能を、組み込みのユーザー設定とアクセシビリティでレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="17de9-228">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="設計作業の処理例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="17de9-230">[しない] タスク モジュールにアプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="17de9-230">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="17de9-231">メッセージング拡張機能でアクション コマンドが必要な場合は、タスク モジュールをシンプルにし、アクションを完了するために必要なコンポーネントのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="17de9-231">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="17de9-232">テーマ</span><span class="sxs-lookup"><span data-stu-id="17de9-232">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="例: それらを使用します。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="17de9-234">Do: Teams カラー トークンを活用する</span><span class="sxs-lookup"><span data-stu-id="17de9-234">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="17de9-235">各 Teams テーマには、独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-235">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="17de9-236">テーマの変更を自動的に処理するには、デザインでカラー <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">トークン (Fluent UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="17de9-236">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="カラー トークンの例。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="17de9-238">[しない] : ハード コードの色の値</span><span class="sxs-lookup"><span data-stu-id="17de9-238">Don't: Hard code color values</span></span>

<span data-ttu-id="17de9-239">Teams カラー トークンを使用しない場合、デザインの拡張性が低く、管理に時間がかかっています。</span><span class="sxs-lookup"><span data-stu-id="17de9-239">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="17de9-240">Actions</span><span class="sxs-lookup"><span data-stu-id="17de9-240">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="アクションの例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="17de9-242">Do: コンテキストで意味のあるアクション コマンドを含める</span><span class="sxs-lookup"><span data-stu-id="17de9-242">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="17de9-243">メッセージアクションは、ユーザーが見ているものに関連する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-243">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="17de9-244">たとえば、ユーザーの投稿のテキストを使用して、問題や作業項目を作成するためのショートカットをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="17de9-244">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="アクション コマンドの例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="17de9-246">[しない]: コンテキストに依存しないアクション コマンドを含める</span><span class="sxs-lookup"><span data-stu-id="17de9-246">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="17de9-247">[ダッシュボードを表示する] というメッセージ **アクションは** 、ほとんどの会話から切断されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-247">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="17de9-248">検索</span><span class="sxs-lookup"><span data-stu-id="17de9-248">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="17de9-249">Do: 入力中に検索結果を表示する</span><span class="sxs-lookup"><span data-stu-id="17de9-249">Do: Show search results while typing</span></span>

<span data-ttu-id="17de9-250">ユーザーが入力している間に、検索結果の候補を提供します。</span><span class="sxs-lookup"><span data-stu-id="17de9-250">Provide suggested search results while users type.</span></span> <span data-ttu-id="17de9-251">最小限の文字数で、必要なコンテンツをより速く見つける場合があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-251">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="17de9-252">[しない]: ユーザーにクエリの送信を要求する</span><span class="sxs-lookup"><span data-stu-id="17de9-252">Don't: Require users to submit a query</span></span>

<span data-ttu-id="17de9-253">ユーザーにキーを押させるか、ボタンを選択してアプリにクエリを送信できます。</span><span class="sxs-lookup"><span data-stu-id="17de9-253">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="17de9-254">アプリ サービス サービスの方が簡単ですが、ユーザーは、入力時にリアルタイムの検索結果が表示されないと混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-254">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="17de9-255">Do: ゼロ用語クエリを検討する</span><span class="sxs-lookup"><span data-stu-id="17de9-255">Do: Consider zero-term queries</span></span>

<span data-ttu-id="17de9-256">たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示した情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="17de9-256">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="17de9-257">会話にコンテンツを挿入する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-257">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="17de9-258">デザインを検証する</span><span class="sxs-lookup"><span data-stu-id="17de9-258">Validate your design</span></span>

<span data-ttu-id="17de9-259">AppSource にアプリを公開する予定がある場合、アプリの提出時に失敗する原因となるデザイン上の問題を理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="17de9-259">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="17de9-260">デザイン検証ガイドラインをチェックする</span><span class="sxs-lookup"><span data-stu-id="17de9-260">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
