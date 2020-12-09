---
title: メッセージング拡張機能の設計
description: Teams メッセージング拡張機能を設計し、Microsoft Teams UI キットを取得する方法について説明します。
keywords: teams 設計ガイドラインリファレンスメッセージング拡張のヒントベストプラクティス
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604854"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="9c46c-104">Microsoft Teams メッセージング拡張機能の設計</span><span class="sxs-lookup"><span data-stu-id="9c46c-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="9c46c-105">メッセージング拡張機能は、会話から離れずに、アプリコンテンツを挿入したり、メッセージに対して動作したりするためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="9c46c-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>

<span data-ttu-id="9c46c-106">アプリの設計をガイドするには、次の情報を参照してください。 Teams でのメッセージング拡張機能の追加、使用、および管理の方法を示します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="9c46c-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="9c46c-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="9c46c-108">Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、包括的なメッセージング拡張設計ガイドラインを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9c46c-109">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="9c46c-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="9c46c-110">メッセージング拡張機能を追加する</span><span class="sxs-lookup"><span data-stu-id="9c46c-110">Add a messaging extension</span></span>

<span data-ttu-id="9c46c-111">メッセージング拡張機能は、次の Teams コンテキストで追加できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="9c46c-112">Teams ストア (AppSource) から。</span><span class="sxs-lookup"><span data-stu-id="9c46c-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="9c46c-113">[新規作成] ボックスの近くにあるチャネル、チャット、または会議 (前、中、および後)。</span><span class="sxs-lookup"><span data-stu-id="9c46c-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="9c46c-114">これらのいずれかの場所にメッセージング拡張機能を追加した場合は、そのコンテキストで使用できるだけのことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9c46c-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="9c46c-115">次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9c46c-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの [新規作成] ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="9c46c-117">メッセージング拡張機能を設定する</span><span class="sxs-lookup"><span data-stu-id="9c46c-117">Set up a messaging extension</span></span>

<span data-ttu-id="9c46c-118">認証は必須ではありませんが、アプリがチケット追跡ツールのようなものである場合、メッセージング拡張機能を使用するには、ユーザーにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="9c46c-119">Teams アプリ間での一貫性を保つため、サインイン画面をカスタマイズすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9c46c-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="9c46c-120">シングルサインオン (SSO) 認証を使用する場合、ユーザーは自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="9c46c-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="例は、[サインイン] ボタンがある [メッセージング拡張機能のセットアップ] 画面を示しています。" border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="9c46c-122">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="9c46c-122">Types of messaging extensions</span></span>

<span data-ttu-id="9c46c-123">メッセージング拡張機能には、検索コマンド、アクションコマンド、またはその両方を使用できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="9c46c-124">自分のコマンドは、アプリの機能によって異なり、Teams 内でそれらがどのように使用されるかによっても異なります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="9c46c-125">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="9c46c-125">Search commands</span></span>

<span data-ttu-id="9c46c-126">検索コマンドを使用すると、ユーザーはメッセージング拡張機能を使用して外部コンテンツをすばやく検索し、メッセージに挿入することができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="9c46c-127">検索コマンドは、通常、[新規作成] ボックスで使用できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="9c46c-128">たとえば、Teams を離れることなく、コンテンツを共有することでディスカッションを開始または追加できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例は、[新規作成] ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="9c46c-130">新規作成ボックスのレイアウトオプション</span><span class="sxs-lookup"><span data-stu-id="9c46c-130">Compose box layout options</span></span>

<span data-ttu-id="9c46c-131">[リストビューやグリッドビュー](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)など、メッセージング拡張機能の検索結果を表示するためのいくつかのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能検索結果のレイアウトオプションを示す図" border="false":::

### <a name="action-commands"></a><span data-ttu-id="9c46c-133">操作コマンド</span><span class="sxs-lookup"><span data-stu-id="9c46c-133">Action commands</span></span>

<span data-ttu-id="9c46c-134">アクションコマンドを使用すると、ユーザーは Teams 内の外部サービスでのアクションをトリガーしたり、要求を処理したりできます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="9c46c-135">たとえば、アプリで注文を追跡している場合、ユーザーは、自分のチャットの外部から同僚のメッセージの内容を使用して、新しい注文を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="9c46c-136">アクションベースのメッセージング拡張機能では、多くの場合、ユーザーがモーダル内でフォームまたはその他の種類の構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="9c46c-137">これらのエクスペリエンスは、 [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="9c46c-138">メッセージング拡張機能を開く</span><span class="sxs-lookup"><span data-stu-id="9c46c-138">Open a messaging extension</span></span>

<span data-ttu-id="9c46c-139">新規作成ボックスとメッセージ/投稿は、ユーザーがメッセージング拡張機能を使用するプライマリコンテキストです。</span><span class="sxs-lookup"><span data-stu-id="9c46c-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="9c46c-140">[新規作成] ボックス</span><span class="sxs-lookup"><span data-stu-id="9c46c-140">From the compose box</span></span>

<span data-ttu-id="9c46c-141">追加されたユーザーは、[新規作成] ボックスの下にあるアプリのアイコンを選択することによって、メッセージング拡張機能を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="9c46c-142">この例では、拡張機能に検索コマンドとアクションコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、[新規作成] ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="9c46c-144">チャットメッセージまたはチャネル投稿から</span><span class="sxs-lookup"><span data-stu-id="9c46c-144">From a chat message or channel post</span></span>

追加されたユーザーは、 **More** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: チャットメッセージまたはチャネルの投稿にある [その他] アイコンを選択して、拡張機能のアクションコマンドを見つけることができます。 <span data-ttu-id="9c46c-146">使用状況に応じて、拡張機能が [ **その他のアクション** ] の下に一覧表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-146">Your extension may be listed under **More actions** based on usage.</span></span>

#### <a name="chat-message"></a><span data-ttu-id="9c46c-147">チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="9c46c-147">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャットメッセージからメッセージング拡張機能を開く方法を示しています。" border="false":::

#### <a name="channel-post"></a><span data-ttu-id="9c46c-149">チャネル投稿</span><span class="sxs-lookup"><span data-stu-id="9c46c-149">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="例は、チャネル投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="9c46c-151">メッセージング拡張機能を使用する</span><span class="sxs-lookup"><span data-stu-id="9c46c-151">Use a messaging extension</span></span>

<span data-ttu-id="9c46c-152">次のシナリオは、ユーザーがメッセージング拡張機能を使用する主な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9c46c-152">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="9c46c-153">メッセージにコンテンツを挿入する</span><span class="sxs-lookup"><span data-stu-id="9c46c-153">Insert content into a message</span></span>

<span data-ttu-id="9c46c-154">**1. メッセージング拡張機能を選択** します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-154">**1. Select a messaging extension**.</span></span> <span data-ttu-id="9c46c-155">ユーザーは、[新規作成] ボックスから共有するコンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-155">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="例は、[新規作成] ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

<span data-ttu-id="9c46c-157">**2. コンテンツを挿入** します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-157">**2. Insert content**.</span></span> <span data-ttu-id="9c46c-158">投稿した後、他のユーザーがコンテンツを返信または選択して、アプリに詳細情報を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-158">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="例は、チャネル会話にコンテンツを送信するユーザーを示しています。" border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="9c46c-160">メッセージに対してアクションを実行する</span><span class="sxs-lookup"><span data-stu-id="9c46c-160">Take action on a message</span></span>

<span data-ttu-id="9c46c-161">**1. メッセージング拡張機能を選択** します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-161">**1. Select a messaging extension**.</span></span> <span data-ttu-id="9c46c-162">アプリには、1つ以上のアクションコマンドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-162">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="この例は、メッセージング拡張機能のアクションコマンドを選択するユーザーを示しています。" border="false":::

<span data-ttu-id="9c46c-164">**2. アクションを完了** します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-164">**2. Complete the action**.</span></span> <span data-ttu-id="9c46c-165">アプリは、メッセージアクションによって送信されたコンテンツまたはデータを受信し、処理することができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-165">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="9c46c-166">これにより、ユーザーが自分のアプリに情報を直接入力しても、次の例のような会話に残すことができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-166">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="例は、[新規作成] ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

### <a name="preview-links"></a><span data-ttu-id="9c46c-168">プレビューのリンク</span><span class="sxs-lookup"><span data-stu-id="9c46c-168">Preview links</span></span>

<span data-ttu-id="9c46c-169">また、メッセージング拡張機能では、認識された URL からのリッチリンクをメッセージに挿入することもできます (この機能は [link unfurling](../../messaging-extensions/how-to/link-unfurling.md)と呼ばれます)。</span><span class="sxs-lookup"><span data-stu-id="9c46c-169">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="9c46c-170">**1. 認識** されたリンクを [新規作成] ボックスに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-170">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="例は、compost ボックスにリンクを貼り付けたユーザーを示しています。" border="false":::

<span data-ttu-id="9c46c-172">**2. コンテンツを挿入** します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-172">**2. Insert content**.</span></span> <span data-ttu-id="9c46c-173">アプリで [新規作成] ボックスの URL を認識している場合は、web コンテンツのコンテンツを豊富にプレビューするカードとしてリンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-173">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="9c46c-174">(詳細については、「 [アダプティブカードのデザインガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="9c46c-174">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="例では、アプリによって認識された後の URL が、[新規作成] ボックスにいくつかのリッチコンテンツを含むことを示しています。" border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="9c46c-176">メッセージング拡張機能を管理する</span><span class="sxs-lookup"><span data-stu-id="9c46c-176">Manage a messaging extension</span></span>

<span data-ttu-id="9c46c-177">アイコンを右クリックすると、ユーザーはメッセージング拡張機能を固定、削除、または構成することができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-177">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="9c46c-178">構造</span><span class="sxs-lookup"><span data-stu-id="9c46c-178">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="9c46c-179">[新規作成] ボックスのメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="9c46c-179">Messaging extension in the compose box</span></span>

<span data-ttu-id="9c46c-180">次の例は、[新規作成] ボックスから開かれたメッセージング拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="9c46c-180">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="[新規作成] ボックスでのメッセージング拡張機能の UI の構造を示す図。" border="false":::

|<span data-ttu-id="9c46c-182">カウンター</span><span class="sxs-lookup"><span data-stu-id="9c46c-182">Counter</span></span>|<span data-ttu-id="9c46c-183">説明</span><span class="sxs-lookup"><span data-stu-id="9c46c-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9c46c-184">1</span><span class="sxs-lookup"><span data-stu-id="9c46c-184">1</span></span>|<span data-ttu-id="9c46c-185">アプリ **ロゴ**: アプリロゴのカラーアイコン。</span><span class="sxs-lookup"><span data-stu-id="9c46c-185">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="9c46c-186">2 </span><span class="sxs-lookup"><span data-stu-id="9c46c-186">2</span></span>|<span data-ttu-id="9c46c-187">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="9c46c-187">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="9c46c-188">3 </span><span class="sxs-lookup"><span data-stu-id="9c46c-188">3</span></span>|<span data-ttu-id="9c46c-189">**アクションコマンドメニューアイコン (オプション)**: メッセージング拡張機能のアクションコマンドの一覧を開きます (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="9c46c-189">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="9c46c-190">4 </span><span class="sxs-lookup"><span data-stu-id="9c46c-190">4</span></span>|<span data-ttu-id="9c46c-191">**検索ボックス**: ユーザーが挿入するアプリコンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-191">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="9c46c-192">5 </span><span class="sxs-lookup"><span data-stu-id="9c46c-192">5</span></span>|<span data-ttu-id="9c46c-193">**タブメニュー (オプション)**: 複数のコンテンツカテゴリを提供します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-193">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="9c46c-194">6 </span><span class="sxs-lookup"><span data-stu-id="9c46c-194">6</span></span>|<span data-ttu-id="9c46c-195">**アクションコマンドメニュー (オプション)**: アクションコマンドの一覧を表示します (任意の数を指定する場合)。</span><span class="sxs-lookup"><span data-stu-id="9c46c-195">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="9c46c-196">7 </span><span class="sxs-lookup"><span data-stu-id="9c46c-196">7</span></span>|<span data-ttu-id="9c46c-197">**アプリコンテンツ**: 主に検索結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-197">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="9c46c-198">この例では、リストレイアウトを使用しています (グリッドレイアウトは別のオプションです)。</span><span class="sxs-lookup"><span data-stu-id="9c46c-198">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="9c46c-199">8 </span><span class="sxs-lookup"><span data-stu-id="9c46c-199">8</span></span>|<span data-ttu-id="9c46c-200">アプリ **ロゴ**: アプリロゴのアウトラインアイコン。</span><span class="sxs-lookup"><span data-stu-id="9c46c-200">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="9c46c-201">メッセージング拡張機能の管理メニュー</span><span class="sxs-lookup"><span data-stu-id="9c46c-201">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能管理メニューの UI の構造を示す図" border="false":::

|<span data-ttu-id="9c46c-203">カウンター</span><span class="sxs-lookup"><span data-stu-id="9c46c-203">Counter</span></span>|<span data-ttu-id="9c46c-204">説明</span><span class="sxs-lookup"><span data-stu-id="9c46c-204">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9c46c-205">1</span><span class="sxs-lookup"><span data-stu-id="9c46c-205">1</span></span>|<span data-ttu-id="9c46c-206">**固定** 解除: ユーザーがアプリを固定している場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-206">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="9c46c-207">2 </span><span class="sxs-lookup"><span data-stu-id="9c46c-207">2</span></span>|<span data-ttu-id="9c46c-208">**Remove**: チャネル、チャット、または会議からメッセージング拡張機能を削除します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-208">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="9c46c-209">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="9c46c-209">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="9c46c-210">セットアップと一般的な使用法</span><span class="sxs-lookup"><span data-stu-id="9c46c-210">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="9c46c-212">Do: シングルサインオンと統合する</span><span class="sxs-lookup"><span data-stu-id="9c46c-212">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="9c46c-213">SSO を使用すると、サインインプロセスが簡単に、より速く、かつ安全になります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-213">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="9c46c-214">また、ユーザーが個人用アプリに既にサインインしている場合は、再度サインインしてメッセージング拡張機能にアクセスする必要もありません。</span><span class="sxs-lookup"><span data-stu-id="9c46c-214">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="9c46c-216">いいえ: ユーザーを会話から離します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-216">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="9c46c-217">メッセージング内線番号は、コンテキスト切り替えが減少すると想定されるショートカットです。</span><span class="sxs-lookup"><span data-stu-id="9c46c-217">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="9c46c-218">たとえば、ユーザーが Teams 以外の web ページにアクセスするということはできません。</span><span class="sxs-lookup"><span data-stu-id="9c46c-218">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="9c46c-219">Do: メッセージング拡張機能を強調表示する</span><span class="sxs-lookup"><span data-stu-id="9c46c-219">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="9c46c-220">メッセージング拡張機能は、必ずしも簡単に見つけることができません。</span><span class="sxs-lookup"><span data-stu-id="9c46c-220">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="9c46c-221">アプリの詳細ページでの使用方法を示したスクリーンショットを含めます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-221">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="9c46c-222">アプリに bot も含まれている場合は、ボットウェルカムツアーにメッセージング拡張機能のヘルプドキュメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-222">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="9c46c-223">テンプレート</span><span class="sxs-lookup"><span data-stu-id="9c46c-223">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="9c46c-225">Do: 可能であれば、チームがいくつかのデザイン作業を処理できるようにします</span><span class="sxs-lookup"><span data-stu-id="9c46c-225">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="9c46c-226">ユースケースにとって意味がある場合は、検索ベースのメッセージング拡張機能を作成することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="9c46c-226">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="9c46c-227">Teams では、これらの種類の拡張子が組み込みのテーマとアクセシビリティを使用してレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-227">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="9c46c-229">[しない]: タスクモジュールにアプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="9c46c-229">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="9c46c-230">メッセージング拡張機能にアクションコマンドが必要な場合は、タスクモジュールをシンプルにし、アクションを実行するために必要なコンポーネントのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-230">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="9c46c-231">テーマ</span><span class="sxs-lookup"><span data-stu-id="9c46c-231">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="9c46c-233">Do: Teams のカラートークンを活用する</span><span class="sxs-lookup"><span data-stu-id="9c46c-233">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="9c46c-234">各 Teams テーマには独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-234">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="9c46c-235">テーマの変更を自動的に処理するには、設計で <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color token (FLUENT UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-235">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="9c46c-237">いいえ: ハードコードの色の値</span><span class="sxs-lookup"><span data-stu-id="9c46c-237">Don't: Hard code color values</span></span>

<span data-ttu-id="9c46c-238">Teams のカラートークンを使用しない場合、設計のスケーラビリティが低下し、管理にかかる時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-238">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="9c46c-239">Actions</span><span class="sxs-lookup"><span data-stu-id="9c46c-239">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="9c46c-241">Do: コンテキストに適したアクションコマンドを含める</span><span class="sxs-lookup"><span data-stu-id="9c46c-241">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="9c46c-242">メッセージアクションは、ユーザーが閲覧しているものと関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-242">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="9c46c-243">たとえば、ユーザーに対して、他のユーザーの投稿のテキストを使用して、懸案事項または作業項目を作成するためのショートカットを提供します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-243">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="9c46c-245">省略: コンテキスト以外のアクションコマンドを含める</span><span class="sxs-lookup"><span data-stu-id="9c46c-245">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="9c46c-246">ダッシュボードを表示するメッセージアクションは、ほとんどの会話から切断され **ている** ように見えます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-246">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="9c46c-247">現われる</span><span class="sxs-lookup"><span data-stu-id="9c46c-247">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="9c46c-248">Do: 入力中に検索結果を表示する</span><span class="sxs-lookup"><span data-stu-id="9c46c-248">Do: Show search results while typing</span></span>

<span data-ttu-id="9c46c-249">ユーザーの入力中に推奨される検索結果を提供します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-249">Provide suggested search results while users type.</span></span> <span data-ttu-id="9c46c-250">必要なコンテンツを最小限の文字で迅速に見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-250">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="9c46c-251">いいえ: クエリの送信をユーザーに要求する</span><span class="sxs-lookup"><span data-stu-id="9c46c-251">Don't: Require users to submit a query</span></span>

<span data-ttu-id="9c46c-252">アプリに対してクエリを送信するためのキーを押すか、ボタンを選択することができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-252">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="9c46c-253">App services サービスの方が簡単な場合もありますが、ユーザーが入力したリアルタイム検索結果が表示されないと混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-253">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="9c46c-254">Do: 0 個のクエリを考慮する</span><span class="sxs-lookup"><span data-stu-id="9c46c-254">Do: Consider zero-term queries</span></span>

<span data-ttu-id="9c46c-255">たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示されたものを表示します。</span><span class="sxs-lookup"><span data-stu-id="9c46c-255">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="9c46c-256">そのようなコンテンツを会話に挿入することができます。</span><span class="sxs-lookup"><span data-stu-id="9c46c-256">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="9c46c-257">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="9c46c-257">Validate your design</span></span>

<span data-ttu-id="9c46c-258">アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c46c-258">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9c46c-259">設計検証ガイドラインの確認</span><span class="sxs-lookup"><span data-stu-id="9c46c-259">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
