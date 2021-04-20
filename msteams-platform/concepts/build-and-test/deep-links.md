---
title: コンテンツへのディープ リンクを作成する
description: ディープ リンクとアプリでの使用方法について説明する
ms.topic: how-to
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: afcb079873f97055c4af43323d12846294861f74
ms.sourcegitcommit: ee8c4800da3b3569d80c6f3661a2f20aa1f2c5e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2021
ms.locfileid: "51885060"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a><span data-ttu-id="b7b27-104">Microsoft Teams のコンテンツと機能へのディープ リンクを作成する</span><span class="sxs-lookup"><span data-stu-id="b7b27-104">Create deep links to content and features in Microsoft Teams</span></span>

<span data-ttu-id="b7b27-105">Teams 内で情報と機能へのリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-105">You can create links to information and features within Teams.</span></span> <span data-ttu-id="b7b27-106">ディープ リンクの作成が役立つ例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-106">Examples where creating deep links are useful are as follows:</span></span>

* <span data-ttu-id="b7b27-107">アプリのいずれかのタブ内のコンテンツにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-107">Navigating the user to content within one of your app's tabs.</span></span> <span data-ttu-id="b7b27-108">たとえば、アプリには、重要なアクティビティをユーザーに通知するメッセージを送信するボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-108">For instance, your app can have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="b7b27-109">ユーザーが通知をタップすると、ディープ リンクがタブに移動し、ユーザーがアクティビティの詳細を表示できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-109">When the user taps on the notification, the deep link navigates to the tab so the user can view more details about the activity.</span></span>
* <span data-ttu-id="b7b27-110">アプリは、必要なパラメーターを使用してディープ リンクを事前に入力して、チャットの作成や会議のスケジュール設定などの特定のユーザー タスクを自動化または単純化します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre-populating the deep links with required parameters.</span></span> <span data-ttu-id="b7b27-111">これにより、ユーザーが手動で情報を入力する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="b7b27-111">This avoids the need for users to manually enter information.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b7b27-112">ディープリンクは、次のようにコンテンツと情報に移動する前にブラウザーを最初に起動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-112">A deeplink launches the browser first before navigating to content and information as follows:</span></span>
>
> <span data-ttu-id="b7b27-113">**タブ**:</span><span class="sxs-lookup"><span data-stu-id="b7b27-113">**Tab**:</span></span>  
> <span data-ttu-id="b7b27-114">✔ ディープリンクの URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-114">✔ Directly navigates to the deeplink url.</span></span>
>
> <span data-ttu-id="b7b27-115">**ボット**:</span><span class="sxs-lookup"><span data-stu-id="b7b27-115">**Bot**:</span></span>  
> <span data-ttu-id="b7b27-116">✔本文の Deeplink: ブラウザーで最初に開きます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-116">✔ Deeplink in card body: Opens in browser first.</span></span>  
> <span data-ttu-id="b7b27-117">✔カードの OpenURL アクションに Deeplink を追加: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-117">✔ Deeplink added to OpenURL action in Adaptive Card: Directly navigates to the deeplink url.</span></span>  
> <span data-ttu-id="b7b27-118">✔の [ハイパーリンク] マークダウン テキスト: ブラウザーで最初に開きます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-118">✔ Hyperlink markdown text in the card: Opens in browser first.</span></span>  
>
> <span data-ttu-id="b7b27-119">**チャット**</span><span class="sxs-lookup"><span data-stu-id="b7b27-119">**Chat**:</span></span>  
> <span data-ttu-id="b7b27-120">✔ メッセージのハイパーリンク マークダウン: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-120">✔ Text message hyperlink markdown: Directly navigates to deeplink url.</span></span>  
> <span data-ttu-id="b7b27-121">✔チャット会話で貼り付けリンク: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-121">✔ Link pasted in general chat conversation: Directly navigates to deeplink url.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="b7b27-122">タブへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="b7b27-122">Deep linking to your tab</span></span>

<span data-ttu-id="b7b27-123">Teams のエンティティへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="b7b27-124">通常、これは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リスト チーム メンバーが含まれている場合は、個々のタスクへのリンクを作成して共有できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-124">Typically, this is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list team members can create and share links to individual tasks.</span></span> <span data-ttu-id="b7b27-125">リンクを選択すると、特定のアイテムに焦点を当てたタブに移動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-125">When you select the link, it  navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="b7b27-126">これを実装するには、各アイテムに「リンクのコピー」アクションを UI に最適な方法で追加します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-126">To implement this, you add a "copy link" action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="b7b27-127">このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-127">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="b7b27-128">この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-128">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="b7b27-129">または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-129">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="b7b27-130">これらをボットおよびコネクタ[](~/bots/what-are-bots.md)メッセージで[使用して、](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)タブまたはタブ内のアイテムに対する変更をユーザーに通知できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-130">You can use these in [bot](~/bots/what-are-bots.md) and [connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="b7b27-131">このディープ リンクは、[タブ へのコピー]リンクによって提供されるリンクとは異なります。これは、このタブをポイントするディープ リンクを生成するだけです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-131">This deep link is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

>[!NOTE]
> <span data-ttu-id="b7b27-132">現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="b7b27-132">Currently, shareDeepLink does not work on mobile platforms.</span></span>

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="b7b27-133">タブ内のアイテムへのディープ リンクを表示する</span><span class="sxs-lookup"><span data-stu-id="b7b27-133">Showing a deep link to an item within your tab</span></span>

<span data-ttu-id="b7b27-134">タブ内のアイテムへのディープ リンクを含むダイアログ ボックスを表示するには、`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` を呼び出します</span><span class="sxs-lookup"><span data-stu-id="b7b27-134">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span></span>

<span data-ttu-id="b7b27-135">次のフィールドを指定します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-135">Provide these fields:</span></span>

* <span data-ttu-id="b7b27-136">`subEntityId`&emsp;タブ内でディープ リンクを設定しているアイテムの一意の識別子</span><span class="sxs-lookup"><span data-stu-id="b7b27-136">`subEntityId`&emsp;A unique identifier for the item within your tab to which you are deep linking</span></span>
* <span data-ttu-id="b7b27-137">`subEntityLabel`&emsp;ディープ リンクを表示するために使用するアイテムのラベル</span><span class="sxs-lookup"><span data-stu-id="b7b27-137">`subEntityLabel`&emsp;A label for the item to use for displaying the deep link</span></span>
* <span data-ttu-id="b7b27-138">`subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用する代替 URL を含むオプションのフィールド</span><span class="sxs-lookup"><span data-stu-id="b7b27-138">`subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab</span></span>

### <a name="generating-a-deep-link-to-your-tab"></a><span data-ttu-id="b7b27-139">タブへのディープ リンクを作成する</span><span class="sxs-lookup"><span data-stu-id="b7b27-139">Generating a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="b7b27-140">個人用タブにはスコープ `personal` が含まれていますが、チャネルタブとグループ タブはスコープ `team` を `group` 使用します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-140">Personal tabs have a `personal` scope, while channel and group tabs use `team` or `group` scopes.</span></span> <span data-ttu-id="b7b27-141">構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。</span><span class="sxs-lookup"><span data-stu-id="b7b27-141">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="b7b27-142">タブ スコープ [の詳細](~/resources/schema/manifest-schema.md) については、マニフェスト リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b7b27-142">See the [manifest](~/resources/schema/manifest-schema.md) reference for more information on tab scopes.</span></span>

> [!NOTE]
> <span data-ttu-id="b7b27-143">ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-143">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="b7b27-144">エンティティ ID のないタブへのディープ リンクは、タブに移動しますが、サブエンティティ ID をタブに提供できない場合があります。</span><span class="sxs-lookup"><span data-stu-id="b7b27-144">Deep links to tabs without entity IDs still navigate to the tab but can not provide the sub-entity ID to the tab.</span></span>

<span data-ttu-id="b7b27-145">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-145">Use the following format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> <span data-ttu-id="b7b27-146">ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-146">If the bot sends a message containing a `TextBlock` with a deep link, then a new browser tab is opened when the user selects the link.</span></span> <span data-ttu-id="b7b27-147">これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-147">This happens in Chrome and in the Microsoft Teams desktop app, both running on Linux.</span></span>
> <span data-ttu-id="b7b27-148">ボットが同じディープ リンク URL を A に送信すると、ユーザーがリンクを選択すると、現在のブラウザー タブで `Action.OpenUrl` [Teams] タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-148">If the bot sends the same deep link URL into an `Action.OpenUrl`, then the Teams tab is opened in the current browser tab when the user selects the link.</span></span> <span data-ttu-id="b7b27-149">新しいブラウザー タブは開きません。</span><span class="sxs-lookup"><span data-stu-id="b7b27-149">No new browser tab is opened.</span></span>

<span data-ttu-id="b7b27-150">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-150">The query parameters are:</span></span>

* <span data-ttu-id="b7b27-151">`appId`&emsp;マニフェストの ID。たとえば、「fe4a8eba-2a31-4737-8e33-e5fae6fee194」のようになります</span><span class="sxs-lookup"><span data-stu-id="b7b27-151">`appId`&emsp;The ID from your manifest; for example, "fe4a8eba-2a31-4737-8e33-e5fae6fee194"</span></span>
* <span data-ttu-id="b7b27-152">`entityId`&emsp;タブのアイテムの ID。[タブを構成する](~/tabs/how-to/create-tab-pages/configuration-page.md)ときに表示されます。たとえば、「tasklist123」のようになります</span><span class="sxs-lookup"><span data-stu-id="b7b27-152">`entityId`&emsp;The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md); for example, "tasklist123"</span></span>
* <span data-ttu-id="b7b27-153">`entityWebUrl` または `subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用する代替 URL を含むオプションのフィールド。たとえば、「https://tasklist.example.com/123」または「https://tasklist.example.com/list123/task456」のようになります</span><span class="sxs-lookup"><span data-stu-id="b7b27-153">`entityWebUrl` or `subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab; for example, "https://tasklist.example.com/123" or "https://tasklist.example.com/list123/task456"</span></span>
* <span data-ttu-id="b7b27-154">`entityLabel` または `subEntityLabel`&emsp;ディープ リンクを表示するときに使用するタブのアイテムのラベル。たとえば、「Task List 123」または「Task 456」のようになります</span><span class="sxs-lookup"><span data-stu-id="b7b27-154">`entityLabel` or `subEntityLabel`&emsp;A label for the item in your tab, to use when displaying the deep link; for example, "Task List 123" or "Task 456"</span></span>
* <span data-ttu-id="b7b27-155">`context`&emsp;次のフィールドを含む JSON オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="b7b27-155">`context`&emsp;A JSON object containing the following fields:</span></span>
  * <span data-ttu-id="b7b27-156">`subEntityId`&emsp;タブ _内_ のアイテムの ID。たとえば、「task456」のようになります</span><span class="sxs-lookup"><span data-stu-id="b7b27-156">`subEntityId`&emsp;An ID for the item _within_ the tab; for example, "task456"</span></span>
  * <span data-ttu-id="b7b27-157">`channelId`&emsp;タブ コンテキストから使用できる Microsoft Teams チャネル [ID。](~/tabs/how-to/access-teams-context.md)たとえば、"19:cbe3683f25094106b826c9cada3afbe0@thread.skype" などです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-157">`channelId`&emsp;The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md); for example, "19:cbe3683f25094106b826c9cada3afbe0@thread.skype".</span></span> <span data-ttu-id="b7b27-158">このプロパティは、「チーム」の範囲を持つ構成可能なタブにのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-158">This property is only available in configurable tabs with a scope of "team".</span></span> <span data-ttu-id="b7b27-159">「個人」の範囲を持つ静的なタブでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="b7b27-159">It is not available in static tabs, which have a scope of "personal".</span></span>

<span data-ttu-id="b7b27-160">例:</span><span class="sxs-lookup"><span data-stu-id="b7b27-160">Examples:</span></span>

* <span data-ttu-id="b7b27-161">構成可能なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="b7b27-161">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="b7b27-162">構成可能なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="b7b27-162">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="b7b27-163">静的なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="b7b27-163">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="b7b27-164">静的なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="b7b27-164">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7b27-165">すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-165">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="b7b27-166">最後の例を使用して、前の例に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7b27-166">You must follow the preceeding examples using the last example:</span></span>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a><span data-ttu-id="b7b27-167">タブからディープ リンクを使用する</span><span class="sxs-lookup"><span data-stu-id="b7b27-167">Consuming a deep link from a tab</span></span>

<span data-ttu-id="b7b27-168">深いリンクに移動すると、Microsoft Teams はタブに移動し、Microsoft Teams JavaScript ライブラリを介してサブエンティティ ID が存在する場合に取得するメカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-168">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism through the Microsoft Teams JavaScript library to retrieve the sub-entity ID if it exists.</span></span>

<span data-ttu-id="b7b27-169">この呼び出しは、タブがディープ リンクを介して移動される場合、フィールドを含 [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) `subEntityId` むコンテキストを返します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-169">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab is navigated through a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="b7b27-170">タブからのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="b7b27-170">Deep linking from your tab</span></span>

<span data-ttu-id="b7b27-171">タブから Teams のコンテンツにディープリンクできます。これは、タブが Teams の他のコンテンツ (チャネル、メッセージ、別のタブ、スケジュール 設定ダイアログを開くなど) にリンクする必要がある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="b7b27-171">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams, such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="b7b27-172">タブからディープリンクをトリガーするには、次のように呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7b27-172">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="b7b27-173">この呼び出しでは、正しい URL に移動したり、スケジュール設定やアプリのインストール ダイアログを開くなどのクライアント アクションをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="b7b27-173">This call navigates you to the correct URL, or trigger a client action, such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="b7b27-174">次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b7b27-174">See the following example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="b7b27-175">チャットへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="b7b27-175">Deep linking to a chat</span></span>

<span data-ttu-id="b7b27-176">参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-176">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="b7b27-177">指定した参加者とチャットが存在しない場合、リンクは空の新しいチャットにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-177">If a chat does not exist with the specified participants, the link navigates the user to an empty new chat.</span></span> <span data-ttu-id="b7b27-178">ユーザーが最初のメッセージを送信するまで、新しいチャットが下書き状態で作成されます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-178">New chats are  created in draft state until the user sends the first message.</span></span> <span data-ttu-id="b7b27-179">それ以外の場合は、チャットが存在しない場合は、ユーザーの作成ボックスに挿入するテキストと共に、チャットの名前を指定できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-179">Otherwise, you can specify the name of the chat if it does not already exist, along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="b7b27-180">この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-180">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="b7b27-181">ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-181">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generate-a-deep-link-to-a-chat"></a><span data-ttu-id="b7b27-182">チャットへのディープ リンクを生成する</span><span class="sxs-lookup"><span data-stu-id="b7b27-182">Generate a deep link to a chat</span></span>

<span data-ttu-id="b7b27-183">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-183">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="b7b27-184">例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="b7b27-184">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="b7b27-185">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-185">The query parameters are:</span></span>

* <span data-ttu-id="b7b27-186">`users`: チャットの参加者を表すユーザー ID のコンマ区切りリストです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-186">`users`: The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="b7b27-187">アクションを実行するユーザーは、常に参加者として含まれます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-187">The user that performs the action is always included as a participant.</span></span> <span data-ttu-id="b7b27-188">現在、User ID フィールドは、通常は電子メール アドレスAD UserPrincipalName の Azure アドレスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b7b27-188">Currently, the User ID field supports the Azure AD UserPrincipalName, typically an email address only.</span></span>
* <span data-ttu-id="b7b27-189">`topicName`: 3 人以上のユーザーとのチャットの場合、チャットの表示名のオプション フィールド。</span><span class="sxs-lookup"><span data-stu-id="b7b27-189">`topicName`: An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="b7b27-190">このフィールドを指定しない場合、チャットの表示名は参加者の名前に基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="b7b27-190">If this field is not specified, the chat's display name is based on the names of the participants.</span></span>
* <span data-ttu-id="b7b27-191">`message`: チャットが下書き状態の間に現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプション フィールド。</span><span class="sxs-lookup"><span data-stu-id="b7b27-191">`message`: An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="b7b27-192">ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。</span><span class="sxs-lookup"><span data-stu-id="b7b27-192">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="generate-deep-links-to-file-in-channel"></a><span data-ttu-id="b7b27-193">チャネル内のファイルへのディープ リンクを生成する</span><span class="sxs-lookup"><span data-stu-id="b7b27-193">Generate deep links to file in channel</span></span>

<span data-ttu-id="b7b27-194">ボット、コネクタ、またはメッセージング拡張機能カードでは、次のディープ リンク形式を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-194">The following deep link format can be used in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/I/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

<span data-ttu-id="b7b27-195">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-195">The query parameters are:</span></span>

* <span data-ttu-id="b7b27-196">`tenantId`: テナント ID の例、0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span><span class="sxs-lookup"><span data-stu-id="b7b27-196">`tenantId`: Tenant ID example, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span></span>
* <span data-ttu-id="b7b27-197">`fileType`: docx、pptx、xlsx、pdf などのサポートされているファイルの種類</span><span class="sxs-lookup"><span data-stu-id="b7b27-197">`fileType`: Supported file type, such as docx, pptx, xlsx, and pdf</span></span>
* <span data-ttu-id="b7b27-198">`objectUrl`: ファイルのオブジェクト URL、 https://microsoft.sharepoint.com/teams/(filepath)</span><span class="sxs-lookup"><span data-stu-id="b7b27-198">`objectUrl`: Object URL of the file, https://microsoft.sharepoint.com/teams/(filepath)</span></span>
* <span data-ttu-id="b7b27-199">`baseUrl`: ファイルの基本 URL、 https://microsoft.sharepoint.com/teams</span><span class="sxs-lookup"><span data-stu-id="b7b27-199">`baseUrl`: Base URL of the file, https://microsoft.sharepoint.com/teams</span></span>
* <span data-ttu-id="b7b27-200">`serviceName`: サービスの名前、アプリ ID</span><span class="sxs-lookup"><span data-stu-id="b7b27-200">`serviceName`: Name of the service, app ID</span></span>
* <span data-ttu-id="b7b27-201">`threadId`: threadId は、ファイルが保存されているチームのチーム ID です。</span><span class="sxs-lookup"><span data-stu-id="b7b27-201">`threadId`: The threadId is the team ID of the team where the file is stored.</span></span> <span data-ttu-id="b7b27-202">これはオプションであり、ユーザーの OneDrive フォルダーに格納されているファイルには設定できません。</span><span class="sxs-lookup"><span data-stu-id="b7b27-202">It is optional and cannot be set for files stored in a user's OneDrive folder.</span></span> <span data-ttu-id="b7b27-203">threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span><span class="sxs-lookup"><span data-stu-id="b7b27-203">threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span></span>
* <span data-ttu-id="b7b27-204">`groupId`: ファイルのグループ ID ae063b79-5315-4ddb-ba70-27328ba6c31e</span><span class="sxs-lookup"><span data-stu-id="b7b27-204">`groupId`: Group ID of the file, ae063b79-5315-4ddb-ba70-27328ba6c31e</span></span>

<span data-ttu-id="b7b27-205">ファイルへのディープリンクのサンプル形式を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-205">Following is the sample format of deeplink to files:</span></span>

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a><span data-ttu-id="b7b27-206">このオブジェクトのシリアル化:</span><span class="sxs-lookup"><span data-stu-id="b7b27-206">Serialization of this object:</span></span>
```
{
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```
## <a name="deep-links-for-sharepoint-framework-tabs"></a><span data-ttu-id="b7b27-207">SharePoint Framework タブのディープ リンク</span><span class="sxs-lookup"><span data-stu-id="b7b27-207">Deep links for SharePoint Framework tabs</span></span>

<span data-ttu-id="b7b27-208">ボット、コネクタ、またはメッセージング拡張カードでは、次のディープ リンク形式を使用できます。 `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span><span class="sxs-lookup"><span data-stu-id="b7b27-208">The following deep link format can be used in a bot, connector or messaging extension card: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span></span>

> [!NOTE]
> <span data-ttu-id="b7b27-209">ボットがディープ リンクを含む TextBlock メッセージを送信すると、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-209">When a bot sends a TextBlock message with a deep link, a new browser tab opens when users select the link.</span></span> <span data-ttu-id="b7b27-210">これは、Linux で実行されている Chrome および Microsoft Teams デスクトップ アプリで発生します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-210">This happens in Chrome and Microsoft Teams desktop app running on Linux.</span></span>
> <span data-ttu-id="b7b27-211">ボットが同じディープ リンク URL を A に送信すると、ユーザーがリンクを選択すると、現在のブラウザーで `Action.OpenUrl` [Teams] タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-211">If the bot sends the same deep link URL into an `Action.OpenUrl`, the Teams tab opens in the current browser when the user selects the link.</span></span> <span data-ttu-id="b7b27-212">新しいブラウザー タブは開きません。</span><span class="sxs-lookup"><span data-stu-id="b7b27-212">No new browser tab is opened.</span></span>

<span data-ttu-id="b7b27-213">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-213">The query parameters are:</span></span>

* <span data-ttu-id="b7b27-214">`appID`: マニフェスト ID fe4a8eba-2a31-4737-8e33-e5fae6fee194。</span><span class="sxs-lookup"><span data-stu-id="b7b27-214">`appID`: Your manifest ID fe4a8eba-2a31-4737-8e33-e5fae6fee194.</span></span>
* <span data-ttu-id="b7b27-215">`entityID`: タブの構成時に指定 [したアイテム ID](~/tabs/how-to/create-tab-pages/configuration-page.md)です。たとえば **、tasklist123**.</span><span class="sxs-lookup"><span data-stu-id="b7b27-215">`entityID`: The item ID that you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md). For example, **tasklist123**.</span></span>
* <span data-ttu-id="b7b27-216">`entityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド https://tasklist.example.com/123 。 https://tasklist.example.com/list123/task456</span><span class="sxs-lookup"><span data-stu-id="b7b27-216">`entityWebUrl`: An optional field with a fallback URL to use if the client does not support rendering of the tab - https://tasklist.example.com/123 or https://tasklist.example.com/list123/task456.</span></span>
* <span data-ttu-id="b7b27-217">`entityName`: タブ内のアイテムのラベルで、ディープ リンクであるタスク リスト 123 またはタスク 456 を表示するときに使用します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-217">`entityName`: A label for the item in your tab, to use when displaying the deep link, Task List 123 or Task 456.</span></span>

<span data-ttu-id="b7b27-218">例: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span><span class="sxs-lookup"><span data-stu-id="b7b27-218">Example: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span></span>

## <a name="linking-to-the-scheduling-dialog"></a><span data-ttu-id="b7b27-219">スケジュール設定ダイアログへのリンクの設定</span><span class="sxs-lookup"><span data-stu-id="b7b27-219">Linking to the scheduling dialog</span></span>

> [!Note]
> <span data-ttu-id="b7b27-220">この機能は現在、開発者プレビュー段階です。</span><span class="sxs-lookup"><span data-stu-id="b7b27-220">This feature is currently in developer preview.</span></span>

<span data-ttu-id="b7b27-221">Teams の組み込みスケジュール ダイアログへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b7b27-221">You can create deep links to the Teams built-in scheduling dialog.</span></span> <span data-ttu-id="b7b27-222">これは、アプリがカレンダーやスケジュールに関連するタスクをユーザーに支援する場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="b7b27-222">This is especially useful if your app helps the user complete calendar or scheduling-related tasks.</span></span>

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="b7b27-223">スケジュール設定ダイアログへのディープ リンクを作成する</span><span class="sxs-lookup"><span data-stu-id="b7b27-223">Generating a deep link to the scheduling dialog</span></span>

<span data-ttu-id="b7b27-224">ボット、コネクタ、またはメッセージング拡張カードで使用できるディープ リンクには、次の形式を使用します。 `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="b7b27-224">Use the following format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="b7b27-225">例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="b7b27-225">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="b7b27-226">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-226">The query parameters are:</span></span>

* <span data-ttu-id="b7b27-227">`attendees`: 会議の出席者を表すユーザー ID のオプションのコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="b7b27-227">`attendees`: The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="b7b27-228">アクションを実行するユーザーは、会議の開催者です。</span><span class="sxs-lookup"><span data-stu-id="b7b27-228">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="b7b27-229">[ユーザー ID] フィールドは現在、Azure AD UserPrincipalName (通常は電子メール アドレス) のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b7b27-229">The User ID field currently only supports the Azure AD UserPrincipalName, typically an email address.</span></span>
* <span data-ttu-id="b7b27-230">`startTime`: イベントのオプションの開始時刻です。</span><span class="sxs-lookup"><span data-stu-id="b7b27-230">`startTime`: The optional start time of the event.</span></span> <span data-ttu-id="b7b27-231">これは *、2018-03-12T23:55:25+02:00* など、長い [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)形式である必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7b27-231">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example *2018-03-12T23:55:25+02:00*.</span></span>
* <span data-ttu-id="b7b27-232">`endTime`: イベントのオプションの終了時刻 (ISO 8601 形式)。</span><span class="sxs-lookup"><span data-stu-id="b7b27-232">`endTime`: The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="b7b27-233">`subject`: 会議の件名の省略可能なフィールドです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-233">`subject`: An optional field for the meeting subject.</span></span>
* <span data-ttu-id="b7b27-234">`content`: 会議の詳細フィールドのオプション フィールドです。</span><span class="sxs-lookup"><span data-stu-id="b7b27-234">`content`: An optional field for the meeting details field.</span></span>

> [!NOTE]
> <span data-ttu-id="b7b27-235">現在、場所の指定はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b7b27-235">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="b7b27-236">UTC オフセットを指定する必要があります。開始時刻と終了時刻を生成するときにタイム ゾーンを意味します。</span><span class="sxs-lookup"><span data-stu-id="b7b27-236">You must specify the UTC offset, it means time zones when generating your start and end times.</span></span>

<span data-ttu-id="b7b27-237">ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。</span><span class="sxs-lookup"><span data-stu-id="b7b27-237">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>
