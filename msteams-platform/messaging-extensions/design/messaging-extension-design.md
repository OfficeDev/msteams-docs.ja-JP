---
title: メッセージング拡張機能の設計
description: メッセージング拡張機能を設計し、Teams UI キットを取得するMicrosoft Teams説明します。
keywords: teams の設計ガイドラインは、メッセージング拡張機能のヒントのベスト プラクティスを参照します。
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: fd870d8e10ef74c36f8f6d145d48980f53e9303c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631073"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="e7a28-104">メッセージング拡張機能Microsoft Teams設計する</span><span class="sxs-lookup"><span data-stu-id="e7a28-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="e7a28-105">メッセージング拡張機能は、アプリコンテンツを挿入したり、会話から離れることなくメッセージに作用するためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="e7a28-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="e7a28-106">アプリの設計をガイドするために、次の情報は、ユーザーがメッセージング拡張機能を追加、使用、および管理する方法を説明し、Teams。</span><span class="sxs-lookup"><span data-stu-id="e7a28-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="e7a28-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="e7a28-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="e7a28-108">必要に応じて取得および変更できる要素を含む、包括的なメッセージング拡張機能の設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。</span><span class="sxs-lookup"><span data-stu-id="e7a28-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7a28-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="e7a28-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="e7a28-110">メッセージング拡張機能の追加</span><span class="sxs-lookup"><span data-stu-id="e7a28-110">Add a messaging extension</span></span>

<span data-ttu-id="e7a28-111">メッセージング拡張機能は、次のコンテキストでTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="e7a28-112">ストアからTeamsします。</span><span class="sxs-lookup"><span data-stu-id="e7a28-112">From the Teams store.</span></span>
* <span data-ttu-id="e7a28-113">作成ボックスの近くのチャネル、チャット、または会議 (前、中、および後)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="e7a28-114">これらの場所の 1 つでメッセージング拡張機能を追加する場合は、そのコンテキストでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="e7a28-115">次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="e7a28-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-116">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-118">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="例は、モバイル上のチャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="e7a28-120">メッセージング拡張機能を設定する</span><span class="sxs-lookup"><span data-stu-id="e7a28-120">Set up a messaging extension</span></span>

<span data-ttu-id="e7a28-121">認証は必須ではありませんが、アプリがチケット追跡ツールのようなものである場合は、メッセージング拡張機能を使用するためにサインインするユーザーが必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="e7a28-122">アプリ間で一Teams一貫性を保つには、サインイン画面をカスタマイズできない。</span><span class="sxs-lookup"><span data-stu-id="e7a28-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="e7a28-123">シングル サインオン (SSO) 認証を使用する場合、ユーザーは自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="e7a28-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-124">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="例では、サインイン ボタンを使用してメッセージング拡張機能のセットアップ画面を表示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-126">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="例では、モバイルのサインイン ボタンを使用してメッセージング拡張機能のセットアップ画面を表示します。" border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="e7a28-128">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="e7a28-128">Types of messaging extensions</span></span>

<span data-ttu-id="e7a28-129">メッセージング拡張機能には、検索コマンド、アクション コマンド、または両方を指定できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="e7a28-130">コマンドは、アプリの機能と、それらの機能がアプリケーションの使用Teamsに依存します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="e7a28-131">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="e7a28-131">Search commands</span></span>

<span data-ttu-id="e7a28-132">検索コマンドを使用すると、ユーザーはメッセージング拡張機能を使用して外部コンテンツをすばやく検索し、メッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="e7a28-133">検索コマンドは、通常、作成ボックスで使用できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="e7a28-134">たとえば、コンテンツを共有することで、ディスカッションを開始または追加Teams。</span><span class="sxs-lookup"><span data-stu-id="e7a28-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-135">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例は、作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-137">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="例は、モバイルの作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="e7a28-139">作成ボックスのレイアウト オプション</span><span class="sxs-lookup"><span data-stu-id="e7a28-139">Compose box layout options</span></span>

<span data-ttu-id="e7a28-140">リストビューやグリッド ビューなど、メッセージング拡張機能の検索結果を表示 [するためのいくつかのオプションがあります](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能の検索結果のレイアウト オプションを示す図。" border="false":::

### <a name="action-commands"></a><span data-ttu-id="e7a28-142">操作コマンド</span><span class="sxs-lookup"><span data-stu-id="e7a28-142">Action commands</span></span>

<span data-ttu-id="e7a28-143">アクション コマンドを使用すると、ユーザーは外部サービス内のアクションをトリガーし、要求を処理Teams。</span><span class="sxs-lookup"><span data-stu-id="e7a28-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="e7a28-144">たとえば、アプリで注文を追跡する場合、ユーザーはチャット内から同僚のメッセージの内容を使用して新しい注文を作成できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="e7a28-145">アクション ベースのメッセージング拡張機能では、多くの場合、モーダル内でフォームまたは他の種類の構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="e7a28-146">これらのエクスペリエンスは、タスク モジュールで [作成できます](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="e7a28-147">メッセージング拡張機能を開く</span><span class="sxs-lookup"><span data-stu-id="e7a28-147">Open a messaging extension</span></span>

<span data-ttu-id="e7a28-148">作成ボックスとメッセージまたは投稿は、ユーザーがメッセージング拡張機能を使用する主要なコンテキストです。</span><span class="sxs-lookup"><span data-stu-id="e7a28-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="e7a28-149">作成ボックスから</span><span class="sxs-lookup"><span data-stu-id="e7a28-149">From the compose box</span></span>

<span data-ttu-id="e7a28-150">追加すると、ユーザーは作成ボックスの下にあるアプリ アイコンを選択して、メッセージング拡張機能を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="e7a28-151">これらの例では、拡張機能には検索コマンドとアクション コマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-152">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-154">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="例は、モバイルの作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="e7a28-156">チャット メッセージまたはチャネル投稿から</span><span class="sxs-lookup"><span data-stu-id="e7a28-156">From a chat message or channel post</span></span>

追加すると、ユーザーはチャット メッセージまたはチャネル投稿の [その他] アイコンを選択して、拡張機能の :::image type="icon" source="../../assets/icons/teams-client-more.png"::: アクション コマンドを見つけることができます。 <span data-ttu-id="e7a28-158">拡張機能が [使用状況に基づくその他 **のアクション] の下** に表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a28-159">チャット メッセージまたはチャネル投稿からのその他のアクションのサポートは、モバイル プラットフォームMicrosoft Teamsできません。</span><span class="sxs-lookup"><span data-stu-id="e7a28-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="e7a28-160">チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="e7a28-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-161">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャット メッセージからメッセージング拡張機能を開く方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-163">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="例は、モバイル上のチャット投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="e7a28-165">メッセージング拡張機能を使用する</span><span class="sxs-lookup"><span data-stu-id="e7a28-165">Use a messaging extension</span></span>

<span data-ttu-id="e7a28-166">次のシナリオは、ユーザーがメッセージング拡張機能を使用する主な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="e7a28-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="e7a28-167">メッセージにコンテンツを挿入する</span><span class="sxs-lookup"><span data-stu-id="e7a28-167">Insert content into a message</span></span>

<span data-ttu-id="e7a28-168">**1. メッセージング拡張機能を選択します**。</span><span class="sxs-lookup"><span data-stu-id="e7a28-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="e7a28-169">ユーザーは、作成ボックスから共有するコンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="例は、作成ボックスから挿入するコンテンツを検索しているユーザーを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-172">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="例は、モバイルの作成ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

---

<span data-ttu-id="e7a28-174">**2. コンテンツを挿入します**。</span><span class="sxs-lookup"><span data-stu-id="e7a28-174">**2. Insert content**.</span></span> <span data-ttu-id="e7a28-175">投稿後、他のユーザーはコンテンツに返信または選択して、アプリの詳細を表示できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-176">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="例は、チャネル会話にコンテンツを投稿するユーザーを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-178">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="例は、モバイルでのチャネル会話にコンテンツを投稿するユーザーを示しています。" border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="e7a28-180">メッセージに対してアクションを実行する</span><span class="sxs-lookup"><span data-stu-id="e7a28-180">Take action on a message</span></span>

<span data-ttu-id="e7a28-181">**1. メッセージング拡張機能を選択します**。</span><span class="sxs-lookup"><span data-stu-id="e7a28-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="e7a28-182">アプリには、1 つ以上のアクション コマンドを含めできます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-183">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="例は、メッセージング拡張機能アクション コマンドを選択しているユーザーを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-185">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="例は、モバイルでメッセージング拡張機能アクション コマンドを選択しているユーザーを示しています。" border="false":::

---

<span data-ttu-id="e7a28-187">**2. アクションを完了します**。</span><span class="sxs-lookup"><span data-stu-id="e7a28-187">**2. Complete the action**.</span></span> <span data-ttu-id="e7a28-188">アプリは、メッセージ アクションによって送信されたコンテンツまたはデータを受信および処理できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="e7a28-189">これにより、ユーザーは会話を続け、次の例では、アプリに直接情報を入力する心配はありません。</span><span class="sxs-lookup"><span data-stu-id="e7a28-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-190">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="メッセージに対してアクションを実行する方法の例。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-192">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="モバイルでメッセージに対してアクションを実行する方法の例。" border="false":::

---

### <a name="preview-links"></a><span data-ttu-id="e7a28-194">リンクのプレビュー</span><span class="sxs-lookup"><span data-stu-id="e7a28-194">Preview links</span></span>

<span data-ttu-id="e7a28-195">メッセージング拡張機能を使用すると、認識された URL からメッセージにリッチ リンクを挿入することもできます (この機能はリンク解除と [呼ばれる](../../messaging-extensions/how-to/link-unfurling.md).)</span><span class="sxs-lookup"><span data-stu-id="e7a28-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="e7a28-196">**1. 作成ボックスに認識されたリンク** を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-197">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="例では、ユーザーがコンポスト ボックスにリンクを貼り付けする例を示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-199">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="例は、モバイルのコンポスト ボックスにリンクを貼り付けするユーザーを示しています。" border="false":::

---

<span data-ttu-id="e7a28-201">**2. コンテンツを挿入します**。</span><span class="sxs-lookup"><span data-stu-id="e7a28-201">**2. Insert content**.</span></span> <span data-ttu-id="e7a28-202">アプリが作成ボックス内の URL を認識すると、リンクは、Web コンテンツのコンテンツリッチ プレビューを提供するカードとしてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="e7a28-203">(詳細 [については、「アダプティブ カードの設計ガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-204">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="例は、URL がアプリによって認識されるので、作成ボックスにリッチ コンテンツを含む方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e7a28-206">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="例は、URL がアプリによって認識されるので、モバイルの作成ボックスにリッチ コンテンツを含む方法を示しています。" border="false":::

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="e7a28-208">メッセージング拡張機能の管理</span><span class="sxs-lookup"><span data-stu-id="e7a28-208">Manage a messaging extension</span></span>

<span data-ttu-id="e7a28-209">アイコンを右クリックすると、ユーザーはメッセージング拡張機能をピン留め、削除、または構成できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="e7a28-210">構造</span><span class="sxs-lookup"><span data-stu-id="e7a28-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="e7a28-211">作成ボックスのメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="e7a28-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="e7a28-212">次の例は、作成ボックスから開いたメッセージング拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="e7a28-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e7a28-213">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e7a28-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="作成ボックスのメッセージング拡張機能の UI 構造を示す図。" border="false":::

|<span data-ttu-id="e7a28-215">カウンター</span><span class="sxs-lookup"><span data-stu-id="e7a28-215">Counter</span></span>|<span data-ttu-id="e7a28-216">説明</span><span class="sxs-lookup"><span data-stu-id="e7a28-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="e7a28-217">1</span><span class="sxs-lookup"><span data-stu-id="e7a28-217">1</span></span>|<span data-ttu-id="e7a28-218">**アプリのロゴ**: アプリのロゴの色のアイコン。</span><span class="sxs-lookup"><span data-stu-id="e7a28-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="e7a28-219">2</span><span class="sxs-lookup"><span data-stu-id="e7a28-219">2</span></span>|<span data-ttu-id="e7a28-220">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="e7a28-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="e7a28-221">3</span><span class="sxs-lookup"><span data-stu-id="e7a28-221">3</span></span>|<span data-ttu-id="e7a28-222">**[アクション コマンド] メニュー アイコン (オプション)**: メッセージング拡張機能のアクション コマンドの一覧を開きます (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="e7a28-223">4</span><span class="sxs-lookup"><span data-stu-id="e7a28-223">4</span></span>|<span data-ttu-id="e7a28-224">**[検索]** ボックス : ユーザーが挿入するアプリ コンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="e7a28-225">5</span><span class="sxs-lookup"><span data-stu-id="e7a28-225">5</span></span>|<span data-ttu-id="e7a28-226">**タブ メニュー (オプション)**: 複数のコンテンツ カテゴリを提供します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="e7a28-227">6</span><span class="sxs-lookup"><span data-stu-id="e7a28-227">6</span></span>|<span data-ttu-id="e7a28-228">**[アクション コマンド] メニュー (オプション)**: アクション コマンドの一覧を表示します (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="e7a28-229">7</span><span class="sxs-lookup"><span data-stu-id="e7a28-229">7</span></span>|<span data-ttu-id="e7a28-230">**アプリのコンテンツ**: 主に検索結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="e7a28-231">この例では、リスト レイアウトを使用しています (グリッド レイアウトは別のオプションです)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="e7a28-232">8</span><span class="sxs-lookup"><span data-stu-id="e7a28-232">8</span></span>|<span data-ttu-id="e7a28-233">**アプリのロゴ**: アプリロゴのアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="e7a28-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="e7a28-234">モバイル</span><span class="sxs-lookup"><span data-stu-id="e7a28-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="モバイルの作成ボックスにメッセージング拡張機能の UI 構造を示す図。" border="false":::

|<span data-ttu-id="e7a28-236">カウンター</span><span class="sxs-lookup"><span data-stu-id="e7a28-236">Counter</span></span>|<span data-ttu-id="e7a28-237">説明</span><span class="sxs-lookup"><span data-stu-id="e7a28-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="e7a28-238">1</span><span class="sxs-lookup"><span data-stu-id="e7a28-238">1</span></span>|<span data-ttu-id="e7a28-239">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="e7a28-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="e7a28-240">2</span><span class="sxs-lookup"><span data-stu-id="e7a28-240">2</span></span>|<span data-ttu-id="e7a28-241">**[アクション コマンド] メニュー アイコン (オプション)**: メッセージング拡張機能のアクション コマンドの一覧を開きます (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="e7a28-242">3</span><span class="sxs-lookup"><span data-stu-id="e7a28-242">3</span></span>|<span data-ttu-id="e7a28-243">**[検索]** ボックス : ユーザーが挿入するアプリ コンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="e7a28-244">4</span><span class="sxs-lookup"><span data-stu-id="e7a28-244">4</span></span>|<span data-ttu-id="e7a28-245">**タブ メニュー (オプション)**: 複数のコンテンツ カテゴリを提供します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="e7a28-246">5</span><span class="sxs-lookup"><span data-stu-id="e7a28-246">5</span></span>|<span data-ttu-id="e7a28-247">**[アクション コマンド] メニュー (オプション)**: アクション コマンドの一覧を表示します (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="e7a28-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="e7a28-248">6</span><span class="sxs-lookup"><span data-stu-id="e7a28-248">6</span></span>|<span data-ttu-id="e7a28-249">**アプリのコンテンツ**: 主に検索結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="e7a28-250">メッセージング拡張機能の管理メニュー</span><span class="sxs-lookup"><span data-stu-id="e7a28-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能管理メニューの UI 構造を示す図。" border="false":::

|<span data-ttu-id="e7a28-252">カウンター</span><span class="sxs-lookup"><span data-stu-id="e7a28-252">Counter</span></span>|<span data-ttu-id="e7a28-253">説明</span><span class="sxs-lookup"><span data-stu-id="e7a28-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="e7a28-254">1</span><span class="sxs-lookup"><span data-stu-id="e7a28-254">1</span></span>|<span data-ttu-id="e7a28-255">**[ピン留め** 解除] : ユーザーがアプリをピン留めしている場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="e7a28-256">2</span><span class="sxs-lookup"><span data-stu-id="e7a28-256">2</span></span>|<span data-ttu-id="e7a28-257">**削除**: チャネル、チャット、または会議からメッセージング拡張機能を削除します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="e7a28-258">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="e7a28-258">Best practices</span></span>

<span data-ttu-id="e7a28-259">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="e7a28-260">セットアップと一般的な使用方法</span><span class="sxs-lookup"><span data-stu-id="e7a28-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="セットアップと一般的な使用方法の例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="e7a28-262">Do: シングル サインオンとの統合</span><span class="sxs-lookup"><span data-stu-id="e7a28-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="e7a28-263">SSO を使用すると、サインイン プロセスが簡単、高速、およびセキュリティで保護されます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="e7a28-264">また、ユーザーが個人用アプリに既にサインインしている場合は、メッセージング拡張機能にアクセスするためにもう一度サインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e7a28-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="シングル サインオンとの統合の例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="e7a28-266">[しない]: ユーザーを会話から離す</span><span class="sxs-lookup"><span data-stu-id="e7a28-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="e7a28-267">メッセージング拡張機能は、コンテキストの切り替えを減らすことが想定されるショートカットです。</span><span class="sxs-lookup"><span data-stu-id="e7a28-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="e7a28-268">拡張機能は、たとえば、ユーザーを外部の Web ページにTeams。</span><span class="sxs-lookup"><span data-stu-id="e7a28-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="e7a28-269">Do: メッセージング拡張機能を強調表示する</span><span class="sxs-lookup"><span data-stu-id="e7a28-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="e7a28-270">メッセージング拡張機能は、必ずしも簡単に見つけることができるとは限らない。</span><span class="sxs-lookup"><span data-stu-id="e7a28-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="e7a28-271">アプリの詳細ページに、その使い方のスクリーンショットを含める。</span><span class="sxs-lookup"><span data-stu-id="e7a28-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="e7a28-272">アプリにボットも含まれる場合は、ボットウェルカム ツアーにメッセージング拡張機能のヘルプ ドキュメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="e7a28-273">テンプレート</span><span class="sxs-lookup"><span data-stu-id="e7a28-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="テンプレートの例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="e7a28-275">Do: 可能Teams一部の設計作業を処理する</span><span class="sxs-lookup"><span data-stu-id="e7a28-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="e7a28-276">使用例に合う場合は、検索ベースのメッセージング拡張機能の作成を検討してください。</span><span class="sxs-lookup"><span data-stu-id="e7a28-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="e7a28-277">Teams、これらの種類の拡張機能を、組み込みのユーザー設定とアクセシビリティでレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="e7a28-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="設計作業の処理例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="e7a28-279">[しない] タスク モジュールにアプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="e7a28-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="e7a28-280">メッセージング拡張機能でアクション コマンドが必要な場合は、タスク モジュールをシンプルにし、アクションを完了するために必要なコンポーネントのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="e7a28-281">テーマ</span><span class="sxs-lookup"><span data-stu-id="e7a28-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="例: それらを使用します。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="e7a28-283">Do: 色トークンのTeams活用する</span><span class="sxs-lookup"><span data-stu-id="e7a28-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="e7a28-284">各Teamsテーマには、独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="e7a28-285">テーマの変更を自動的に処理するには、デザインでカラー <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">トークン (Fluent UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="カラー トークンの例。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="e7a28-287">[しない] : ハード コードの色の値</span><span class="sxs-lookup"><span data-stu-id="e7a28-287">Don't: Hard code color values</span></span>

<span data-ttu-id="e7a28-288">色トークンを使用しないTeamsデザインの拡張性が低く、管理に時間がかかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="e7a28-289">Actions</span><span class="sxs-lookup"><span data-stu-id="e7a28-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="アクションの例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="e7a28-291">Do: コンテキストで意味のあるアクション コマンドを含める</span><span class="sxs-lookup"><span data-stu-id="e7a28-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="e7a28-292">メッセージアクションは、ユーザーが見ているものに関連する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="e7a28-293">たとえば、ユーザーの投稿のテキストを使用して、問題や作業項目を作成するためのショートカットをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="アクション コマンドの例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="e7a28-295">[しない]: コンテキストに依存しないアクション コマンドを含める</span><span class="sxs-lookup"><span data-stu-id="e7a28-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="e7a28-296">[ダッシュボードを表示する] というメッセージ **アクションは** 、ほとんどの会話から切断されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="e7a28-297">検索</span><span class="sxs-lookup"><span data-stu-id="e7a28-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="e7a28-298">Do: 入力中に検索結果を表示する</span><span class="sxs-lookup"><span data-stu-id="e7a28-298">Do: Show search results while typing</span></span>

<span data-ttu-id="e7a28-299">ユーザーが入力している間に、検索結果の候補を提供します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="e7a28-300">最小限の文字数で、必要なコンテンツをより速く見つける場合があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="e7a28-301">[しない]: ユーザーにクエリの送信を要求する</span><span class="sxs-lookup"><span data-stu-id="e7a28-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="e7a28-302">ユーザーにキーを押させるか、ボタンを選択してアプリにクエリを送信できます。</span><span class="sxs-lookup"><span data-stu-id="e7a28-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="e7a28-303">アプリ サービス サービスの方が簡単ですが、ユーザーは、入力時にリアルタイムの検索結果が表示されないと混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="e7a28-304">Do: ゼロ用語クエリを検討する</span><span class="sxs-lookup"><span data-stu-id="e7a28-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="e7a28-305">たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示した情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="e7a28-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="e7a28-306">会話にコンテンツを挿入する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e7a28-306">It's possible that they want to insert that content into their conversation.</span></span>
