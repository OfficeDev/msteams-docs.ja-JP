---
title: メッセージング拡張機能のデザイン
description: Teams のメッセージング拡張機能をデザインして、Microsoft Teams UI Kit を取得する方法をご紹介します。
keywords: Teams デザイン ガイドライン リファレンス メッセージング拡張機能のヒント ベスト プラクティス
author: heath-hamilton
localization_priority: Priority
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: f4d1ba1e6e0b71b37e2b7b2d2a32fb729822ba1c
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037671"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="d5fa5-104">Microsoft Teams メッセージング拡張機能のデザイン</span><span class="sxs-lookup"><span data-stu-id="d5fa5-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="d5fa5-105">メッセージング拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作したりするためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="d5fa5-106">アプリのデザインに役立てるために、次の情報では、Teams でユーザーがどのようにメッセージング拡張機能を追加、使用、管理できるかを説明、図解しています。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d5fa5-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="d5fa5-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d5fa5-108">Microsoft Teams UI Kit には、必要に応じて把握、変更できる要素を含む、より包括的なメッセージング拡張機能のデザインのガイドラインが掲載されています。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5fa5-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="d5fa5-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="d5fa5-110">メッセージング拡張機能の追加</span><span class="sxs-lookup"><span data-stu-id="d5fa5-110">Add a messaging extension</span></span>

<span data-ttu-id="d5fa5-111">メッセージング拡張機能は、次の Teams コンテキストで追加できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="d5fa5-112">Teams ストアから。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-112">From the Teams store.</span></span>
* <span data-ttu-id="d5fa5-113">作成ボックスの近くにあるチャネル、チャット、または会議中 (または前後)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="d5fa5-114">これらの場所のいずれかにメッセージング拡張機能を追加すると、そのコンテキストで使用できるのは自分だけであるという点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="d5fa5-115">次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-116">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-118">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="例は、モバイルのチャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="d5fa5-120">メッセージング拡張機能の設定</span><span class="sxs-lookup"><span data-stu-id="d5fa5-120">Set up a messaging extension</span></span>

<span data-ttu-id="d5fa5-121">認証は必須ではありませんが、アプリがチケット追跡ツールのようなものの場合は、メッセージング拡張機能を使用するためにユーザーにサインインしてもらう必要がある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="d5fa5-122">Teams アプリ間で一貫性を保つために、サインイン画面をカスタマイズすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="d5fa5-123">シングル サインオン (SSO) 認証を使用すると、ユーザーは自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-124">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="サインイン ボタンを含むメッセージング拡張機能の設定画面を示す例です。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-126">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="モバイルでサインイン ボタンを含むメッセージング拡張機能の設定画面を示す例です。" border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="d5fa5-128">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="d5fa5-128">Types of messaging extensions</span></span>

<span data-ttu-id="d5fa5-129">メッセージング拡張機能には、検索コマンド、アクション コマンド、またはその両方を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="d5fa5-130">コマンドは、アプリの機能と、それらが Teams のユース ケースへの適合状況によって異なります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="d5fa5-131">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="d5fa5-131">Search commands</span></span>

<span data-ttu-id="d5fa5-132">検索コマンドを使用すると、ユーザーはメッセージング拡張機能を使用して外部コンテンツをすばやく検索し、メッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="d5fa5-133">検索コマンドは、通常、作成ボックスで使用できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="d5fa5-134">たとえば、Teams から離れることなくコンテンツを共有することで、ディスカッションを開始またはディスカッションに追加できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-135">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例では、作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-137">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="例では、モバイルで作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="d5fa5-139">作成ボックスのレイアウト オプション</span><span class="sxs-lookup"><span data-stu-id="d5fa5-139">Compose box layout options</span></span>

<span data-ttu-id="d5fa5-140">メッセージング拡張機能の検索結果を表示するには、[リスト ビューやグリッド ビュー](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)など、いくつかのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能の検索結果のレイアウト オプションを示す図。" border="false":::

### <a name="action-commands"></a><span data-ttu-id="d5fa5-142">操作コマンド</span><span class="sxs-lookup"><span data-stu-id="d5fa5-142">Action commands</span></span>

<span data-ttu-id="d5fa5-143">アクション コマンドを使用すると、ユーザーは Teams 内の外部サービスでアクションをトリガーし、要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="d5fa5-144">たとえば、アプリが注文を追跡する場合、ユーザーはチャット内から同僚のメッセージの内容を使用して新しい注文を作成できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="d5fa5-145">アクション ベースのメッセージング拡張機能では、多くの場合、ユーザーはフォーム、またはモーダル内でその他の種類の構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="d5fa5-146">[タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用して、これらのエクスペリエンス作成できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="d5fa5-147">メッセージング拡張機能を開く</span><span class="sxs-lookup"><span data-stu-id="d5fa5-147">Open a messaging extension</span></span>

<span data-ttu-id="d5fa5-148">ユーザーがメッセージング拡張機能を使用する主要なコンテキストは、作成ボックスと、メッセージまたは投稿です。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="d5fa5-149">作成ボックスから</span><span class="sxs-lookup"><span data-stu-id="d5fa5-149">From the compose box</span></span>

<span data-ttu-id="d5fa5-150">追加すると、ユーザーは作成ボックスの下にあるアプリ アイコンを選択して、メッセージング拡張機能を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="d5fa5-151">これらの例では、拡張機能に検索コマンドとアクション コマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-152">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-154">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="例は、モバイルで作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="d5fa5-156">チャット メッセージまたはチャネルの投稿から</span><span class="sxs-lookup"><span data-stu-id="d5fa5-156">From a chat message or channel post</span></span>

追加すると、ユーザーはチャット メッセージまたはチャネル投稿の **[その他]** の:::image type="icon" source="../../assets/icons/teams-client-more.png":::アイコンを選択して、拡張機能のアクション コマンドを見つけることができます。 <span data-ttu-id="d5fa5-158">拡張機能は、使用状況に基づいて **その他のアクション** に一覧表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="d5fa5-159">Microsoft Teams モバイル プラットフォームでは、チャット メッセージまたはチャネル投稿からのその他のアクションはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="d5fa5-160">チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-161">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャット メッセージからメッセージング拡張機能を開く方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-163">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="例は、モバイルでチャット投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="d5fa5-165">メッセージング拡張機能の使用</span><span class="sxs-lookup"><span data-stu-id="d5fa5-165">Use a messaging extension</span></span>

<span data-ttu-id="d5fa5-166">次のシナリオでは、ユーザーがメッセージング拡張機能を使用する主な方法を示します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="d5fa5-167">メッセージにコンテンツを挿入する</span><span class="sxs-lookup"><span data-stu-id="d5fa5-167">Insert content into a message</span></span>

<span data-ttu-id="d5fa5-168">**1. メッセージング拡張機能を選択します**。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d5fa5-169">ユーザーは、作成ボックスから共有するコンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="作成ボックスから挿入するコンテンツを検索するユーザーの例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-172">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="たとえば、モバイルで作成ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

---

<span data-ttu-id="d5fa5-174">**2. コンテンツの挿入**。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-174">**2. Insert content**.</span></span> <span data-ttu-id="d5fa5-175">投稿されると、他のユーザーが返信したり、コンテンツを選択してアプリの詳細情報を表示したりできます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-176">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="ユーザーがチャネルの会話にコンテンツを投稿する例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-178">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="ユーザーがモバイルでチャネルの会話にコンテンツを投稿する例を示します。" border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="d5fa5-180">メッセージに対してアクションを取る</span><span class="sxs-lookup"><span data-stu-id="d5fa5-180">Take action on a message</span></span>

<span data-ttu-id="d5fa5-181">**1. メッセージング拡張機能を選択します**。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d5fa5-182">アプリには、1 つ以上のアクション コマンドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-183">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="ユーザーがメッセージング拡張機能のアクション コマンドを選択する例を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-185">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="ユーザーがモバイルでメッセージング拡張機能のアクション コマンドを選択する例を示しています。" border="false":::

---

<span data-ttu-id="d5fa5-187">**2. アクションの完了**。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-187">**2. Complete the action**.</span></span> <span data-ttu-id="d5fa5-188">アプリは、メッセージ アクションによって送信されたコンテンツやデータを受信して処理できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="d5fa5-189">これにより、ユーザーは会話を続け、次の例では、アプリに直接情報を入力するという心配をすることもありません。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-190">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="メッセージに対してアクションを実行する方法の例。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-192">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="モバイルでメッセージに対してアクションを実行する方法の例。" border="false":::

---

### <a name="preview-links"></a><span data-ttu-id="d5fa5-194">リンクのプレビュー</span><span class="sxs-lookup"><span data-stu-id="d5fa5-194">Preview links</span></span>

<span data-ttu-id="d5fa5-195">メッセージング拡張機能を使用すると、認識された URL からメッセージにリッチなリンクを挿入することもできます (この機能は、[リンク展開の解除](../../messaging-extensions/how-to/link-unfurling.md)と呼ばれます)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="d5fa5-196">**1. 認識されたリンク** を作成ボックスに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-197">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="たとえば、ユーザーが作成ボックスにリンクを貼り付ける例を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-199">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="例では、モバイルでユーザーが作成ボックスにリンクを貼り付ける例を示しています。" border="false":::

---

<span data-ttu-id="d5fa5-201">**2. コンテンツの挿入**。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-201">**2. Insert content**.</span></span> <span data-ttu-id="d5fa5-202">アプリが作成ボックス内の URL を認識すると、Web コンテンツのコンテンツリッチなプレビューを提供するカードとしてリンクがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="d5fa5-203">(詳細については[アダプティブ カード デザイン ガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-204">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="例は、URL がアプリに認識されてから作成ボックスにリッチ コンテンツを含める方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-206">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="例は、モバイルで URL がアプリによって認識されるから作成ボックスにリッチ コンテンツを含める方法を示しています。" border="false":::

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="d5fa5-208">メッセージング拡張機能の管理</span><span class="sxs-lookup"><span data-stu-id="d5fa5-208">Manage a messaging extension</span></span>

<span data-ttu-id="d5fa5-209">アイコンを右クリックすると、ユーザーはメッセージング拡張機能をピン留め、削除、または構成できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="d5fa5-210">構造</span><span class="sxs-lookup"><span data-stu-id="d5fa5-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="d5fa5-211">作成ボックスのメッセージの拡張機能</span><span class="sxs-lookup"><span data-stu-id="d5fa5-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="d5fa5-212">次の例は、作成ボックスから開かれたメッセージング拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d5fa5-213">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="作成ボックスのメッセージング拡張機能の UI 構造を示す図。" border="false":::

|<span data-ttu-id="d5fa5-215">カウンター</span><span class="sxs-lookup"><span data-stu-id="d5fa5-215">Counter</span></span>|<span data-ttu-id="d5fa5-216">説明</span><span class="sxs-lookup"><span data-stu-id="d5fa5-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d5fa5-217">1.</span><span class="sxs-lookup"><span data-stu-id="d5fa5-217">1</span></span>|<span data-ttu-id="d5fa5-218">**アプリのロゴ**: アプリのロゴの色アイコン。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="d5fa5-219">2.</span><span class="sxs-lookup"><span data-stu-id="d5fa5-219">2</span></span>|<span data-ttu-id="d5fa5-220">**アプリ名**: アプリのフル ネーム</span><span class="sxs-lookup"><span data-stu-id="d5fa5-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d5fa5-221">3</span><span class="sxs-lookup"><span data-stu-id="d5fa5-221">3</span></span>|<span data-ttu-id="d5fa5-222">**[アクション コマンド] メニュー アイコン (省略可能)**: メッセージング拡張機能のアクション コマンドのリストを開きます (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="d5fa5-223">4</span><span class="sxs-lookup"><span data-stu-id="d5fa5-223">4</span></span>|<span data-ttu-id="d5fa5-224">**検索ボックス**: ユーザーが挿入するアプリ コンテンツを検索できるようにします。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d5fa5-225">5</span><span class="sxs-lookup"><span data-stu-id="d5fa5-225">5</span></span>|<span data-ttu-id="d5fa5-226">**タブ メニュー (省略可能)**: 複数のコンテンツ カテゴリを提供します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="d5fa5-227">6</span><span class="sxs-lookup"><span data-stu-id="d5fa5-227">6</span></span>|<span data-ttu-id="d5fa5-228">**[アクション コマンド] メニュー (省略可能)**: アクション コマンドのリストを表示します (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="d5fa5-229">7</span><span class="sxs-lookup"><span data-stu-id="d5fa5-229">7</span></span>|<span data-ttu-id="d5fa5-230">**アプリ コンテンツ**: 主に検索結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="d5fa5-231">この例では、リスト レイアウトを使用しています (グリッド レイアウトは別のオプションです)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="d5fa5-232">8</span><span class="sxs-lookup"><span data-stu-id="d5fa5-232">8</span></span>|<span data-ttu-id="d5fa5-233">**アプリのロゴ**: アプリのロゴの枠線アイコン。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="d5fa5-234">モバイル</span><span class="sxs-lookup"><span data-stu-id="d5fa5-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="モバイルで作成ボックスのメッセージング拡張機能の UI 構造を示す図。" border="false":::

|<span data-ttu-id="d5fa5-236">カウンター</span><span class="sxs-lookup"><span data-stu-id="d5fa5-236">Counter</span></span>|<span data-ttu-id="d5fa5-237">説明</span><span class="sxs-lookup"><span data-stu-id="d5fa5-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d5fa5-238">1.</span><span class="sxs-lookup"><span data-stu-id="d5fa5-238">1</span></span>|<span data-ttu-id="d5fa5-239">**アプリ名**: アプリのフル ネーム</span><span class="sxs-lookup"><span data-stu-id="d5fa5-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d5fa5-240">2.</span><span class="sxs-lookup"><span data-stu-id="d5fa5-240">2</span></span>|<span data-ttu-id="d5fa5-241">**[アクション コマンド] メニュー アイコン (省略可能)**: メッセージング拡張機能のアクション コマンドのリストを開きます (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="d5fa5-242">3</span><span class="sxs-lookup"><span data-stu-id="d5fa5-242">3</span></span>|<span data-ttu-id="d5fa5-243">**検索ボックス**: ユーザーが挿入するアプリ コンテンツを検索できるようにします。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d5fa5-244">4</span><span class="sxs-lookup"><span data-stu-id="d5fa5-244">4</span></span>|<span data-ttu-id="d5fa5-245">**タブ メニュー (省略可能)**: 複数のコンテンツ カテゴリを提供します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="d5fa5-246">5</span><span class="sxs-lookup"><span data-stu-id="d5fa5-246">5</span></span>|<span data-ttu-id="d5fa5-247">**[アクション コマンド] メニュー (省略可能)**: アクション コマンドのリストを表示します (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="d5fa5-248">6</span><span class="sxs-lookup"><span data-stu-id="d5fa5-248">6</span></span>|<span data-ttu-id="d5fa5-249">**アプリ コンテンツ**: 主に検索結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="d5fa5-250">メッセージング拡張機能の管理メニュー</span><span class="sxs-lookup"><span data-stu-id="d5fa5-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能の管理メニューの UI 構造を示す図。" border="false":::

|<span data-ttu-id="d5fa5-252">カウンター</span><span class="sxs-lookup"><span data-stu-id="d5fa5-252">Counter</span></span>|<span data-ttu-id="d5fa5-253">説明</span><span class="sxs-lookup"><span data-stu-id="d5fa5-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d5fa5-254">1.</span><span class="sxs-lookup"><span data-stu-id="d5fa5-254">1</span></span>|<span data-ttu-id="d5fa5-255">**ピン留めを外す**: ユーザーがアプリをピン留めしている場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="d5fa5-256">2.</span><span class="sxs-lookup"><span data-stu-id="d5fa5-256">2</span></span>|<span data-ttu-id="d5fa5-257">**削除**: チャネル、チャット、または会議からメッセージング拡張機能を削除します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="d5fa5-258">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="d5fa5-258">Best practices</span></span>

<span data-ttu-id="d5fa5-259">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="d5fa5-260">セットアップと一般的な使用方法</span><span class="sxs-lookup"><span data-stu-id="d5fa5-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="セットアップと一般的な使用方法の例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="d5fa5-262">Do: シングル サインオンとの統合</span><span class="sxs-lookup"><span data-stu-id="d5fa5-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="d5fa5-263">SSO を使用すると、サインイン プロセスが簡単、高速になり、セキュリティで保護されます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="d5fa5-264">また、ユーザーが既に個人用アプリにサインインしている場合は、メッセージング拡張機能にアクセスするためにもう一度サインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="シングル サインオンとの統合の例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="d5fa5-266">Don't: ユーザーを会話から除外しないでください</span><span class="sxs-lookup"><span data-stu-id="d5fa5-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="d5fa5-267">メッセージング拡張機能は、コンテキストの切り替えを減らすはずのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="d5fa5-268">拡張機能は、たとえば、Teams の外部の Web ページにユーザーを誘導するものであってはいけません。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="d5fa5-269">Do: メッセージング拡張機能のハイライト</span><span class="sxs-lookup"><span data-stu-id="d5fa5-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="d5fa5-270">メッセージング拡張機能は、必ずしも簡単に見つかるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="d5fa5-271">アプリの詳細ページにその使用方法のスクリーンショットを含めます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="d5fa5-272">アプリにボットも含まれている場合は、ボットウェルカム ツアーにメッセージング拡張機能のヘルプ ドキュメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="d5fa5-273">テンプレート作成</span><span class="sxs-lookup"><span data-stu-id="d5fa5-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="テンプレート作成の例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="d5fa5-275">Do: 可能であれば、Teams が設計作業の一部を処理できるようにします</span><span class="sxs-lookup"><span data-stu-id="d5fa5-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="d5fa5-276">ユース ケースに適している場合は、検索ベースのメッセージング拡張機能を作成することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="d5fa5-277">Teams は、これらの種類の拡張機能を、組み込みのテーマ設定とアクセシビリティでレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="デザイン作業の処理の例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="d5fa5-279">Don't: アプリ全体をタスク モジュールに埋め込まないでください</span><span class="sxs-lookup"><span data-stu-id="d5fa5-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="d5fa5-280">メッセージング拡張機能でアクション コマンドが必要な場合は、タスク モジュールをシンプルにし、アクションを完了するために必要なコンポーネントのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="d5fa5-281">テーマ</span><span class="sxs-lookup"><span data-stu-id="d5fa5-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="テーマの例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="d5fa5-283">実行: Teams のカラー トークンを活用する</span><span class="sxs-lookup"><span data-stu-id="d5fa5-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="d5fa5-284">各 Teams テーマには独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="d5fa5-285">テーマの変更を自動的に処理するには、デザインで<a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">カラー トークン (Fluent UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="カラー トークンの例。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="d5fa5-287">Don't: 色の値をハードコード化しないでください</span><span class="sxs-lookup"><span data-stu-id="d5fa5-287">Don't: Hard code color values</span></span>

<span data-ttu-id="d5fa5-288">Teams のカラー トークンを使用しない場合、デザインのスケーラビリティが低下し、管理に時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="d5fa5-289">アクション</span><span class="sxs-lookup"><span data-stu-id="d5fa5-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="アクションの例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="d5fa5-291">Do: コンテキストで意味のあるアクション コマンドを含めます</span><span class="sxs-lookup"><span data-stu-id="d5fa5-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="d5fa5-292">メッセージ アクションは、ユーザーが見ている内容に関連している必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="d5fa5-293">たとえば、他のユーザーの投稿のテキストを使用して、問題や作業項目を作成するためのショートカットをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="アクション コマンドの例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="d5fa5-295">Don't: コンテキストに依存しないアクション コマンドを含めないでください</span><span class="sxs-lookup"><span data-stu-id="d5fa5-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="d5fa5-296">**ダッシュボードを表示** するメッセージ アクションは、ほとんどの会話から切断されているように見える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="d5fa5-297">検索</span><span class="sxs-lookup"><span data-stu-id="d5fa5-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="d5fa5-298">Do: 入力中に検索結果を表示します</span><span class="sxs-lookup"><span data-stu-id="d5fa5-298">Do: Show search results while typing</span></span>

<span data-ttu-id="d5fa5-299">ユーザーの入力中に、おすすめの検索結果を提供します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="d5fa5-300">最小限の文字数を入力するだけですばやくコンテンツを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="d5fa5-301">Don't: ユーザーにクエリの送信を要求しないでください。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="d5fa5-302">ユーザーがキーを押すか、またはボタンを選択してアプリにクエリを送信するようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="d5fa5-303">App Services サービスの方が簡単な場合もありますが、ユーザーは入力時にリアルタイムの検索結果が表示されないと混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="d5fa5-304">Do: ゼロ用語クエリを検討してください</span><span class="sxs-lookup"><span data-stu-id="d5fa5-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="d5fa5-305">たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示した内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="d5fa5-306">そのコンテンツを会話に挿入したい可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d5fa5-306">It's possible that they want to insert that content into their conversation.</span></span>
