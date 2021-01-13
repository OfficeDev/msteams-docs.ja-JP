---
title: コンテンツへのディープ リンクを作成する
description: ディープ リンクとアプリでの使用方法について説明する
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: 35aceba4b569baac9283a3355ee5719273145652
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797786"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a><span data-ttu-id="fb38d-104">Microsoft Teams のコンテンツと機能へのディープ リンクを作成する</span><span class="sxs-lookup"><span data-stu-id="fb38d-104">Create deep links to content and features in Microsoft Teams</span></span>

<span data-ttu-id="fb38d-105">Teams 内の情報と機能へのリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-105">You can create links to information and features within Teams.</span></span> <span data-ttu-id="fb38d-106">これが役に立つ例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-106">Examples of where this may be useful:</span></span>

* <span data-ttu-id="fb38d-107">アプリのいずれかのタブ内のコンテンツにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-107">Navigating the user to content within one of your app's tabs.</span></span> <span data-ttu-id="fb38d-108">たとえば、アプリに重要なアクティビティをユーザーに通知するメッセージを送信するボットがある場合があります。</span><span class="sxs-lookup"><span data-stu-id="fb38d-108">For instance, your app may have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="fb38d-109">ユーザーが通知をタップすると、ディープ リンクがタブに移動し、ユーザーがアクティビティの詳細を表示できます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-109">When the user taps on the notification, the deep link navigates to the tab so the user can view more details about the activity.</span></span>
* <span data-ttu-id="fb38d-110">アプリは、必要なパラメーターを使用してディープ リンクを事前に入力して、チャットの作成や会議のスケジュール設定などの特定のユーザー タスクを自動化または単純化します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre-populating the deep links with required parameters.</span></span> <span data-ttu-id="fb38d-111">これにより、ユーザーが手動で情報を入力する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="fb38d-111">This avoids the need for users to manually enter information.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fb38d-112">ディープリンクは、次のようにコンテンツと情報に移動する前にブラウザーを最初に起動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-112">A deeplink launches the browser first before navigating to content and information as follows:</span></span>
>
> <span data-ttu-id="fb38d-113">**タブ**:</span><span class="sxs-lookup"><span data-stu-id="fb38d-113">**Tab**:</span></span>  
> <span data-ttu-id="fb38d-114">✔ ディープリンクの URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-114">✔ Directly navigates to the deeplink url.</span></span>
>
> <span data-ttu-id="fb38d-115">**ボット**:</span><span class="sxs-lookup"><span data-stu-id="fb38d-115">**Bot**:</span></span>  
> <span data-ttu-id="fb38d-116">✔ カード本文のディープリンク - ブラウザーを最初に開きます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-116">✔ Deeplink in card body - Opens in browser first.</span></span>  
> <span data-ttu-id="fb38d-117">✔ アダプティブ カードの OpenURL アクションに追加されたディープリンク - ディープリンクの URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-117">✔ Deeplink added to OpenURL action in Adaptive Card - Directly navigates to the deeplink url.</span></span>  
> <span data-ttu-id="fb38d-118">✔ カードのハイパーリンク マークダウン テキスト - ブラウザーを最初に開きます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-118">✔ Hyperlink markdown text in the card - Opens in browser first.</span></span>  
>
> <span data-ttu-id="fb38d-119">**チャット**</span><span class="sxs-lookup"><span data-stu-id="fb38d-119">**Chat**:</span></span>  
> <span data-ttu-id="fb38d-120">✔ テキスト メッセージ ハイパーリンク マークダウン: ディープリンクの URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-120">✔ Text message hyperlink markdown : Directly navigates to deeplink url.</span></span>  
> <span data-ttu-id="fb38d-121">✔ 一般的なチャット会話に貼り付けられたリンク - ディープリンクの URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-121">✔ Link pasted in general chat conversation - Directly navigates to deeplink url.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="fb38d-122">タブへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="fb38d-122">Deep linking to your tab</span></span>

<span data-ttu-id="fb38d-123">Teams のエンティティへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="fb38d-124">通常は、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーはリンクを作成して、個々のタスクに共有することができます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-124">Typically, this is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list team members may create and share links to individual tasks.</span></span> <span data-ttu-id="fb38d-125">このリンクをクリックすると、特定のアイテムにフォーカスするタブに移動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-125">When clicked, the link navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="fb38d-126">これを実装するには、各アイテムに「リンクのコピー」アクションを UI に最適な方法で追加します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-126">To implement this, you add a "copy link" action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="fb38d-127">このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-127">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="fb38d-128">この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-128">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="fb38d-129">または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-129">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="fb38d-130">これらは、タブまたはタブ内の[](~/bots/what-are-bots.md)アイテムに[](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)対する変更をユーザーに通知するボットおよびコネクタ メッセージで使用できます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-130">You might want to use these in [bot](~/bots/what-are-bots.md) and [connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="fb38d-131">これは **[リンクをタブにコピー]** メニュー項目によって提供されるリンクとは異なり、このタブを指すディープ リンクを生成するだけです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-131">This is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

>[!NOTE]
> <span data-ttu-id="fb38d-132">現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="fb38d-132">Currently, shareDeepLink does not work on mobile platforms.</span></span>

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="fb38d-133">タブ内のアイテムへのディープ リンクを表示する</span><span class="sxs-lookup"><span data-stu-id="fb38d-133">Showing a deep link to an item within your tab</span></span>

<span data-ttu-id="fb38d-134">タブ内のアイテムへのディープ リンクを含むダイアログ ボックスを表示するには、`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` を呼び出します</span><span class="sxs-lookup"><span data-stu-id="fb38d-134">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span></span>

<span data-ttu-id="fb38d-135">次のフィールドを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-135">Provide these fields:</span></span>

* <span data-ttu-id="fb38d-136">`subEntityId`&emsp;タブ内でディープ リンクを設定しているアイテムの一意の識別子</span><span class="sxs-lookup"><span data-stu-id="fb38d-136">`subEntityId`&emsp;A unique identifier for the item within your tab to which you are deep linking</span></span>
* <span data-ttu-id="fb38d-137">`subEntityLabel`&emsp;ディープ リンクを表示するために使用するアイテムのラベル</span><span class="sxs-lookup"><span data-stu-id="fb38d-137">`subEntityLabel`&emsp;A label for the item to use for displaying the deep link</span></span>
* <span data-ttu-id="fb38d-138">`subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用する代替 URL を含むオプションのフィールド</span><span class="sxs-lookup"><span data-stu-id="fb38d-138">`subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab</span></span>

### <a name="generating-a-deep-link-to-your-tab"></a><span data-ttu-id="fb38d-139">タブへのディープ リンクを作成する</span><span class="sxs-lookup"><span data-stu-id="fb38d-139">Generating a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="fb38d-140">[個人用] タブには `personal` 範囲が設定され、チャネルタブとグループ タブでは範囲 `team` が `group` 使用されます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-140">Personal tabs have a `personal` scope, while channel and group tabs use `team` or `group` scopes.</span></span> <span data-ttu-id="fb38d-141">構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。</span><span class="sxs-lookup"><span data-stu-id="fb38d-141">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="fb38d-142">タブ スコープ [の詳細](~/resources/schema/manifest-schema.md) については、マニフェスト リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb38d-142">See the [manifest](~/resources/schema/manifest-schema.md) reference for more information on tab scopes.</span></span>

> [!NOTE]
> <span data-ttu-id="fb38d-143">ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-143">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="fb38d-144">エンティティ ID のないタブへのディープ リンクは、引き続きタブに移動しますが、サブ エンティティ ID をタブに提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="fb38d-144">Deep links to tabs without entity IDs still navigate to the tab but can't provide the sub-entity ID to the tab.</span></span>

<span data-ttu-id="fb38d-145">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-145">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> <span data-ttu-id="fb38d-146">ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-146">If the bot sends a message containing a `TextBlock` with a deep link, then a new browser tab is opened when the user selects the link.</span></span> <span data-ttu-id="fb38d-147">これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-147">This happens in Chrome and in the Microsoft Teams desktop app, both running on Linux.</span></span>
> <span data-ttu-id="fb38d-148">ボットが同じディープ リンク URL を `Action.OpenUrl` に送信する場合、ユーザーがリンクをクリックすると、現在のブラウザー　タブで [Teams] タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-148">If the bot sends the same deep link URL into an `Action.OpenUrl`, then the Teams tab is opened in the current browser tab when the user clicks on the link.</span></span> <span data-ttu-id="fb38d-149">新しいブラウザー タブは開きません。</span><span class="sxs-lookup"><span data-stu-id="fb38d-149">No new browser tab is opened.</span></span>

<span data-ttu-id="fb38d-150">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-150">The query parameters are:</span></span>

* <span data-ttu-id="fb38d-151">`appId`&emsp;マニフェストの ID。たとえば、「fe4a8eba-2a31-4737-8e33-e5fae6fee194」のようになります</span><span class="sxs-lookup"><span data-stu-id="fb38d-151">`appId`&emsp;The ID from your manifest; for example, "fe4a8eba-2a31-4737-8e33-e5fae6fee194"</span></span>
* <span data-ttu-id="fb38d-152">`entityId`&emsp;タブのアイテムの ID。[タブを構成する](~/tabs/how-to/create-tab-pages/configuration-page.md)ときに表示されます。たとえば、「tasklist123」のようになります</span><span class="sxs-lookup"><span data-stu-id="fb38d-152">`entityId`&emsp;The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md); for example, "tasklist123"</span></span>
* <span data-ttu-id="fb38d-153">`entityWebUrl` または `subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用する代替 URL を含むオプションのフィールド。たとえば、「https://tasklist.example.com/123」または「https://tasklist.example.com/list123/task456」のようになります</span><span class="sxs-lookup"><span data-stu-id="fb38d-153">`entityWebUrl` or `subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab; for example, "https://tasklist.example.com/123" or "https://tasklist.example.com/list123/task456"</span></span>
* <span data-ttu-id="fb38d-154">`entityLabel` または `subEntityLabel`&emsp;ディープ リンクを表示するときに使用するタブのアイテムのラベル。たとえば、「Task List 123」または「Task 456」のようになります</span><span class="sxs-lookup"><span data-stu-id="fb38d-154">`entityLabel` or `subEntityLabel`&emsp;A label for the item in your tab, to use when displaying the deep link; for example, "Task List 123" or "Task 456"</span></span>
* <span data-ttu-id="fb38d-155">`context`&emsp;次のフィールドを含む JSON オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="fb38d-155">`context`&emsp;A JSON object containing the following fields:</span></span>
  * <span data-ttu-id="fb38d-156">`subEntityId`&emsp;タブ _内_ のアイテムの ID。たとえば、「task456」のようになります</span><span class="sxs-lookup"><span data-stu-id="fb38d-156">`subEntityId`&emsp;An ID for the item _within_ the tab; for example, "task456"</span></span>
  * <span data-ttu-id="fb38d-157">`channelId`&emsp;Microsoft Teams チャネル ID (タブ [コンテキスト](~/tabs/how-to/access-teams-context.md)から使用可能。たとえば、「19:cbe3683f25094106b826c9cada3afbe0@thread.skype」のようになります。</span><span class="sxs-lookup"><span data-stu-id="fb38d-157">`channelId`&emsp;The Microsoft Teams channel ID (available from the tab [context](~/tabs/how-to/access-teams-context.md); for example, "19:cbe3683f25094106b826c9cada3afbe0@thread.skype".</span></span> <span data-ttu-id="fb38d-158">このプロパティは、「チーム」の範囲を持つ構成可能なタブにのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-158">This property is only available in configurable tabs with a scope of "team".</span></span> <span data-ttu-id="fb38d-159">「個人」の範囲を持つ静的なタブでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="fb38d-159">It is not available in static tabs, which have a scope of "personal".</span></span>

<span data-ttu-id="fb38d-160">例:</span><span class="sxs-lookup"><span data-stu-id="fb38d-160">Examples:</span></span>

* <span data-ttu-id="fb38d-161">構成可能なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="fb38d-161">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="fb38d-162">構成可能なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="fb38d-162">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="fb38d-163">静的なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="fb38d-163">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="fb38d-164">静的なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="fb38d-164">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb38d-165">すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-165">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="fb38d-166">上記の例では当てはまりませんが、読みやすくするために、行うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="fb38d-166">For the sake of readability, the above examples are not, but you should.</span></span> <span data-ttu-id="fb38d-167">最後の例を使用します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-167">Using the last example:</span></span>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a><span data-ttu-id="fb38d-168">タブからディープ リンクを使用する</span><span class="sxs-lookup"><span data-stu-id="fb38d-168">Consuming a deep link from a tab</span></span>

<span data-ttu-id="fb38d-169">ディープ リンクに移動すると、Microsoft Teams は単にタブに移動し、サブエンティティ ID (存在する場合) を取得するためのメカニズムを Microsoft Teams JavaScript ライブラリを通して提供します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-169">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism via the Microsoft Teams JavaScript library to retrieve the sub-entity ID (if it exists).</span></span>

<span data-ttu-id="fb38d-170">[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) を呼び出すと、ディープ リンクを介してタブに移動する場合、`subEntityId` フィールドを含むコンテンツを返します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-170">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab was navigated to via a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="fb38d-171">タブからのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="fb38d-171">Deep linking from your tab</span></span>

<span data-ttu-id="fb38d-172">タブから Teams のコンテンツにディープ リンクを設定することができます。これは、チャネル、メッセージ、別のタブなど、Teams 内の他のコンテンツにリンクする必要がある場合や、スケジュール設定ダイアログを開く場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="fb38d-172">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="fb38d-173">タブからディープリンクをトリガーするには、次のように呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb38d-173">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="fb38d-174">これにより、正しい URL に移動するか、またはスケジュール設定ダイアログやアプリ インストール ダイアログなどのクライアント アクションをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="fb38d-174">This will navigate you to the correct URL, or trigger a client action such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="fb38d-175">例: </span><span class="sxs-lookup"><span data-stu-id="fb38d-175">Example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="fb38d-176">チャットへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="fb38d-176">Deep linking to a chat</span></span>

<span data-ttu-id="fb38d-177">参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-177">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="fb38d-178">指定した参加者とのチャットが存在しない場合は、リンクは、ユーザーを空の新しいチャットに移動します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-178">If a chat doesn't exist with the specified participants, the link will navigate the user to an empty new chat.</span></span> <span data-ttu-id="fb38d-179">新しいチャットは、ユーザーが最初のメッセージを送信するまで、下書きの状態で作成されます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-179">New chats will be created in draft state until the user sends the first message.</span></span> <span data-ttu-id="fb38d-180">必要に応じて、チャットの名前 (まだ存在しない場合) と、ユーザーの作成ボックスに挿入するテキストを指定することができます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-180">Optionally, you can specify the name of the chat (if it doesn't already exist), along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="fb38d-181">この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-181">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="fb38d-182">ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-182">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generating-a-deep-link-to-a-chat"></a><span data-ttu-id="fb38d-183">チェットへのディープ リンクを作成する</span><span class="sxs-lookup"><span data-stu-id="fb38d-183">Generating a deep link to a chat</span></span>

<span data-ttu-id="fb38d-184">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="fb38d-184">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="fb38d-185">例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="fb38d-185">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="fb38d-186">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-186">The query parameters are:</span></span>

* <span data-ttu-id="fb38d-187">`users`: チャットの参加者を表すユーザー ID のコンマ区切りのリスト。</span><span class="sxs-lookup"><span data-stu-id="fb38d-187">`users`: The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="fb38d-188">アクションを実行するユーザーは、参加者として常に含まれます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-188">The user performing the action is always included as a participant.</span></span> <span data-ttu-id="fb38d-189">現在、[ユーザー ID] フィールドには、Azure AD UserPrincipalName のみがサポートされています (通常はメール アドレス)。</span><span class="sxs-lookup"><span data-stu-id="fb38d-189">The User ID field currently only supports the Azure AD UserPrincipalName (typically an email address).</span></span>
* <span data-ttu-id="fb38d-190">`topicName`: 3 名以上のユーザーとのチャットの場合、チャットの表示名のオプション フィールド。</span><span class="sxs-lookup"><span data-stu-id="fb38d-190">`topicName`: An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="fb38d-191">このフィールドを指定しない場合、チャットの表示名は、参加者の名前に基づきます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-191">If this field is not specified, the chat's display name will be based on the names of the participants.</span></span>
* <span data-ttu-id="fb38d-192">`message`: チャットが下書き状態の間に現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプションのフィールドです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-192">`message`: An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="fb38d-193">ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。</span><span class="sxs-lookup"><span data-stu-id="fb38d-193">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="linking-to-the-scheduling-dialog"></a><span data-ttu-id="fb38d-194">スケジュール設定ダイアログへのリンクの設定</span><span class="sxs-lookup"><span data-stu-id="fb38d-194">Linking to the scheduling dialog</span></span>

> [!Note]
> <span data-ttu-id="fb38d-195">この機能は現在、開発者プレビュー段階です。</span><span class="sxs-lookup"><span data-stu-id="fb38d-195">This feature is currently in developer preview.</span></span>

<span data-ttu-id="fb38d-196">Teams の組み込みスケジュール ダイアログへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fb38d-196">You can create deep links to the Teams built-in scheduling dialog.</span></span> <span data-ttu-id="fb38d-197">これは、アプリがカレンダーやスケジュールに関連するタスクをユーザーに支援する場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="fb38d-197">This is especially useful if your app helps the user complete calendar or scheduling-related tasks.</span></span>

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="fb38d-198">スケジュール設定ダイアログへのディープ リンクを作成する</span><span class="sxs-lookup"><span data-stu-id="fb38d-198">Generating a deep link to the scheduling dialog</span></span>

<span data-ttu-id="fb38d-199">ボット、コネクタ、またはメッセージングの拡張機能カードで使用できるディープ リンクには、次の形式を使用します: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="fb38d-199">Use this format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="fb38d-200">例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="fb38d-200">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="fb38d-201">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-201">The query parameters are:</span></span>

* <span data-ttu-id="fb38d-202">`attendees`: 会議の出席者を表すユーザー ID のコンマ区切りリスト (省略可能)。</span><span class="sxs-lookup"><span data-stu-id="fb38d-202">`attendees`: The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="fb38d-203">アクションを実行するユーザーは、会議の開催者です。</span><span class="sxs-lookup"><span data-stu-id="fb38d-203">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="fb38d-204">現在、[ユーザー ID] フィールドには、Azure AD UserPrincipalName のみがサポートされています (通常はメール アドレス)。</span><span class="sxs-lookup"><span data-stu-id="fb38d-204">The User ID field currently only supports the Azure AD UserPrincipalName (typically an email address).</span></span>
* <span data-ttu-id="fb38d-205">`startTime`: イベントの開始時刻 (省略可能)。</span><span class="sxs-lookup"><span data-stu-id="fb38d-205">`startTime`: The optional start time of the event.</span></span> <span data-ttu-id="fb38d-206">これは、[long ISO 8601 形式](https://en.wikipedia.org/wiki/ISO_8601)、たとえば、「2018-03-12T23:55:25+02:00」にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb38d-206">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example “2018-03-12T23:55:25+02:00”.</span></span>
* <span data-ttu-id="fb38d-207">`endTime`: イベントのオプションの終了時刻(ISO 8601 形式)。</span><span class="sxs-lookup"><span data-stu-id="fb38d-207">`endTime`: The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="fb38d-208">`subject`: 会議の件名の省略可能なフィールドです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-208">`subject`: An optional field for the meeting subject.</span></span>
* <span data-ttu-id="fb38d-209">`content`: 会議の詳細フィールドのオプションのフィールドです。</span><span class="sxs-lookup"><span data-stu-id="fb38d-209">`content`: An optional field for the meeting details field.</span></span>

<span data-ttu-id="fb38d-210">現在、場所の指定はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="fb38d-210">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="fb38d-211">開始時刻と終了時刻を生成するときに、UTC オフセット (タイム ゾーン) を指定してください。</span><span class="sxs-lookup"><span data-stu-id="fb38d-211">When generating your start and end times be sure to specify the UTC offset (time zones).</span></span>

<span data-ttu-id="fb38d-212">ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。</span><span class="sxs-lookup"><span data-stu-id="fb38d-212">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>
