---
title: メッセージング拡張機能の設計
description: Teamsメッセージング拡張機能を設計し、Microsoft Teams UI キットを入手する方法について説明します。
keywords: チーム設計ガイドライン 参照メッセージング拡張機能のヒント ベスト プラクティス
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ed1f0f2eb2ce8d429a8a780bd2c4c4eb421d6d54
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566216"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="c3f2a-104">Microsoft Teamsメッセージング拡張機能の設計</span><span class="sxs-lookup"><span data-stu-id="c3f2a-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="c3f2a-105">メッセージング拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作を行ったりするためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="c3f2a-106">アプリの設計をガイドするために、次の情報は、ユーザーがTeamsでメッセージング拡張機能を追加、使用、および管理する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="c3f2a-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="c3f2a-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="c3f2a-108">必要に応じて取得および変更できる要素を含む、包括的なメッセージング拡張機能の設計ガイドラインについては、「Microsoft Teams UI キット」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3f2a-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="c3f2a-110">メッセージング拡張機能を追加する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-110">Add a messaging extension</span></span>

<span data-ttu-id="c3f2a-111">メッセージング拡張機能は、次のTeamsコンテキストで追加できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="c3f2a-112">Teams ストア (AppSource) から。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="c3f2a-113">チャンネル、チャット、または会議 (作成中、および後) で、作成ボックスの近く。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="c3f2a-114">これらの場所のいずれかでメッセージング拡張機能を追加する場合は、そのコンテキストでしか使用できません。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="c3f2a-115">次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-115">The following example shows how you add a messaging extension in a channel:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="c3f2a-117">メッセージング拡張機能の設定</span><span class="sxs-lookup"><span data-stu-id="c3f2a-117">Set up a messaging extension</span></span>

<span data-ttu-id="c3f2a-118">認証は必須ではありませんが、アプリがチケット追跡ツールのようなものの場合は、メッセージング拡張機能を使用するためにサインインするユーザーが必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="c3f2a-119">Teamsアプリ間で一貫性を保つには、サインイン画面をカスタマイズすることはできません。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="c3f2a-120">シングル サインオン (SSO) 認証を使用する場合、ユーザーは自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="例は、サインイン ボタンを使用してメッセージング拡張機能のセットアップ画面を示しています。" border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="c3f2a-122">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="c3f2a-122">Types of messaging extensions</span></span>

<span data-ttu-id="c3f2a-123">メッセージング拡張機能には、検索コマンド、アクション コマンド、またはその両方を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="c3f2a-124">コマンドは、アプリの機能と、ユース ケース内での機能Teams合わせて異なります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="c3f2a-125">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="c3f2a-125">Search commands</span></span>

<span data-ttu-id="c3f2a-126">検索コマンドを使用すると、メッセージング拡張機能を使用して、外部コンテンツをすばやく検索し、メッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="c3f2a-127">検索コマンドは、通常、作成ボックスで使用できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="c3f2a-128">たとえば、コンテンツを共有することでディスカッションを開始したり、ディスカッションに追加したりTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例は、新規作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="c3f2a-130">作成ボックスレイアウトオプション</span><span class="sxs-lookup"><span data-stu-id="c3f2a-130">Compose box layout options</span></span>

<span data-ttu-id="c3f2a-131">[リスト ビューやグリッド ビュー](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)など、メッセージング拡張機能の検索結果を表示するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能の検索結果のレイアウト オプションを示す図。" border="false":::

### <a name="action-commands"></a><span data-ttu-id="c3f2a-133">操作コマンド</span><span class="sxs-lookup"><span data-stu-id="c3f2a-133">Action commands</span></span>

<span data-ttu-id="c3f2a-134">アクションコマンドを使用すると、ユーザーはTeams内の外部サービスでアクションをトリガーし、要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="c3f2a-135">たとえば、アプリが注文を追跡する場合、ユーザーはチャット内から同僚のメッセージの内容を使用して新しい注文を作成できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="c3f2a-136">アクションベースのメッセージング拡張機能では、多くの場合、ユーザーがフォームまたはその他の種類の構成をモーダル内で入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="c3f2a-137">[タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用してこれらのエクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="c3f2a-138">メッセージング拡張機能を開く</span><span class="sxs-lookup"><span data-stu-id="c3f2a-138">Open a messaging extension</span></span>

<span data-ttu-id="c3f2a-139">作成ボックスとメッセージまたは投稿は、ユーザーがメッセージング拡張機能を使用する主要なコンテキストです。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-139">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="c3f2a-140">作成ボックスから</span><span class="sxs-lookup"><span data-stu-id="c3f2a-140">From the compose box</span></span>

<span data-ttu-id="c3f2a-141">追加すると、ユーザーは作成ボックスの下にあるアプリアイコンを選択して、メッセージング拡張機能を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="c3f2a-142">この例では、拡張機能には検索コマンドとアクションコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-142">In this example, the extension has search and action commands:</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="c3f2a-144">チャット メッセージまたはチャネル投稿から</span><span class="sxs-lookup"><span data-stu-id="c3f2a-144">From a chat message or channel post</span></span>

追加すると、ユーザーは :::image type="icon" source="../../assets/icons/teams-client-more.png"::: チャットメッセージまたはチャンネル投稿の[その他]アイコンを選択して、拡張機能のアクションコマンドを見つけることができます。 <span data-ttu-id="c3f2a-146">拡張機能は、使用状況に基づいて **[その他のアクション]** の下に表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-146">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="c3f2a-147">チャット メッセージやチャネル投稿からのその他のアクションのサポートは、モバイル プラットフォームではMicrosoft Teamsできません。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-147">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="c3f2a-148">チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="c3f2a-148">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャット メッセージからメッセージ拡張機能を開く方法を示しています。" border="false":::

#### <a name="channel-post"></a><span data-ttu-id="c3f2a-150">チャンネル投稿</span><span class="sxs-lookup"><span data-stu-id="c3f2a-150">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="例は、チャネル投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="c3f2a-152">メッセージング拡張機能を使用する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-152">Use a messaging extension</span></span>

<span data-ttu-id="c3f2a-153">次のシナリオは、ユーザーがメッセージング拡張機能を使用する主な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-153">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="c3f2a-154">メッセージにコンテンツを挿入する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-154">Insert content into a message</span></span>

<span data-ttu-id="c3f2a-155">**1. メッセージング拡張機能 を選択** します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-155">**1. Select a messaging extension**.</span></span> <span data-ttu-id="c3f2a-156">ユーザーは、作成ボックスから共有するコンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-156">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="例は、作成ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

<span data-ttu-id="c3f2a-158">**2. コンテンツを挿入** します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-158">**2. Insert content**.</span></span> <span data-ttu-id="c3f2a-159">投稿されると、他のユーザーは返信したり、コンテンツを選択して、アプリの詳細情報を表示したりできます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-159">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="例は、ユーザーがチャネル会話にコンテンツを投稿する例です。" border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="c3f2a-161">メッセージに対するアクションの実行</span><span class="sxs-lookup"><span data-stu-id="c3f2a-161">Take action on a message</span></span>

<span data-ttu-id="c3f2a-162">**1. メッセージング拡張機能 を選択** します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-162">**1. Select a messaging extension**.</span></span> <span data-ttu-id="c3f2a-163">アプリには、1 つ以上のアクション コマンドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-163">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="例は、メッセージング拡張機能アクション コマンドを選択するユーザーを示しています。" border="false":::

<span data-ttu-id="c3f2a-165">**2. アクションを完了します**。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-165">**2. Complete the action**.</span></span> <span data-ttu-id="c3f2a-166">アプリは、メッセージ アクションによって送信されたコンテンツやデータを受信して処理できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-166">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="c3f2a-167">これにより、ユーザーは会話を続けることができ、次の例では、アプリに直接情報を入力する心配はありません。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-167">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="メッセージに対するアクションの実行方法の例。" border="false":::

### <a name="preview-links"></a><span data-ttu-id="c3f2a-169">プレビュー リンク</span><span class="sxs-lookup"><span data-stu-id="c3f2a-169">Preview links</span></span>

<span data-ttu-id="c3f2a-170">また、メッセージング拡張機能を使用すると、認識された URL からリッチ リンクをメッセージに挿入することもできます (この機能は [リンク展開](../../messaging-extensions/how-to/link-unfurling.md)と呼ばれます)。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-170">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="c3f2a-171">**1. 認識されたリンクを作成ボックスに貼り付けます** 。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-171">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="例は、ユーザーがコンポスト ボックスにリンクを貼り付けた場合を示しています。" border="false":::

<span data-ttu-id="c3f2a-173">**2. コンテンツを挿入** します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-173">**2. Insert content**.</span></span> <span data-ttu-id="c3f2a-174">アプリが作成ボックス内の URL を認識すると、Web コンテンツのコンテンツリッチ プレビューを提供するカードとしてリンクがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-174">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="c3f2a-175">(詳細については [、アダプティブ カード設計ガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-175">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="URL がアプリで認識されるため、URL に作成ボックスにリッチ コンテンツが含まれる方法を例に示します。" border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="c3f2a-177">メッセージング拡張機能の管理</span><span class="sxs-lookup"><span data-stu-id="c3f2a-177">Manage a messaging extension</span></span>

<span data-ttu-id="c3f2a-178">アイコンを右クリックすると、ユーザーはメッセージング拡張機能をピン留め、削除、または構成できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-178">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="c3f2a-179">構造</span><span class="sxs-lookup"><span data-stu-id="c3f2a-179">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="c3f2a-180">[新規作成] ボックスのメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c3f2a-180">Messaging extension in the compose box</span></span>

<span data-ttu-id="c3f2a-181">次の例は、作成ボックスから開いたメッセージング拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-181">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="作成ボックス内のメッセージング拡張機能の UI の解剖学を示す図。" border="false":::

|<span data-ttu-id="c3f2a-183">カウンター</span><span class="sxs-lookup"><span data-stu-id="c3f2a-183">Counter</span></span>|<span data-ttu-id="c3f2a-184">説明</span><span class="sxs-lookup"><span data-stu-id="c3f2a-184">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c3f2a-185">1</span><span class="sxs-lookup"><span data-stu-id="c3f2a-185">1</span></span>|<span data-ttu-id="c3f2a-186">**アプリロゴ**: アプリロゴのカラーアイコン。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-186">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="c3f2a-187">2</span><span class="sxs-lookup"><span data-stu-id="c3f2a-187">2</span></span>|<span data-ttu-id="c3f2a-188">**アプリ名**: アプリのフルネーム。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-188">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="c3f2a-189">3</span><span class="sxs-lookup"><span data-stu-id="c3f2a-189">3</span></span>|<span data-ttu-id="c3f2a-190">**アクションコマンドメニューアイコン(オプション)**: メッセージング拡張機能のアクションコマンドのリストを開きます(指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-190">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="c3f2a-191">4</span><span class="sxs-lookup"><span data-stu-id="c3f2a-191">4</span></span>|<span data-ttu-id="c3f2a-192">**検索ボックス**: ユーザーは、挿入するアプリのコンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-192">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="c3f2a-193">5</span><span class="sxs-lookup"><span data-stu-id="c3f2a-193">5</span></span>|<span data-ttu-id="c3f2a-194">**タブメニュー (オプション)**: 複数のコンテンツカテゴリを提供します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-194">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="c3f2a-195">6</span><span class="sxs-lookup"><span data-stu-id="c3f2a-195">6</span></span>|<span data-ttu-id="c3f2a-196">**[アクション コマンド] メニュー (オプション):** アクション コマンドの一覧を表示します (指定した場合)。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-196">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="c3f2a-197">7</span><span class="sxs-lookup"><span data-stu-id="c3f2a-197">7</span></span>|<span data-ttu-id="c3f2a-198">**アプリコンテンツ**: 主に検索結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-198">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="c3f2a-199">ここでの例は、リストレイアウトを使用しています(グリッドレイアウトは別のオプションです)。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-199">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="c3f2a-200">8</span><span class="sxs-lookup"><span data-stu-id="c3f2a-200">8</span></span>|<span data-ttu-id="c3f2a-201">**アプリロゴ**: アプリロゴのアウトラインアイコン。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-201">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="c3f2a-202">メッセージング拡張機能管理メニュー</span><span class="sxs-lookup"><span data-stu-id="c3f2a-202">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能管理メニューの UI の構成を示す図。" border="false":::

|<span data-ttu-id="c3f2a-204">カウンター</span><span class="sxs-lookup"><span data-stu-id="c3f2a-204">Counter</span></span>|<span data-ttu-id="c3f2a-205">説明</span><span class="sxs-lookup"><span data-stu-id="c3f2a-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="c3f2a-206">1</span><span class="sxs-lookup"><span data-stu-id="c3f2a-206">1</span></span>|<span data-ttu-id="c3f2a-207">**固定解除**: ユーザーがアプリをピン留めしている場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-207">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="c3f2a-208">2</span><span class="sxs-lookup"><span data-stu-id="c3f2a-208">2</span></span>|<span data-ttu-id="c3f2a-209">**削除**: チャネル、チャット、または会議からメッセージ拡張機能を削除します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-209">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="c3f2a-210">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="c3f2a-210">Best practices</span></span>

<span data-ttu-id="c3f2a-211">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-211">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="c3f2a-212">セットアップと一般的な使用法</span><span class="sxs-lookup"><span data-stu-id="c3f2a-212">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="セットアップと一般的な使用方法の例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="c3f2a-214">行う: シングル サインオンと統合</span><span class="sxs-lookup"><span data-stu-id="c3f2a-214">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="c3f2a-215">SSO により、サインイン プロセスがより簡単、より高速、およびセキュリティで保護されます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-215">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="c3f2a-216">また、ユーザーが個人用アプリに既にサインインしている場合は、メッセージング拡張機能にアクセスするために再度サインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-216">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="シングル サインオンとの統合の例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="c3f2a-218">しない: ユーザーを会話から遠ざける</span><span class="sxs-lookup"><span data-stu-id="c3f2a-218">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="c3f2a-219">メッセージング拡張機能は、コンテキストの切り替えを減らすことが想定されるショートカットです。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-219">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="c3f2a-220">たとえば、拡張機能では、Teamsの外部の Web ページにユーザーを誘導しないでください。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-220">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="c3f2a-221">行う: メッセージング拡張機能を強調表示します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-221">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="c3f2a-222">メッセージング拡張機能は、必ずしも簡単に見つけるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-222">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="c3f2a-223">アプリの詳細ページに、その使用方法のスクリーンショットを含めます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-223">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="c3f2a-224">アプリにボットも含まれている場合は、ボットのウェルカム ツアーにメッセージング拡張機能のヘルプ ドキュメントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-224">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="c3f2a-225">テンプレート</span><span class="sxs-lookup"><span data-stu-id="c3f2a-225">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="テンプレートの例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="c3f2a-227">行う:可能であれば、Teams設計作業の一部を処理してみましょう</span><span class="sxs-lookup"><span data-stu-id="c3f2a-227">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="c3f2a-228">ユース ケースに適している場合は、検索ベースのメッセージング拡張機能を作成することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-228">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="c3f2a-229">Teamsでは、組み込みのテーマとアクセシビリティを備えたこれらのタイプの拡張機能をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-229">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="設計作業の処理例" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="c3f2a-231">しない: タスク モジュールにアプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="c3f2a-231">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="c3f2a-232">メッセージング拡張機能でアクション コマンドが必要な場合は、タスク モジュールをシンプルにし、アクションを完了するために必要なコンポーネントのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-232">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="c3f2a-233">テーマ</span><span class="sxs-lookup"><span data-stu-id="c3f2a-233">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="テーマの例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="c3f2a-235">行う: カラートークンTeams活用する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-235">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="c3f2a-236">各Teamsテーマには独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-236">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="c3f2a-237">テーマの変更を自動的に処理するには、 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">デザインでカラー トークン (Fluent UI) を</a> 使用します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-237">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="カラートークンの例。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="c3f2a-239">しない: ハードコードのカラー値</span><span class="sxs-lookup"><span data-stu-id="c3f2a-239">Don't: Hard code color values</span></span>

<span data-ttu-id="c3f2a-240">Teams色のトークンを使用しない場合、デザインの拡張性が低下し、管理に時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-240">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="c3f2a-241">Actions</span><span class="sxs-lookup"><span data-stu-id="c3f2a-241">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="アクションの例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="c3f2a-243">行う: コンテキストで意味のあるアクション コマンドを含める</span><span class="sxs-lookup"><span data-stu-id="c3f2a-243">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="c3f2a-244">メッセージアクションは、ユーザーが見ているものに関連付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-244">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="c3f2a-245">たとえば、ユーザーの投稿のテキストを使用して問題や作業項目を作成するためのショートカットをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-245">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="アクション コマンドの例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="c3f2a-247">しない: コンテキストに依存しないアクション コマンドを含める</span><span class="sxs-lookup"><span data-stu-id="c3f2a-247">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="c3f2a-248">**ダッシュボードを表示** するメッセージ アクションは、ほとんどの会話から切断されているように見えるでしょう。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-248">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="c3f2a-249">検索</span><span class="sxs-lookup"><span data-stu-id="c3f2a-249">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="c3f2a-250">行う: 入力中に検索結果を表示する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-250">Do: Show search results while typing</span></span>

<span data-ttu-id="c3f2a-251">ユーザーが入力している間に、推奨される検索結果を提供します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-251">Provide suggested search results while users type.</span></span> <span data-ttu-id="c3f2a-252">必要なコンテンツは最小限の文字ですばやく見つかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-252">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="c3f2a-253">しない: ユーザーにクエリの送信を要求する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-253">Don't: Require users to submit a query</span></span>

<span data-ttu-id="c3f2a-254">ユーザーがキーを押したり、ボタンを選択してアプリにクエリを送信したりできます。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-254">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="c3f2a-255">アプリ サービス サービスでは、この操作が簡単に行える場合がありますが、入力時にリアルタイムの検索結果が表示されないという混乱が生じる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-255">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="c3f2a-256">実行: ゼロターム クエリを検討する</span><span class="sxs-lookup"><span data-stu-id="c3f2a-256">Do: Consider zero-term queries</span></span>

<span data-ttu-id="c3f2a-257">たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示された内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-257">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="c3f2a-258">そのコンテンツを会話に挿入したい場合があります。</span><span class="sxs-lookup"><span data-stu-id="c3f2a-258">It's possible that they want to insert that content into their conversation.</span></span>
