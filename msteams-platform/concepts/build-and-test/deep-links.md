---
title: ディープ リンクの作成
description: ディープ リンクとアプリでの使用方法について説明する
ms.topic: how-to
localization_priority: Normal
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: 837d180b06f69b9be49d898c62b9ab8ee64d51d0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566055"
---
# <a name="create-deep-links"></a><span data-ttu-id="776d1-104">ディープ リンクの作成</span><span class="sxs-lookup"><span data-stu-id="776d1-104">Create deep links</span></span> 

<span data-ttu-id="776d1-105">Teams内の情報や機能へのリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-105">You can create links to information and features within Teams.</span></span> <span data-ttu-id="776d1-106">ディープ リンクを作成する場合は、次のようなシナリオが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="776d1-106">The scenarios where creating deep links are useful are as follows:</span></span>

* <span data-ttu-id="776d1-107">アプリのタブの 1 つ内のコンテンツにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-107">Navigating the user to the content within one of your app's tabs.</span></span> <span data-ttu-id="776d1-108">たとえば、重要なアクティビティをユーザーに通知するメッセージを送信するボットをアプリに含めることができます。</span><span class="sxs-lookup"><span data-stu-id="776d1-108">For instance, your app can have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="776d1-109">ユーザーが通知をタップすると、ディープリンクがタブに移動し、アクティビティの詳細を表示できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-109">When the user taps on the notification, the deep link navigates to the tab so that the user can view more details about the activity.</span></span>
* <span data-ttu-id="776d1-110">アプリは、必要なパラメーターを含むディープ リンクを事前に設定することで、チャットの作成や会議のスケジュールなどの特定のユーザー タスクを自動化または簡略化します。</span><span class="sxs-lookup"><span data-stu-id="776d1-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre populating the deep links with required parameters.</span></span> <span data-ttu-id="776d1-111">これにより、ユーザーが手動で情報を入力する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="776d1-111">This avoids the need for users to manually enter information.</span></span>

> [!NOTE]
>
> <span data-ttu-id="776d1-112">ディープリンクは、コンテンツに移動する前に、まずブラウザを起動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-112">A deeplink launches the browser first before navigating to content.</span></span> <span data-ttu-id="776d1-113">Teamsエンティティのディープ リンクの動作は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="776d1-113">The behaviour of deep links on Teams entities are as follows:</span></span>
>
> <span data-ttu-id="776d1-114">**タブ**:</span><span class="sxs-lookup"><span data-stu-id="776d1-114">**Tab**:</span></span>  
> <span data-ttu-id="776d1-115">✔ ディープリンクの URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-115">✔ Directly navigates to the deeplink url.</span></span>
>
> <span data-ttu-id="776d1-116">**ボット**:</span><span class="sxs-lookup"><span data-stu-id="776d1-116">**Bot**:</span></span>  
> <span data-ttu-id="776d1-117">✔カード本体のディープリンク: 最初にブラウザで開きます。</span><span class="sxs-lookup"><span data-stu-id="776d1-117">✔ Deeplink in card body: Opens in browser first.</span></span>  
> <span data-ttu-id="776d1-118">✔アダプティブカードの OpenURL アクションにディープリンクが追加されました: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-118">✔ Deeplink added to OpenURL action in Adaptive Card: Directly navigates to the deeplink url.</span></span>  
> <span data-ttu-id="776d1-119">✔カードのハイパーリンクマークダウンテキスト: ブラウザで最初に開きます。</span><span class="sxs-lookup"><span data-stu-id="776d1-119">✔ Hyperlink markdown text in the card: Opens in browser first.</span></span>  
>
> <span data-ttu-id="776d1-120">**チャット**</span><span class="sxs-lookup"><span data-stu-id="776d1-120">**Chat**:</span></span>  
> <span data-ttu-id="776d1-121">✔ テキスト メッセージ ハイパーリンクマークダウン: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-121">✔ Text message hyperlink markdown: Directly navigates to deeplink url.</span></span>  
> <span data-ttu-id="776d1-122">✔一般的なチャット会話で貼り付けたリンク: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-122">✔ Link pasted in general chat conversation: Directly navigates to deeplink url.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="776d1-123">タブへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="776d1-123">Deep linking to your tab</span></span>

<span data-ttu-id="776d1-124">Teams のエンティティへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="776d1-125">これは、タブ内のコンテンツや情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーは個々のタスクへのリンクを作成して共有できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-125">This is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list, team members can create and share links to individual tasks.</span></span> <span data-ttu-id="776d1-126">リンクを選択すると、特定の項目に焦点を当てたタブに移動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-126">When you select the link, it navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="776d1-127">これを実装するには、UI に最適な方法で、各項目に **コピー リンク** アクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="776d1-127">To implement this, you add a **copy link** action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="776d1-128">このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="776d1-128">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="776d1-129">この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。</span><span class="sxs-lookup"><span data-stu-id="776d1-129">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="776d1-130">または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="776d1-130">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="776d1-131">[ボット](~/bots/what-are-bots.md)と[コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)のメッセージにディープ リンクを使用して、タブの変更や、その中のアイテムの変更をユーザーに知らせることができます。</span><span class="sxs-lookup"><span data-stu-id="776d1-131">You can use deep links in [bot](~/bots/what-are-bots.md) and [connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="776d1-132">このディープ リンクは、[ **リンクをタブにコピー** ] メニュー項目によって提供されるリンクとは異なり、このタブを指すディープ リンクが生成されます。</span><span class="sxs-lookup"><span data-stu-id="776d1-132">This deep link is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

>[!NOTE]
> <span data-ttu-id="776d1-133">現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="776d1-133">Currently, shareDeepLink does not work on mobile platforms.</span></span>

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="776d1-134">タブ内の項目へのディープリンクを表示する</span><span class="sxs-lookup"><span data-stu-id="776d1-134">Show a deep link to an item within your tab</span></span>

<span data-ttu-id="776d1-135">タブ内の項目へのディープリンクを含むダイアログボックスを表示するには、 を呼び出 `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` します。</span><span class="sxs-lookup"><span data-stu-id="776d1-135">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`.</span></span>

<span data-ttu-id="776d1-136">次のフィールドを指定します。</span><span class="sxs-lookup"><span data-stu-id="776d1-136">Provide the following fields:</span></span>

* <span data-ttu-id="776d1-137">`subEntityId`: 深いリンクを設定しているタブ内の項目の一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="776d1-137">`subEntityId`: A unique identifier for the item within your tab to which you are deep linking.</span></span>
* <span data-ttu-id="776d1-138">`subEntityLabel`: ディープ リンクの表示に使用するアイテムのラベル。</span><span class="sxs-lookup"><span data-stu-id="776d1-138">`subEntityLabel`: A label for the item to use for displaying the deep link.</span></span>
* <span data-ttu-id="776d1-139">`subEntityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションのフィールド。</span><span class="sxs-lookup"><span data-stu-id="776d1-139">`subEntityWebUrl`: An optional field with a fallback URL to use if the client does not support rendering the tab.</span></span>

### <a name="generate-a-deep-link-to-your-tab"></a><span data-ttu-id="776d1-140">タブへのディープリンクを生成する</span><span class="sxs-lookup"><span data-stu-id="776d1-140">Generate a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="776d1-141">個人タブには `personal` スコープがあり、チャンネルタブとグループタブ `team` `group` はスコープを使用します。</span><span class="sxs-lookup"><span data-stu-id="776d1-141">Personal tabs have a `personal` scope, while channel and group tabs use `team` or `group` scopes.</span></span> <span data-ttu-id="776d1-142">構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。</span><span class="sxs-lookup"><span data-stu-id="776d1-142">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="776d1-143">タブスコープの詳細については、 [マニフェスト](~/resources/schema/manifest-schema.md) リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="776d1-143">See the [manifest](~/resources/schema/manifest-schema.md) reference for more information on tab scopes.</span></span>

> [!NOTE]
> <span data-ttu-id="776d1-144">ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="776d1-144">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="776d1-145">エンティティ ID のないタブへのディープ リンクは、タブに移動しますが、サブエンティティ ID をタブに提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="776d1-145">Deep links to tabs without entity IDs still navigate to the tab but cannot provide the sub entity ID to the tab.</span></span>

<span data-ttu-id="776d1-146">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="776d1-146">Use the following format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> <span data-ttu-id="776d1-147">ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="776d1-147">If the bot sends a message containing a `TextBlock` with a deep link, then a new browser tab is opened when the user selects the link.</span></span> <span data-ttu-id="776d1-148">これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。</span><span class="sxs-lookup"><span data-stu-id="776d1-148">This happens in Chrome and in the Microsoft Teams desktop app, both running on Linux.</span></span>
> <span data-ttu-id="776d1-149">ボットが同じディープ リンク URL `Action.OpenUrl` を に送信した場合、ユーザーがリンクを選択したときに、現在のブラウザ タブで [Teams] タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="776d1-149">If the bot sends the same deep link URL into an `Action.OpenUrl`, then the Teams tab is opened in the current browser tab when the user selects the link.</span></span> <span data-ttu-id="776d1-150">新しいブラウザ タブは開かれていない。</span><span class="sxs-lookup"><span data-stu-id="776d1-150">A new browser tab is not opened.</span></span>

<span data-ttu-id="776d1-151">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="776d1-151">The query parameters are:</span></span>

| <span data-ttu-id="776d1-152">パラメーター名</span><span class="sxs-lookup"><span data-stu-id="776d1-152">Parameter name</span></span> | <span data-ttu-id="776d1-153">説明</span><span class="sxs-lookup"><span data-stu-id="776d1-153">Description</span></span> | <span data-ttu-id="776d1-154">例</span><span class="sxs-lookup"><span data-stu-id="776d1-154">Example</span></span> |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | <span data-ttu-id="776d1-155">マニフェストの ID。</span><span class="sxs-lookup"><span data-stu-id="776d1-155">The ID from your manifest.</span></span> |<span data-ttu-id="776d1-156">fe4a8eba-2a31-4737-8e33-e5fae6fee194</span><span class="sxs-lookup"><span data-stu-id="776d1-156">fe4a8eba-2a31-4737-8e33-e5fae6fee194</span></span>|
| `entityId`&emsp; | <span data-ttu-id="776d1-157">タブの構成時に指定したタブ内の項目 [の](~/tabs/how-to/create-tab-pages/configuration-page.md)ID。</span><span class="sxs-lookup"><span data-stu-id="776d1-157">The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>|<span data-ttu-id="776d1-158">タスクリスト123</span><span class="sxs-lookup"><span data-stu-id="776d1-158">Tasklist123</span></span>|
| <span data-ttu-id="776d1-159">`entityWebUrl` 又は `subEntityWebUrl`&emsp;</span><span class="sxs-lookup"><span data-stu-id="776d1-159">`entityWebUrl` or `subEntityWebUrl`&emsp;</span></span> | <span data-ttu-id="776d1-160">クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションのフィールド。</span><span class="sxs-lookup"><span data-stu-id="776d1-160">An optional field with a fallback URL to use if the client does not support rendering the tab.</span></span> | <span data-ttu-id="776d1-161"> https://tasklist.example.com/123 または https://tasklist.example.com/list123/task456</span><span class="sxs-lookup"><span data-stu-id="776d1-161">https://tasklist.example.com/123 or https://tasklist.example.com/list123/task456</span></span> |
| <span data-ttu-id="776d1-162">`entityLabel` 又は `subEntityLabel`&emsp;</span><span class="sxs-lookup"><span data-stu-id="776d1-162">`entityLabel` or `subEntityLabel`&emsp;</span></span> | <span data-ttu-id="776d1-163">深いリンクを表示するときに使用する、タブ内の項目のラベル。</span><span class="sxs-lookup"><span data-stu-id="776d1-163">A label for the item in your tab, to use when displaying the deep link.</span></span> | <span data-ttu-id="776d1-164">タスク リスト 123 または "タスク 456</span><span class="sxs-lookup"><span data-stu-id="776d1-164">Task List 123 or "Task 456</span></span> |
| <span data-ttu-id="776d1-165">`context`&emsp;</span><span class="sxs-lookup"><span data-stu-id="776d1-165">`context`&emsp;</span></span> </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| <span data-ttu-id="776d1-166">次のフィールドを含む JSON オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="776d1-166">A JSON object containing the following fields:</span></span></br></br> <span data-ttu-id="776d1-167">\* タブ内の項目の ID。</span><span class="sxs-lookup"><span data-stu-id="776d1-167">\* An ID for the item within the tab.</span></span> </br></br> <span data-ttu-id="776d1-168">\* タブ[コンテキスト](~/tabs/how-to/access-teams-context.md)から取得できるMicrosoft Teamsチャネル ID。</span><span class="sxs-lookup"><span data-stu-id="776d1-168">\*  The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md).</span></span> | 
| `subEntityId`&emsp; | <span data-ttu-id="776d1-169">タブ内の項目の ID。</span><span class="sxs-lookup"><span data-stu-id="776d1-169">An ID for the item within the tab.</span></span> |<span data-ttu-id="776d1-170">タスク456</span><span class="sxs-lookup"><span data-stu-id="776d1-170">Task456</span></span> |
| `channelId`&emsp; | <span data-ttu-id="776d1-171">タブ[コンテキスト](~/tabs/how-to/access-teams-context.md)から取得できるMicrosoft Teams チャネル ID。</span><span class="sxs-lookup"><span data-stu-id="776d1-171">The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="776d1-172">このプロパティは、 **チーム** のスコープを持つ構成可能なタブでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-172">This property is only available in configurable tabs with a scope of **team**.</span></span> <span data-ttu-id="776d1-173">**個人用** のスコープを持つ静的タブでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="776d1-173">It is not available in static tabs, which have a scope of **personal**.</span></span>| <span data-ttu-id="776d1-174">19:cbe3683f25094106b826c9cada3afbe0@thread.skype</span><span class="sxs-lookup"><span data-stu-id="776d1-174">19:cbe3683f25094106b826c9cada3afbe0@thread.skype</span></span> |

<span data-ttu-id="776d1-175">例:</span><span class="sxs-lookup"><span data-stu-id="776d1-175">Examples:</span></span>

* <span data-ttu-id="776d1-176">構成可能なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="776d1-176">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="776d1-177">構成可能なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="776d1-177">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="776d1-178">静的なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="776d1-178">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="776d1-179">静的なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="776d1-179">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="776d1-180">すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="776d1-180">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="776d1-181">最後の例を使用して、前の例に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="776d1-181">You must follow the preceeding examples using the last example:</span></span>

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a><span data-ttu-id="776d1-182">タブからディープ リンクを使用する</span><span class="sxs-lookup"><span data-stu-id="776d1-182">Consume a deep link from a tab</span></span>

<span data-ttu-id="776d1-183">ディープ リンクに移動すると、Microsoft Teamsタブに移動するだけで、サブエンティティ ID が存在する場合は、Microsoft Teams JavaScript ライブラリを通じてそのサブエンティティ ID を取得するメカニズムが提供されます。</span><span class="sxs-lookup"><span data-stu-id="776d1-183">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism through the Microsoft Teams JavaScript library to retrieve the sub-entity ID if it exists.</span></span>

<span data-ttu-id="776d1-184">[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-)この呼び出しは、 `subEntityId` タブがディープ リンクを介してナビゲートされた場合に、フィールドを含むコンテキストを返します。</span><span class="sxs-lookup"><span data-stu-id="776d1-184">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab is navigated through a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="776d1-185">タブからのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="776d1-185">Deep linking from your tab</span></span>

<span data-ttu-id="776d1-186">タブからTeams内のコンテンツにディープリンクできます。これは、タブがチャンネル、メッセージ、別のタブ、またはスケジューリングダイアログを開くなど、Teams内の他のコンテンツにリンクする必要がある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="776d1-186">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams, such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="776d1-187">タブからディープリンクをトリガーするには、次のように呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="776d1-187">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="776d1-188">この呼び出しは、正しい URL に移動するか、スケジュールやアプリのインストール ダイアログを開くなどのクライアント アクションをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="776d1-188">This call navigates you to the correct URL, or trigger a client action, such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="776d1-189">次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="776d1-189">See the following example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="776d1-190">チャットへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="776d1-190">Deep linking to a chat</span></span>

<span data-ttu-id="776d1-191">参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-191">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="776d1-192">指定した参加者とチャットが存在しない場合、リンクは空の新しいチャットにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="776d1-192">If a chat does not exist with the specified participants, the link navigates the user to an empty new chat.</span></span> <span data-ttu-id="776d1-193">新しいチャットは、ユーザーが最初のメッセージを送信するまでドラフト状態で作成されます。</span><span class="sxs-lookup"><span data-stu-id="776d1-193">New chats are  created in draft state until the user sends the first message.</span></span> <span data-ttu-id="776d1-194">それ以外の場合は、チャットの名前が存在しない場合は、ユーザーの作成ボックスに挿入する必要があるテキストと共に指定できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-194">Otherwise, you can specify the name of the chat if it does not already exist, along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="776d1-195">この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。</span><span class="sxs-lookup"><span data-stu-id="776d1-195">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="776d1-196">ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。</span><span class="sxs-lookup"><span data-stu-id="776d1-196">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generate-a-deep-link-to-a-chat"></a><span data-ttu-id="776d1-197">チャットへのディープリンクを生成する</span><span class="sxs-lookup"><span data-stu-id="776d1-197">Generate a deep link to a chat</span></span>

<span data-ttu-id="776d1-198">この形式は、ボット、コネクタ、またはメッセージング拡張カードで使用できるディープ リンクに使用します。</span><span class="sxs-lookup"><span data-stu-id="776d1-198">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="776d1-199">例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="776d1-199">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="776d1-200">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="776d1-200">The query parameters are:</span></span>

* <span data-ttu-id="776d1-201">`users`: チャットの参加者を表すユーザー ID のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="776d1-201">`users`: The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="776d1-202">アクションを実行するユーザーは、常に参加者として含まれます。</span><span class="sxs-lookup"><span data-stu-id="776d1-202">The user that performs the action is always included as a participant.</span></span> <span data-ttu-id="776d1-203">現在、ユーザー ID フィールドは、電子メール アドレスなど、Azure AD ユーザー プリンシパル名をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="776d1-203">Currently, the User ID field supports the Azure AD UserPrincipalName, such as an email address only.</span></span>
* <span data-ttu-id="776d1-204">`topicName`: チャットの表示名 (3 人以上のユーザーとチャットの場合) のオプションフィールド。</span><span class="sxs-lookup"><span data-stu-id="776d1-204">`topicName`: An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="776d1-205">このフィールドを指定しない場合、チャットの表示名は参加者の名前に基づいて作成されます。</span><span class="sxs-lookup"><span data-stu-id="776d1-205">If this field is not specified, the chat's display name is based on the names of the participants.</span></span>
* <span data-ttu-id="776d1-206">`message`: チャットが下書き状態のときに、現在のユーザーの作成ボックスに挿入するメッセージ テキストの省略可能なフィールド。</span><span class="sxs-lookup"><span data-stu-id="776d1-206">`message`: An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="776d1-207">ボットとのディープリンクを使用するには、カードのボタンで URL ターゲットとして指定するか、 `openUrl` アクションタイプをタップします。</span><span class="sxs-lookup"><span data-stu-id="776d1-207">To use this deep link with your bot, specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="generate-deep-links-to-file-in-channel"></a><span data-ttu-id="776d1-208">チャネル内のファイルへのディープリンクを生成する</span><span class="sxs-lookup"><span data-stu-id="776d1-208">Generate deep links to file in channel</span></span>

<span data-ttu-id="776d1-209">次のディープ リンク形式は、ボット、コネクタ、またはメッセージング拡張カードで使用できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-209">The following deep link format can be used in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

<span data-ttu-id="776d1-210">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="776d1-210">The query parameters are:</span></span>

* <span data-ttu-id="776d1-211">`tenantId`: テナント ID の例, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span><span class="sxs-lookup"><span data-stu-id="776d1-211">`tenantId`: Tenant ID example, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span></span>
* <span data-ttu-id="776d1-212">`fileType`: サポートされているファイルの種類 (docx、pptx、xlsx、pdf など)</span><span class="sxs-lookup"><span data-stu-id="776d1-212">`fileType`: Supported file type, such as docx, pptx, xlsx, and pdf</span></span>
* <span data-ttu-id="776d1-213">`objectUrl`: ファイルのオブジェクト URL、 https://microsoft.sharepoint.com/teams/(filepath)</span><span class="sxs-lookup"><span data-stu-id="776d1-213">`objectUrl`: Object URL of the file, https://microsoft.sharepoint.com/teams/(filepath)</span></span>
* <span data-ttu-id="776d1-214">`baseUrl`: ファイルのベース URL https://microsoft.sharepoint.com/teams</span><span class="sxs-lookup"><span data-stu-id="776d1-214">`baseUrl`: Base URL of the file, https://microsoft.sharepoint.com/teams</span></span>
* <span data-ttu-id="776d1-215">`serviceName`: サービス名、アプリ ID</span><span class="sxs-lookup"><span data-stu-id="776d1-215">`serviceName`: Name of the service, app ID</span></span>
* <span data-ttu-id="776d1-216">`threadId`: スレッド ID は、ファイルが格納されているチームのチーム ID です。</span><span class="sxs-lookup"><span data-stu-id="776d1-216">`threadId`: The threadId is the team ID of the team where the file is stored.</span></span> <span data-ttu-id="776d1-217">これはオプションであり、ユーザーのOneDriveフォルダーに格納されているファイルに対しては設定できません。</span><span class="sxs-lookup"><span data-stu-id="776d1-217">It is optional and cannot be set for files stored in a user's OneDrive folder.</span></span> <span data-ttu-id="776d1-218">スレッド Id - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span><span class="sxs-lookup"><span data-stu-id="776d1-218">threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span></span>
* <span data-ttu-id="776d1-219">`groupId`: ファイルのグループ ID ae063b79-5315-4ddb-ba70-27328ba6c31e</span><span class="sxs-lookup"><span data-stu-id="776d1-219">`groupId`: Group ID of the file, ae063b79-5315-4ddb-ba70-27328ba6c31e</span></span>

<span data-ttu-id="776d1-220">ファイルへのディープリンクの形式の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="776d1-220">Following is the sample format of deeplink to files:</span></span>

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a><span data-ttu-id="776d1-221">このオブジェクトのシリアル化:</span><span class="sxs-lookup"><span data-stu-id="776d1-221">Serialization of this object:</span></span>
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
## <a name="deep-linking-for-sharepoint-framework-tabs"></a><span data-ttu-id="776d1-222">SharePoint Frameworkタブのディープリンク</span><span class="sxs-lookup"><span data-stu-id="776d1-222">Deep linking for SharePoint Framework tabs</span></span>

<span data-ttu-id="776d1-223">次のディープ リンク形式は、ボット、コネクタ、またはメッセージング拡張カードで使用できます。 `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span><span class="sxs-lookup"><span data-stu-id="776d1-223">The following deep link format can be used in a bot, connector or messaging extension card: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span></span>

> [!NOTE]
> <span data-ttu-id="776d1-224">ボットがディープリンクを含む TextBlock メッセージを送信すると、ユーザーがリンクを選択すると新しいブラウザタブが開きます。</span><span class="sxs-lookup"><span data-stu-id="776d1-224">When a bot sends a TextBlock message with a deep link, a new browser tab opens when users select the link.</span></span> <span data-ttu-id="776d1-225">これは、Chromeで発生し、Linux上で実行されているMicrosoft Teamsデスクトップアプリ。</span><span class="sxs-lookup"><span data-stu-id="776d1-225">This happens in Chrome and Microsoft Teams desktop app running on Linux.</span></span>
> <span data-ttu-id="776d1-226">ボットが同じディープ リンク URL を に送信した場合、 `Action.OpenUrl` ユーザーがリンクを選択すると、Teamsタブが現在のブラウザで開きます。</span><span class="sxs-lookup"><span data-stu-id="776d1-226">If the bot sends the same deep link URL into an `Action.OpenUrl`, the Teams tab opens in the current browser when the user selects the link.</span></span> <span data-ttu-id="776d1-227">新しいブラウザー タブは開きません。</span><span class="sxs-lookup"><span data-stu-id="776d1-227">No new browser tab is opened.</span></span>

<span data-ttu-id="776d1-228">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="776d1-228">The query parameters are:</span></span>

* <span data-ttu-id="776d1-229">`appID`: マニフェスト ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.</span><span class="sxs-lookup"><span data-stu-id="776d1-229">`appID`: Your manifest ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.</span></span>

* <span data-ttu-id="776d1-230">`entityID`:[タブを構成](~/tabs/how-to/create-tab-pages/configuration-page.md)するときに指定した項目 ID。たとえば、**タスクリスト123。**</span><span class="sxs-lookup"><span data-stu-id="776d1-230">`entityID`: The item ID that you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md). For example, **tasklist123**.</span></span>
* <span data-ttu-id="776d1-231">`entityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションのフィールド - https://tasklist.example.com/123 または https://tasklist.example.com/list123/task456 .</span><span class="sxs-lookup"><span data-stu-id="776d1-231">`entityWebUrl`: An optional field with a fallback URL to use if the client does not support rendering of the tab - https://tasklist.example.com/123 or https://tasklist.example.com/list123/task456.</span></span>
* <span data-ttu-id="776d1-232">`entityName`: 深いリンク、タスク リスト 123 またはタスク 456 を表示するときに使用するタブ内の項目のラベル。</span><span class="sxs-lookup"><span data-stu-id="776d1-232">`entityName`: A label for the item in your tab, to use when displaying the deep link, Task List 123 or Task 456.</span></span>

<span data-ttu-id="776d1-233">例: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span><span class="sxs-lookup"><span data-stu-id="776d1-233">Example: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span></span>

## <a name="deep-linking-to-the-scheduling-dialog"></a><span data-ttu-id="776d1-234">スケジュール設定ダイアログへのディープリンク</span><span class="sxs-lookup"><span data-stu-id="776d1-234">Deep linking to the scheduling dialog</span></span>

> [!NOTE]
> <span data-ttu-id="776d1-235">この機能は現在、開発者プレビュー段階です。</span><span class="sxs-lookup"><span data-stu-id="776d1-235">This feature is currently in developer preview.</span></span>

<span data-ttu-id="776d1-236">組み込みのスケジュール設定ダイアログTeamsへのディープリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-236">You can create deep links to the Teams built-in scheduling dialog.</span></span> <span data-ttu-id="776d1-237">これは、アプリがユーザーのカレンダーの完了や関連タスクのスケジュール設定を支援する場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="776d1-237">This is especially useful if your app helps the user complete calendar or scheduling related tasks.</span></span>

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="776d1-238">スケジュール設定ダイアログへのディープリンクを生成する</span><span class="sxs-lookup"><span data-stu-id="776d1-238">Generate a deep link to the scheduling dialog</span></span>

<span data-ttu-id="776d1-239">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。 `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="776d1-239">Use the following format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="776d1-240">例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="776d1-240">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="776d1-241">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="776d1-241">The query parameters are:</span></span>

* <span data-ttu-id="776d1-242">`attendees`: 会議の出席者を表すユーザー ID のコンマ区切りリスト (省略可能)。</span><span class="sxs-lookup"><span data-stu-id="776d1-242">`attendees`: The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="776d1-243">アクションを実行するユーザーは、会議の開催者です。</span><span class="sxs-lookup"><span data-stu-id="776d1-243">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="776d1-244">[ユーザー ID] フィールドは、現在 Azure AD ユーザー プリンシパル名 (通常は電子メール アドレス) のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="776d1-244">The User ID field currently only supports the Azure AD UserPrincipalName, typically an email address.</span></span>
* <span data-ttu-id="776d1-245">`startTime`: イベントの開始時刻 (省略可能)。</span><span class="sxs-lookup"><span data-stu-id="776d1-245">`startTime`: The optional start time of the event.</span></span> <span data-ttu-id="776d1-246">これは *、2018-03-12T23:55:25+02:00* など、[長いISO 8601形式](https://en.wikipedia.org/wiki/ISO_8601)でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="776d1-246">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example *2018-03-12T23:55:25+02:00*.</span></span>
* <span data-ttu-id="776d1-247">`endTime`: イベントの終了時刻 (ISO 8601 形式も含む)</span><span class="sxs-lookup"><span data-stu-id="776d1-247">`endTime`: The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="776d1-248">`subject`: 会議の件名のオプションフィールド。</span><span class="sxs-lookup"><span data-stu-id="776d1-248">`subject`: An optional field for the meeting subject.</span></span>
* <span data-ttu-id="776d1-249">`content`: 会議の詳細フィールドのオプション フィールド。</span><span class="sxs-lookup"><span data-stu-id="776d1-249">`content`: An optional field for the meeting details field.</span></span>

> [!NOTE]
> <span data-ttu-id="776d1-250">現在、場所の指定はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="776d1-250">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="776d1-251">UTC オフセットを指定する必要があり、開始時刻と終了時刻を生成するときにタイム ゾーンを意味します。</span><span class="sxs-lookup"><span data-stu-id="776d1-251">You must specify the UTC offset, it means time zones when generating your start and end times.</span></span>

<span data-ttu-id="776d1-252">ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。</span><span class="sxs-lookup"><span data-stu-id="776d1-252">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a><span data-ttu-id="776d1-253">オーディオ通話またはオーディオビデオ通話へのディープリンク</span><span class="sxs-lookup"><span data-stu-id="776d1-253">Deep linking to an audio or audio-video call</span></span>

<span data-ttu-id="776d1-254">ディープ リンクを作成して、オーディオまたは *AV* などのコールの種類と参加者を指定することで、1 人のユーザーまたはユーザーのグループに対してオーディオ *のみまたはオーディオ* ビデオ通話を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="776d1-254">You can create deep links to invoke audio only or audio-video calls to a single user or a group of users, by specifying the call type, as *audio* or *av*, and the participants.</span></span> <span data-ttu-id="776d1-255">ディープ リンクが呼び出された後、呼び出しを行う前に、デスクトップ クライアントTeams呼び出しを行う確認を求めるプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="776d1-255">After the deep link is invoked and before placing the call, Teams desktop client prompts a confirmation to make the call.</span></span> <span data-ttu-id="776d1-256">グループコールの場合、同じディープリンク呼び出しで一連の VoIP ユーザと PSTN ユーザのセットを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="776d1-256">In case of group call, you can call a set of VoIP users and a set of PSTN users in the same deeplink invocation.</span></span> 

<span data-ttu-id="776d1-257">ビデオ通話の場合、クライアントは確認を求め、発信者のビデオをオンにします。</span><span class="sxs-lookup"><span data-stu-id="776d1-257">In case of a video call, the client will ask for confirmation and turn on the caller's video for the call.</span></span> <span data-ttu-id="776d1-258">通話の受信者は、Teams呼び出し通知ウィンドウを介して、オーディオのみまたはオーディオとビデオを介して応答する選択肢があります。</span><span class="sxs-lookup"><span data-stu-id="776d1-258">The receiver of the call has a choice to respond through audio only or audio and video, through the Teams call notification window.</span></span>

> [!NOTE]
> <span data-ttu-id="776d1-259">このディープリンクは、会議の呼び出しには使用できません。</span><span class="sxs-lookup"><span data-stu-id="776d1-259">This deeplink cannot be used for invoking a meeting.</span></span>

### <a name="generate-a-deep-link-to-a-call"></a><span data-ttu-id="776d1-260">通話へのディープ リンクを生成する</span><span class="sxs-lookup"><span data-stu-id="776d1-260">Generate a deep link to a call</span></span>

| <span data-ttu-id="776d1-261">ディープリンク</span><span class="sxs-lookup"><span data-stu-id="776d1-261">Deep link</span></span> | <span data-ttu-id="776d1-262">Format</span><span class="sxs-lookup"><span data-stu-id="776d1-262">Format</span></span> | <span data-ttu-id="776d1-263">例</span><span class="sxs-lookup"><span data-stu-id="776d1-263">Example</span></span> |
|-----------|--------|---------|
| <span data-ttu-id="776d1-264">音声通話を発信する</span><span class="sxs-lookup"><span data-stu-id="776d1-264">Make an audio call</span></span> | <span data-ttu-id="776d1-265"> https://teams.microsoft.com/l/call/0/0?users=&lt;ユーザー 1 &gt; , &lt; ユーザー2&gt;</span><span class="sxs-lookup"><span data-stu-id="776d1-265">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| <span data-ttu-id="776d1-266">音声通話とビデオ通話を行う</span><span class="sxs-lookup"><span data-stu-id="776d1-266">Make an audio and video call</span></span> | <span data-ttu-id="776d1-267"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; ユーザー2 &gt;&ビデオ=true</span><span class="sxs-lookup"><span data-stu-id="776d1-267">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;&withvideo=true</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|<span data-ttu-id="776d1-268">オプションのパラメータソースを使用して音声通話とビデオ通話を行う</span><span class="sxs-lookup"><span data-stu-id="776d1-268">Make an audio and video call with an optional parameter source</span></span> | <span data-ttu-id="776d1-269"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; ユーザー2 &gt;&ビデオ=真の&ソース=デモアプリ</span><span class="sxs-lookup"><span data-stu-id="776d1-269">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;&withvideo=true&source=demoApp</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| <span data-ttu-id="776d1-270">VoIP と PSTN ユーザーの組み合わせに音声通話とビデオ通話を行う</span><span class="sxs-lookup"><span data-stu-id="776d1-270">Make an audio and video call to a combination of VoIP and PSTN users</span></span> | <span data-ttu-id="776d1-271"> https://teams.microsoft.com/l/call/0/0?users=&lt;ユーザー &gt; 1,4: &lt; 電話番号&gt;</span><span class="sxs-lookup"><span data-stu-id="776d1-271">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,4:&lt;phonenumber&gt;</span></span> | <span data-ttu-id="776d1-272"> https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210</span><span class="sxs-lookup"><span data-stu-id="776d1-272">https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210</span></span> |
  
<span data-ttu-id="776d1-273">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="776d1-273">Following are the query parameters:</span></span>
* <span data-ttu-id="776d1-274">`users`: コールの参加者を表すユーザー ID のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="776d1-274">`users`: The comma-separated list of user IDs representing the participants of the call.</span></span> <span data-ttu-id="776d1-275">現在、ユーザー ID フィールドは、Azure AD ユーザー プリンシパル名 (通常は電子メール アドレス) をサポートしているか、PSTN 呼び出しの場合は pstn mri 4: &lt; 電話番号 &gt; をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="776d1-275">Currently, the User ID field supports the Azure AD UserPrincipalName, typically an email address, or in case of a PSTN call, it supports a pstn mri 4:&lt;phonenumber&gt;.</span></span>
* <span data-ttu-id="776d1-276">`Withvideo`: これはオプションのパラメータで、ビデオコールを行うために使用できます。</span><span class="sxs-lookup"><span data-stu-id="776d1-276">`Withvideo`: This is an optional parameter, which you can use to make a video call.</span></span> <span data-ttu-id="776d1-277">このパラメータを設定すると、呼び出し元のカメラだけがオンになります。</span><span class="sxs-lookup"><span data-stu-id="776d1-277">Setting this parameter will only turn on the caller's camera.</span></span> <span data-ttu-id="776d1-278">通話の受信者は、Teams呼び出し通知ウィンドウを介して音声または音声とビデオ通話を通じて応答する選択肢があります。</span><span class="sxs-lookup"><span data-stu-id="776d1-278">The receiver of the call has a choice to answer through audio or audio and video call through the Teams call notification window.</span></span> 
* <span data-ttu-id="776d1-279">`Source`: これは、ディープリンクのソースを知らせるオプションのパラメータです。</span><span class="sxs-lookup"><span data-stu-id="776d1-279">`Source`: This is an optional parameter, which informs about the source of the deeplink.</span></span>

## <a name="code-sample"></a><span data-ttu-id="776d1-280">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="776d1-280">Code sample</span></span>

| <span data-ttu-id="776d1-281">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="776d1-281">Sample name</span></span> | <span data-ttu-id="776d1-282">説明</span><span class="sxs-lookup"><span data-stu-id="776d1-282">Description</span></span> | <span data-ttu-id="776d1-283">C#</span><span class="sxs-lookup"><span data-stu-id="776d1-283">C#</span></span> |<span data-ttu-id="776d1-284">Node.js</span><span class="sxs-lookup"><span data-stu-id="776d1-284">Node.js</span></span>|
|-------------|-------------|------|----|
|<span data-ttu-id="776d1-285">深いリンク使用サブエンティティ ID</span><span class="sxs-lookup"><span data-stu-id="776d1-285">Deep Link consuming Subentity ID</span></span>  |<span data-ttu-id="776d1-286">Microsoft Teamsサンプル アプリで、ボット チャットからサブエンティティ ID を使用するタブへのディープリンクをデモンストレーションします。</span><span class="sxs-lookup"><span data-stu-id="776d1-286">Microsoft Teams sample app for demonstrating deeplink from bot chat to tab consuming Subentity ID.</span></span>|[<span data-ttu-id="776d1-287">View</span><span class="sxs-lookup"><span data-stu-id="776d1-287">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[<span data-ttu-id="776d1-288">View</span><span class="sxs-lookup"><span data-stu-id="776d1-288">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a><span data-ttu-id="776d1-289">関連項目</span><span class="sxs-lookup"><span data-stu-id="776d1-289">See also</span></span>

[<span data-ttu-id="776d1-290">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="776d1-290">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

