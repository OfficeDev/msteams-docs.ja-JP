---
title: ディープ リンクの作成
description: ディープ リンクとアプリでの使用方法について説明する
ms.topic: how-to
localization_priority: Normal
keywords: Teams ディープ リンク ディープリンク
ms.openlocfilehash: ccad5c6cc8daa513b12185efa2ed57e02438fd89
ms.sourcegitcommit: 20e623a82f9676dd036cf6a350dd480885e0ea2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2021
ms.locfileid: "52300557"
---
# <a name="create-deep-links"></a><span data-ttu-id="94a31-104">ディープ リンクの作成</span><span class="sxs-lookup"><span data-stu-id="94a31-104">Create deep links</span></span> 

<span data-ttu-id="94a31-105">情報と機能へのリンクは、Teams。</span><span class="sxs-lookup"><span data-stu-id="94a31-105">You can create links to information and features within Teams.</span></span> <span data-ttu-id="94a31-106">ディープ リンクの作成が役立つシナリオは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-106">The scenarios where creating deep links are useful are as follows:</span></span>

* <span data-ttu-id="94a31-107">アプリのいずれかのタブ内のコンテンツにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-107">Navigating the user to the content within one of your app's tabs.</span></span> <span data-ttu-id="94a31-108">たとえば、アプリには、重要なアクティビティをユーザーに通知するメッセージを送信するボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-108">For instance, your app can have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="94a31-109">ユーザーが通知をタップすると、深いリンクがタブに移動し、ユーザーがアクティビティの詳細を表示できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-109">When the user taps on the notification, the deep link navigates to the tab so that the user can view more details about the activity.</span></span>
* <span data-ttu-id="94a31-110">アプリは、必要なパラメーターを含むディープ リンクを事前に設定することで、チャットの作成や会議のスケジュール設定など、特定のユーザー タスクを自動化または簡素化します。</span><span class="sxs-lookup"><span data-stu-id="94a31-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre populating the deep links with required parameters.</span></span> <span data-ttu-id="94a31-111">これにより、ユーザーが手動で情報を入力する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="94a31-111">This avoids the need for users to manually enter information.</span></span>

> [!NOTE]
>
> <span data-ttu-id="94a31-112">ディープリンクは、コンテンツに移動する前にブラウザーを最初に起動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-112">A deeplink launches the browser first before navigating to content.</span></span> <span data-ttu-id="94a31-113">エンティティ上のディープ リンクTeamsは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-113">The behaviour of deep links on Teams entities are as follows:</span></span>
>
> <span data-ttu-id="94a31-114">**タブ**:</span><span class="sxs-lookup"><span data-stu-id="94a31-114">**Tab**:</span></span>  
> <span data-ttu-id="94a31-115">✔ ディープリンクの URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-115">✔ Directly navigates to the deeplink url.</span></span>
>
> <span data-ttu-id="94a31-116">**ボット**:</span><span class="sxs-lookup"><span data-stu-id="94a31-116">**Bot**:</span></span>  
> <span data-ttu-id="94a31-117">✔本文の Deeplink: ブラウザーで最初に開きます。</span><span class="sxs-lookup"><span data-stu-id="94a31-117">✔ Deeplink in card body: Opens in browser first.</span></span>  
> <span data-ttu-id="94a31-118">✔カードの OpenURL アクションに Deeplink を追加: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-118">✔ Deeplink added to OpenURL action in Adaptive Card: Directly navigates to the deeplink url.</span></span>  
> <span data-ttu-id="94a31-119">✔の [ハイパーリンク] マークダウン テキスト: ブラウザーで最初に開きます。</span><span class="sxs-lookup"><span data-stu-id="94a31-119">✔ Hyperlink markdown text in the card: Opens in browser first.</span></span>  
>
> <span data-ttu-id="94a31-120">**チャット**</span><span class="sxs-lookup"><span data-stu-id="94a31-120">**Chat**:</span></span>  
> <span data-ttu-id="94a31-121">✔ メッセージのハイパーリンク マークダウン: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-121">✔ Text message hyperlink markdown: Directly navigates to deeplink url.</span></span>  
> <span data-ttu-id="94a31-122">✔チャット会話で貼り付けリンク: ディープリンク URL に直接移動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-122">✔ Link pasted in general chat conversation: Directly navigates to deeplink url.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="94a31-123">タブへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="94a31-123">Deep linking to your tab</span></span>

<span data-ttu-id="94a31-124">Teams のエンティティへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="94a31-125">これは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスク リストが含まれている場合、チーム メンバーは個々のタスクへのリンクを作成して共有できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-125">This is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list, team members can create and share links to individual tasks.</span></span> <span data-ttu-id="94a31-126">リンクを選択すると、特定のアイテムに焦点を当てたタブに移動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-126">When you select the link, it navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="94a31-127">これを実装するには、UI に最も適した方法で、各アイテムにコピー リンク アクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="94a31-127">To implement this, you add a **copy link** action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="94a31-128">このアクションを実行すると、 `shareDeepLink()` を呼び出して、ユーザーがクリップボードにコピーできるリンクを含むダイアログボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="94a31-128">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="94a31-129">この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクに従って、タブを再読み込みするとき、[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。</span><span class="sxs-lookup"><span data-stu-id="94a31-129">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="94a31-130">または、このトピックで後述する形式を使用して、プログラミングして、ディープ リンクを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="94a31-130">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="94a31-131">ボットおよびコネクタ メッセージ内のディープ [リンク](~/bots/what-are-bots.md) を [使用](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) すると、タブの変更、またはタブ内のアイテムに関する情報をユーザーに通知できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-131">You can use deep links in [bot](~/bots/what-are-bots.md) and [connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="94a31-132">このディープ リンクは、[タブ へのコピー]リンクによって提供されるリンクとは異なります。これは、このタブをポイントするディープ リンクを生成するだけです。</span><span class="sxs-lookup"><span data-stu-id="94a31-132">This deep link is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

>[!NOTE]
> <span data-ttu-id="94a31-133">現在、shareDeepLinkは、モバイル プラットフォームでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="94a31-133">Currently, shareDeepLink does not work on mobile platforms.</span></span>

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="94a31-134">タブ内のアイテムへの深いリンクを表示する</span><span class="sxs-lookup"><span data-stu-id="94a31-134">Show a deep link to an item within your tab</span></span>

<span data-ttu-id="94a31-135">タブ内のアイテムへのディープ リンクを含むダイアログ ボックスを表示するには、`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` を呼び出します</span><span class="sxs-lookup"><span data-stu-id="94a31-135">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span></span>

<span data-ttu-id="94a31-136">次のフィールドを指定します。</span><span class="sxs-lookup"><span data-stu-id="94a31-136">Provide the following fields:</span></span>

* <span data-ttu-id="94a31-137">`subEntityId`: ディープ リンク先のタブ内のアイテムの一意の識別子です。</span><span class="sxs-lookup"><span data-stu-id="94a31-137">`subEntityId`: A unique identifier for the item within your tab to which you are deep linking.</span></span>
* <span data-ttu-id="94a31-138">`subEntityLabel`: ディープ リンクの表示に使用するアイテムのラベル。</span><span class="sxs-lookup"><span data-stu-id="94a31-138">`subEntityLabel`: A label for the item to use for displaying the deep link.</span></span>
* <span data-ttu-id="94a31-139">`subEntityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。</span><span class="sxs-lookup"><span data-stu-id="94a31-139">`subEntityWebUrl`: An optional field with a fallback URL to use if the client does not support rendering the tab.</span></span>

### <a name="generate-a-deep-link-to-your-tab"></a><span data-ttu-id="94a31-140">タブへのディープ リンクを生成する</span><span class="sxs-lookup"><span data-stu-id="94a31-140">Generate a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="94a31-141">個人用タブにはスコープ `personal` が含まれていますが、チャネルタブとグループ タブはスコープ `team` を `group` 使用します。</span><span class="sxs-lookup"><span data-stu-id="94a31-141">Personal tabs have a `personal` scope, while channel and group tabs use `team` or `group` scopes.</span></span> <span data-ttu-id="94a31-142">構成可能なタブだけがコンテキスト オブジェクトに関連付けられている `channel` プロパティを持つため、2 つのタブの種類の構文はわずかに異なります。</span><span class="sxs-lookup"><span data-stu-id="94a31-142">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="94a31-143">タブ スコープ [の詳細](~/resources/schema/manifest-schema.md) については、マニフェスト リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="94a31-143">See the [manifest](~/resources/schema/manifest-schema.md) reference for more information on tab scopes.</span></span>

> [!NOTE]
> <span data-ttu-id="94a31-144">ディープ リンクは、タブが v0.4 以降のライブラリを使用して構成されていて、そのためエンティティ ID がある場合にのみ正常に機能します。</span><span class="sxs-lookup"><span data-stu-id="94a31-144">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="94a31-145">エンティティ ID のないタブへのディープ リンクは、タブに移動しますが、サブエンティティ ID をタブに提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="94a31-145">Deep links to tabs without entity IDs still navigate to the tab but cannot provide the sub entity ID to the tab.</span></span>

<span data-ttu-id="94a31-146">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="94a31-146">Use the following format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> <span data-ttu-id="94a31-147">ボットがディープ リンクを使用して `TextBlock` を含むメッセージを送信する場合、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="94a31-147">If the bot sends a message containing a `TextBlock` with a deep link, then a new browser tab is opened when the user selects the link.</span></span> <span data-ttu-id="94a31-148">これは、Chrome および Microsoft Teams デスクトップ アプリ (いずれも Linux で実行されています) で発生します。</span><span class="sxs-lookup"><span data-stu-id="94a31-148">This happens in Chrome and in the Microsoft Teams desktop app, both running on Linux.</span></span>
> <span data-ttu-id="94a31-149">ボットが同じディープ リンク URL を a に送信すると、ユーザーがリンクを選択すると、現在Teamsタブで [詳細リンク] タブ `Action.OpenUrl` が開きます。</span><span class="sxs-lookup"><span data-stu-id="94a31-149">If the bot sends the same deep link URL into an `Action.OpenUrl`, then the Teams tab is opened in the current browser tab when the user selects the link.</span></span> <span data-ttu-id="94a31-150">新しいブラウザー タブが開かれません。</span><span class="sxs-lookup"><span data-stu-id="94a31-150">A new browser tab is not opened.</span></span>

<span data-ttu-id="94a31-151">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-151">The query parameters are:</span></span>

| <span data-ttu-id="94a31-152">パラメーター名</span><span class="sxs-lookup"><span data-stu-id="94a31-152">Parameter name</span></span> | <span data-ttu-id="94a31-153">説明</span><span class="sxs-lookup"><span data-stu-id="94a31-153">Description</span></span> | <span data-ttu-id="94a31-154">例</span><span class="sxs-lookup"><span data-stu-id="94a31-154">Example</span></span> |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | <span data-ttu-id="94a31-155">マニフェストの ID。</span><span class="sxs-lookup"><span data-stu-id="94a31-155">The ID from your manifest.</span></span> |<span data-ttu-id="94a31-156">fe4a8eba-2a31-4737-8e33-e5fae6fee194</span><span class="sxs-lookup"><span data-stu-id="94a31-156">fe4a8eba-2a31-4737-8e33-e5fae6fee194</span></span>|
| `entityId`&emsp; | <span data-ttu-id="94a31-157">タブの構成時に指定したタブ内のアイテムの [ID](~/tabs/how-to/create-tab-pages/configuration-page.md)です。</span><span class="sxs-lookup"><span data-stu-id="94a31-157">The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>|<span data-ttu-id="94a31-158">Tasklist123</span><span class="sxs-lookup"><span data-stu-id="94a31-158">Tasklist123</span></span>|
| <span data-ttu-id="94a31-159">`entityWebUrl` または `subEntityWebUrl`&emsp;</span><span class="sxs-lookup"><span data-stu-id="94a31-159">`entityWebUrl` or `subEntityWebUrl`&emsp;</span></span> | <span data-ttu-id="94a31-160">クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド。</span><span class="sxs-lookup"><span data-stu-id="94a31-160">An optional field with a fallback URL to use if the client does not support rendering the tab.</span></span> | <span data-ttu-id="94a31-161"> https://tasklist.example.com/123 または https://tasklist.example.com/list123/task456</span><span class="sxs-lookup"><span data-stu-id="94a31-161">https://tasklist.example.com/123 or https://tasklist.example.com/list123/task456</span></span> |
| <span data-ttu-id="94a31-162">`entityLabel` または `subEntityLabel`&emsp;</span><span class="sxs-lookup"><span data-stu-id="94a31-162">`entityLabel` or `subEntityLabel`&emsp;</span></span> | <span data-ttu-id="94a31-163">ディープ リンクを表示するときに使用するタブ内のアイテムのラベル。</span><span class="sxs-lookup"><span data-stu-id="94a31-163">A label for the item in your tab, to use when displaying the deep link.</span></span> | <span data-ttu-id="94a31-164">タスク リスト 123 または "タスク 456"</span><span class="sxs-lookup"><span data-stu-id="94a31-164">Task List 123 or "Task 456</span></span> |
| <span data-ttu-id="94a31-165">`context`&emsp;</span><span class="sxs-lookup"><span data-stu-id="94a31-165">`context`&emsp;</span></span> </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| <span data-ttu-id="94a31-166">次のフィールドを含む JSON オブジェクト</span><span class="sxs-lookup"><span data-stu-id="94a31-166">A JSON object containing the following fields</span></span></br></br> <span data-ttu-id="94a31-167">\* タブ内のアイテムの ID。</span><span class="sxs-lookup"><span data-stu-id="94a31-167">\* An ID for the item within the tab.</span></span> </br></br> <span data-ttu-id="94a31-168">\* タブ コンテキストMicrosoft Teams利用可能なチャネル ID を指定[します](~/tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="94a31-168">\*  The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md).</span></span> | 
| `subEntityId`&emsp; | <span data-ttu-id="94a31-169">タブ内のアイテムの ID。</span><span class="sxs-lookup"><span data-stu-id="94a31-169">An ID for the item within the tab.</span></span> |<span data-ttu-id="94a31-170">Task456</span><span class="sxs-lookup"><span data-stu-id="94a31-170">Task456</span></span> |
| `channelId`&emsp; | <span data-ttu-id="94a31-171">タブ Microsoft Teamsから使用できるチャネル ID を指定[します](~/tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="94a31-171">The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="94a31-172">このプロパティは、チームのスコープを持つ構成可能なタブでのみ使用 **できます**。</span><span class="sxs-lookup"><span data-stu-id="94a31-172">This property is only available in configurable tabs with a scope of **team**.</span></span> <span data-ttu-id="94a31-173">これは、個人用の範囲を持つ静的タブでは使用 **できません**。</span><span class="sxs-lookup"><span data-stu-id="94a31-173">It is not available in static tabs, which have a scope of **personal**.</span></span>| <span data-ttu-id="94a31-174">19:cbe3683f25094106b826c9cada3afbe0@thread.skype</span><span class="sxs-lookup"><span data-stu-id="94a31-174">19:cbe3683f25094106b826c9cada3afbe0@thread.skype</span></span> |

<span data-ttu-id="94a31-175">例:</span><span class="sxs-lookup"><span data-stu-id="94a31-175">Examples:</span></span>

* <span data-ttu-id="94a31-176">構成可能なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="94a31-176">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="94a31-177">構成可能なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="94a31-177">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="94a31-178">静的なタブ自体へのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="94a31-178">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="94a31-179">静的なタブ内のタスク アイテムへのリンク: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="94a31-179">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94a31-180">すべてのクエリ パラメーターが適切に URI にエンコードされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="94a31-180">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="94a31-181">最後の例を使用して、前の例に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="94a31-181">You must follow the preceeding examples using the last example:</span></span>

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a><span data-ttu-id="94a31-182">タブからディープ リンクを使用する</span><span class="sxs-lookup"><span data-stu-id="94a31-182">Consume a deep link from a tab</span></span>

<span data-ttu-id="94a31-183">ディープ リンクに移動すると、Microsoft Teams はタブに移動し、Microsoft Teams JavaScript ライブラリを介してサブエンティティ ID が存在する場合に取得するメカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="94a31-183">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism through the Microsoft Teams JavaScript library to retrieve the sub-entity ID if it exists.</span></span>

<span data-ttu-id="94a31-184">この呼び出しは、タブがディープ リンクを介して移動される場合、フィールドを含 [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) `subEntityId` むコンテキストを返します。</span><span class="sxs-lookup"><span data-stu-id="94a31-184">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab is navigated through a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="94a31-185">タブからのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="94a31-185">Deep linking from your tab</span></span>

<span data-ttu-id="94a31-186">タブから、Teamsにディープリンクできます。これは、タブがチャネル、メッセージ、別のタブ、スケジュール 設定ダイアログを開くなど、Teams 内の他のコンテンツにリンクする必要がある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="94a31-186">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams, such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="94a31-187">タブからディープリンクをトリガーするには、次のように呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="94a31-187">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="94a31-188">この呼び出しでは、正しい URL に移動したり、スケジュール設定やアプリのインストール ダイアログを開くなどのクライアント アクションをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="94a31-188">This call navigates you to the correct URL, or trigger a client action, such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="94a31-189">次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94a31-189">See the following example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="94a31-190">チャットへのディープ リンクの設定</span><span class="sxs-lookup"><span data-stu-id="94a31-190">Deep linking to a chat</span></span>

<span data-ttu-id="94a31-191">参加者のセットを指定することで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-191">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="94a31-192">指定した参加者とチャットが存在しない場合、リンクは空の新しいチャットにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="94a31-192">If a chat does not exist with the specified participants, the link navigates the user to an empty new chat.</span></span> <span data-ttu-id="94a31-193">ユーザーが最初のメッセージを送信するまで、新しいチャットが下書き状態で作成されます。</span><span class="sxs-lookup"><span data-stu-id="94a31-193">New chats are  created in draft state until the user sends the first message.</span></span> <span data-ttu-id="94a31-194">それ以外の場合は、チャットが存在しない場合は、ユーザーの作成ボックスに挿入するテキストと共に、チャットの名前を指定できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-194">Otherwise, you can specify the name of the chat if it does not already exist, along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="94a31-195">この機能は、ユーザーがチャットに移動したり、チャットを参加したり、メッセージを入力したりする手動操作を行うためのショートカットとして考えることができます。</span><span class="sxs-lookup"><span data-stu-id="94a31-195">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="94a31-196">ユースケースの例として、ボットから Office 365 ユーザー プロファイルをカードとして返す場合、このディープ リンクを使用すると、ユーザーはそのユーザーと簡単にチャットできます。</span><span class="sxs-lookup"><span data-stu-id="94a31-196">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generate-a-deep-link-to-a-chat"></a><span data-ttu-id="94a31-197">チャットへのディープ リンクを生成する</span><span class="sxs-lookup"><span data-stu-id="94a31-197">Generate a deep link to a chat</span></span>

<span data-ttu-id="94a31-198">ボット、コネクタ、またはメッセージング拡張機能カードで使用できるディープ リンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="94a31-198">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="94a31-199">例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="94a31-199">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="94a31-200">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-200">The query parameters are:</span></span>

* <span data-ttu-id="94a31-201">`users`: チャットの参加者を表すユーザー ID のコンマ区切りリストです。</span><span class="sxs-lookup"><span data-stu-id="94a31-201">`users`: The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="94a31-202">アクションを実行するユーザーは、常に参加者として含まれます。</span><span class="sxs-lookup"><span data-stu-id="94a31-202">The user that performs the action is always included as a participant.</span></span> <span data-ttu-id="94a31-203">現在、User ID フィールドは、電子メール アドレスADなど、UserPrincipalName の Azure ADをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="94a31-203">Currently, the User ID field supports the Azure AD UserPrincipalName, such as an email address only.</span></span>
* <span data-ttu-id="94a31-204">`topicName`: 3 人以上のユーザーとのチャットの場合、チャットの表示名のオプション フィールド。</span><span class="sxs-lookup"><span data-stu-id="94a31-204">`topicName`: An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="94a31-205">このフィールドを指定しない場合、チャットの表示名は参加者の名前に基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="94a31-205">If this field is not specified, the chat's display name is based on the names of the participants.</span></span>
* <span data-ttu-id="94a31-206">`message`: チャットが下書き状態の間に現在のユーザーの作成ボックスに挿入するメッセージ テキストのオプション フィールド。</span><span class="sxs-lookup"><span data-stu-id="94a31-206">`message`: An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="94a31-207">ボットでこのディープ リンクを使用するには、これをカードのボタンの URL ターゲットとして指定するか、アクションの種類を使用してアクションを `openUrl` タップします。</span><span class="sxs-lookup"><span data-stu-id="94a31-207">To use this deep link with your bot, specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="generate-deep-links-to-file-in-channel"></a><span data-ttu-id="94a31-208">チャネル内のファイルへのディープ リンクを生成する</span><span class="sxs-lookup"><span data-stu-id="94a31-208">Generate deep links to file in channel</span></span>

<span data-ttu-id="94a31-209">ボット、コネクタ、またはメッセージング拡張機能カードでは、次のディープ リンク形式を使用できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-209">The following deep link format can be used in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

<span data-ttu-id="94a31-210">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-210">The query parameters are:</span></span>

* <span data-ttu-id="94a31-211">`tenantId`: テナント ID の例、0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span><span class="sxs-lookup"><span data-stu-id="94a31-211">`tenantId`: Tenant ID example, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span></span>
* <span data-ttu-id="94a31-212">`fileType`: docx、pptx、xlsx、pdf などのサポートされているファイルの種類</span><span class="sxs-lookup"><span data-stu-id="94a31-212">`fileType`: Supported file type, such as docx, pptx, xlsx, and pdf</span></span>
* <span data-ttu-id="94a31-213">`objectUrl`: ファイルのオブジェクト URL、 https://microsoft.sharepoint.com/teams/(filepath)</span><span class="sxs-lookup"><span data-stu-id="94a31-213">`objectUrl`: Object URL of the file, https://microsoft.sharepoint.com/teams/(filepath)</span></span>
* <span data-ttu-id="94a31-214">`baseUrl`: ファイルの基本 URL、 https://microsoft.sharepoint.com/teams</span><span class="sxs-lookup"><span data-stu-id="94a31-214">`baseUrl`: Base URL of the file, https://microsoft.sharepoint.com/teams</span></span>
* <span data-ttu-id="94a31-215">`serviceName`: サービスの名前、アプリ ID</span><span class="sxs-lookup"><span data-stu-id="94a31-215">`serviceName`: Name of the service, app ID</span></span>
* <span data-ttu-id="94a31-216">`threadId`: threadId は、ファイルが保存されているチームのチーム ID です。</span><span class="sxs-lookup"><span data-stu-id="94a31-216">`threadId`: The threadId is the team ID of the team where the file is stored.</span></span> <span data-ttu-id="94a31-217">これはオプションで、ユーザーのフォルダーに保存されているファイルに対してOneDriveできません。</span><span class="sxs-lookup"><span data-stu-id="94a31-217">It is optional and cannot be set for files stored in a user's OneDrive folder.</span></span> <span data-ttu-id="94a31-218">threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span><span class="sxs-lookup"><span data-stu-id="94a31-218">threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span></span>
* <span data-ttu-id="94a31-219">`groupId`: ファイルのグループ ID ae063b79-5315-4ddb-ba70-27328ba6c31e</span><span class="sxs-lookup"><span data-stu-id="94a31-219">`groupId`: Group ID of the file, ae063b79-5315-4ddb-ba70-27328ba6c31e</span></span>

<span data-ttu-id="94a31-220">ファイルへのディープリンクのサンプル形式を次に示します。</span><span class="sxs-lookup"><span data-stu-id="94a31-220">Following is the sample format of deeplink to files:</span></span>

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a><span data-ttu-id="94a31-221">このオブジェクトのシリアル化:</span><span class="sxs-lookup"><span data-stu-id="94a31-221">Serialization of this object:</span></span>
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
## <a name="deep-linking-for-sharepoint-framework-tabs"></a><span data-ttu-id="94a31-222">タブの詳細SharePoint Frameworkリンク</span><span class="sxs-lookup"><span data-stu-id="94a31-222">Deep linking for SharePoint Framework tabs</span></span>

<span data-ttu-id="94a31-223">ボット、コネクタ、またはメッセージング拡張カードでは、次のディープ リンク形式を使用できます。 `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span><span class="sxs-lookup"><span data-stu-id="94a31-223">The following deep link format can be used in a bot, connector or messaging extension card: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span></span>

> [!NOTE]
> <span data-ttu-id="94a31-224">ボットがディープ リンクを含む TextBlock メッセージを送信すると、ユーザーがリンクを選択すると、新しいブラウザー タブが開きます。</span><span class="sxs-lookup"><span data-stu-id="94a31-224">When a bot sends a TextBlock message with a deep link, a new browser tab opens when users select the link.</span></span> <span data-ttu-id="94a31-225">これは、Chrome および Linux でMicrosoft Teamsデスクトップ アプリで発生します。</span><span class="sxs-lookup"><span data-stu-id="94a31-225">This happens in Chrome and Microsoft Teams desktop app running on Linux.</span></span>
> <span data-ttu-id="94a31-226">ボットが同じディープ リンク URL を a に送信すると、ユーザーがリンクを選択すると、Teamsタブが現在のブラウザー `Action.OpenUrl` で開きます。</span><span class="sxs-lookup"><span data-stu-id="94a31-226">If the bot sends the same deep link URL into an `Action.OpenUrl`, the Teams tab opens in the current browser when the user selects the link.</span></span> <span data-ttu-id="94a31-227">新しいブラウザー タブは開きません。</span><span class="sxs-lookup"><span data-stu-id="94a31-227">No new browser tab is opened.</span></span>

<span data-ttu-id="94a31-228">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-228">The query parameters are:</span></span>

* <span data-ttu-id="94a31-229">`appID`: マニフェスト ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.</span><span class="sxs-lookup"><span data-stu-id="94a31-229">`appID`: Your manifest ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.</span></span>

* <span data-ttu-id="94a31-230">`entityID`: タブの構成時に指定 [したアイテム ID](~/tabs/how-to/create-tab-pages/configuration-page.md)です。たとえば **、tasklist123**.</span><span class="sxs-lookup"><span data-stu-id="94a31-230">`entityID`: The item ID that you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md). For example, **tasklist123**.</span></span>
* <span data-ttu-id="94a31-231">`entityWebUrl`: クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションのフィールド https://tasklist.example.com/123 。 https://tasklist.example.com/list123/task456</span><span class="sxs-lookup"><span data-stu-id="94a31-231">`entityWebUrl`: An optional field with a fallback URL to use if the client does not support rendering of the tab - https://tasklist.example.com/123 or https://tasklist.example.com/list123/task456.</span></span>
* <span data-ttu-id="94a31-232">`entityName`: タブ内のアイテムのラベルで、ディープ リンクであるタスク リスト 123 またはタスク 456 を表示するときに使用します。</span><span class="sxs-lookup"><span data-stu-id="94a31-232">`entityName`: A label for the item in your tab, to use when displaying the deep link, Task List 123 or Task 456.</span></span>

<span data-ttu-id="94a31-233">例: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span><span class="sxs-lookup"><span data-stu-id="94a31-233">Example: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span></span>

## <a name="deep-linking-to-the-scheduling-dialog"></a><span data-ttu-id="94a31-234">[スケジュール] ダイアログへのディープ リンク</span><span class="sxs-lookup"><span data-stu-id="94a31-234">Deep linking to the scheduling dialog</span></span>

> [!NOTE]
> <span data-ttu-id="94a31-235">この機能は現在、開発者プレビュー段階です。</span><span class="sxs-lookup"><span data-stu-id="94a31-235">This feature is currently in developer preview.</span></span>

<span data-ttu-id="94a31-236">組み込みのスケジュール 設定ダイアログTeams深いリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-236">You can create deep links to the Teams built-in scheduling dialog.</span></span> <span data-ttu-id="94a31-237">これは、ユーザーが予定表を完了したり、関連するタスクをスケジュールしたりするのに役立つ場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="94a31-237">This is especially useful if your app helps the user complete calendar or scheduling related tasks.</span></span>

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="94a31-238">スケジュール ダイアログへの深いリンクを生成する</span><span class="sxs-lookup"><span data-stu-id="94a31-238">Generate a deep link to the scheduling dialog</span></span>

<span data-ttu-id="94a31-239">ボット、コネクタ、またはメッセージング拡張カードで使用できるディープ リンクには、次の形式を使用します。 `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="94a31-239">Use the following format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="94a31-240">例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="94a31-240">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="94a31-241">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-241">The query parameters are:</span></span>

* <span data-ttu-id="94a31-242">`attendees`: 会議の出席者を表すユーザー ID のオプションのコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="94a31-242">`attendees`: The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="94a31-243">アクションを実行するユーザーは、会議の開催者です。</span><span class="sxs-lookup"><span data-stu-id="94a31-243">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="94a31-244">[ユーザー ID] フィールドは現在、Azure AD UserPrincipalName (通常は電子メール アドレス) のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="94a31-244">The User ID field currently only supports the Azure AD UserPrincipalName, typically an email address.</span></span>
* <span data-ttu-id="94a31-245">`startTime`: イベントのオプションの開始時刻です。</span><span class="sxs-lookup"><span data-stu-id="94a31-245">`startTime`: The optional start time of the event.</span></span> <span data-ttu-id="94a31-246">これは *、2018-03-12T23:55:25+02:00* など、長い [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)形式である必要があります。</span><span class="sxs-lookup"><span data-stu-id="94a31-246">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example *2018-03-12T23:55:25+02:00*.</span></span>
* <span data-ttu-id="94a31-247">`endTime`: イベントのオプションの終了時刻 (ISO 8601 形式)。</span><span class="sxs-lookup"><span data-stu-id="94a31-247">`endTime`: The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="94a31-248">`subject`: 会議の件名の省略可能なフィールドです。</span><span class="sxs-lookup"><span data-stu-id="94a31-248">`subject`: An optional field for the meeting subject.</span></span>
* <span data-ttu-id="94a31-249">`content`: 会議の詳細フィールドのオプション フィールドです。</span><span class="sxs-lookup"><span data-stu-id="94a31-249">`content`: An optional field for the meeting details field.</span></span>

> [!NOTE]
> <span data-ttu-id="94a31-250">現在、場所の指定はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="94a31-250">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="94a31-251">UTC オフセットを指定する必要があります。開始時刻と終了時刻を生成するときにタイム ゾーンを意味します。</span><span class="sxs-lookup"><span data-stu-id="94a31-251">You must specify the UTC offset, it means time zones when generating your start and end times.</span></span>

<span data-ttu-id="94a31-252">ボットとのこのディープ リンクを使用するには、カードのボタンで URL を対象として指定するか、[ `openUrl` アクションの種類] で [アクション] をタップします。</span><span class="sxs-lookup"><span data-stu-id="94a31-252">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a><span data-ttu-id="94a31-253">音声通話または音声ビデオ通話へのディープ リンク</span><span class="sxs-lookup"><span data-stu-id="94a31-253">Deep linking to an audio or audio-video call</span></span>

<span data-ttu-id="94a31-254">音声または *av* として、通話の種類と参加者を指定することで、1 人のユーザーまたはユーザーのグループに対して音声のみまたはオーディオ ビデオ通話を呼び出すディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-254">You can create deep links to invoke audio only or audio-video calls to a single user or a group of users, by specifying the call type, as *audio* or *av*, and the participants.</span></span> <span data-ttu-id="94a31-255">ディープ リンクが呼び出された後、呼び出しを行う前にTeamsデスクトップ クライアントから通話の確認を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="94a31-255">After the deep link is invoked and before placing the call, Teams desktop client prompts a confirmation to make the call.</span></span> <span data-ttu-id="94a31-256">グループ呼び出しの場合は、同じディープリンク呼び出しで VoIP ユーザーのセットと PSTN ユーザーのセットを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="94a31-256">In case of group call, you can call a set of VoIP users and a set of PSTN users in the same deeplink invocation.</span></span> 

<span data-ttu-id="94a31-257">ビデオ通話の場合、クライアントは確認を求め、通話のために発信者のビデオをオンにします。</span><span class="sxs-lookup"><span data-stu-id="94a31-257">In case of a video call, the client will ask for confirmation and turn on the caller's video for the call.</span></span> <span data-ttu-id="94a31-258">通話の受信者は、音声のみまたは音声とビデオを通じて、通話通知ウィンドウで応答Teams選択できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-258">The receiver of the call has a choice to respond through audio only or audio and video, through the Teams call notification window.</span></span>

> [!NOTE]
> <span data-ttu-id="94a31-259">このディープリンクは、会議の呼び出しには使用できません。</span><span class="sxs-lookup"><span data-stu-id="94a31-259">This deeplink cannot be used for invoking a meeting.</span></span>

### <a name="generate-a-deep-link-to-a-chat"></a><span data-ttu-id="94a31-260">チャットへのディープ リンクを生成する</span><span class="sxs-lookup"><span data-stu-id="94a31-260">Generate a deep link to a chat</span></span>

| <span data-ttu-id="94a31-261">ディープ リンク</span><span class="sxs-lookup"><span data-stu-id="94a31-261">Deep link</span></span> | <span data-ttu-id="94a31-262">Format</span><span class="sxs-lookup"><span data-stu-id="94a31-262">Format</span></span> | <span data-ttu-id="94a31-263">例</span><span class="sxs-lookup"><span data-stu-id="94a31-263">Example</span></span> |
|-----------|--------|---------|
| <span data-ttu-id="94a31-264">音声通話を行う</span><span class="sxs-lookup"><span data-stu-id="94a31-264">Make an audio call</span></span> | <span data-ttu-id="94a31-265"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; 、 &lt; user2&gt;</span><span class="sxs-lookup"><span data-stu-id="94a31-265">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| <span data-ttu-id="94a31-266">音声およびビデオ通話を行う</span><span class="sxs-lookup"><span data-stu-id="94a31-266">Make an audio and video call</span></span> | <span data-ttu-id="94a31-267"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; 、 &lt; user2&video=true &gt;</span><span class="sxs-lookup"><span data-stu-id="94a31-267">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;&withvideo=true</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|<span data-ttu-id="94a31-268">オプションのパラメーター ソースを使用して音声およびビデオ通話を行う</span><span class="sxs-lookup"><span data-stu-id="94a31-268">Make an audio and video call with an optional parameter source</span></span> | <span data-ttu-id="94a31-269"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; , &lt; user2&&gt; withvideo=true&source=demoApp</span><span class="sxs-lookup"><span data-stu-id="94a31-269">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;&withvideo=true&source=demoApp</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| <span data-ttu-id="94a31-270">VoIP ユーザーと PSTN ユーザーの組み合わせに音声およびビデオ通話を行う</span><span class="sxs-lookup"><span data-stu-id="94a31-270">Make an audio and video call to a combination of VoIP and PSTN users</span></span> | <span data-ttu-id="94a31-271"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; ,4: &lt; phonenumber&gt;</span><span class="sxs-lookup"><span data-stu-id="94a31-271">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,4:&lt;phonenumber&gt;</span></span> | <span data-ttu-id="94a31-272"> https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210</span><span class="sxs-lookup"><span data-stu-id="94a31-272">https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210</span></span> |
  
<span data-ttu-id="94a31-273">クエリ パラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94a31-273">Following are the query parameters:</span></span>
* <span data-ttu-id="94a31-274">`users`: 呼び出しの参加者を表すユーザー ID のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="94a31-274">`users`: The comma-separated list of user IDs representing the participants of the call.</span></span> <span data-ttu-id="94a31-275">現在、User ID フィールドは Azure AD UserPrincipalName (通常は電子メール アドレス) をサポートしています。PSTN 通話の場合は、pstn mri 4: phonenumber をサポートしています。 &lt; &gt;</span><span class="sxs-lookup"><span data-stu-id="94a31-275">Currently, the User ID field supports the Azure AD UserPrincipalName, typically an email address, or in case of a PSTN call, it supports a pstn mri 4:&lt;phonenumber&gt;.</span></span>
* <span data-ttu-id="94a31-276">`Withvideo`: これはオプションのパラメーターで、ビデオ通話に使用できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-276">`Withvideo`: This is an optional parameter, which you can use to make a video call.</span></span> <span data-ttu-id="94a31-277">このパラメーターを設定すると、呼び出し元のカメラだけがオンにされます。</span><span class="sxs-lookup"><span data-stu-id="94a31-277">Setting this parameter will only turn on the caller's camera.</span></span> <span data-ttu-id="94a31-278">通話の受信者は、通話通知ウィンドウから音声通話または音声通話とビデオ通話に応答Teams選択できます。</span><span class="sxs-lookup"><span data-stu-id="94a31-278">The receiver of the call has a choice to answer through audio or audio and video call through the Teams call notification window.</span></span> 
* <span data-ttu-id="94a31-279">`Source`: これはオプションのパラメーターで、ディープリンクのソースを通知します。</span><span class="sxs-lookup"><span data-stu-id="94a31-279">`Source`: This is an optional parameter, which informs about the source of the deeplink.</span></span>

## <a name="code-sample"></a><span data-ttu-id="94a31-280">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="94a31-280">Code sample</span></span>

| <span data-ttu-id="94a31-281">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="94a31-281">Sample name</span></span> | <span data-ttu-id="94a31-282">説明</span><span class="sxs-lookup"><span data-stu-id="94a31-282">Description</span></span> | <span data-ttu-id="94a31-283">C#</span><span class="sxs-lookup"><span data-stu-id="94a31-283">C#</span></span> |<span data-ttu-id="94a31-284">Node.js</span><span class="sxs-lookup"><span data-stu-id="94a31-284">Node.js</span></span>|
|-------------|-------------|------|----|
|<span data-ttu-id="94a31-285">Subentity ID を使用するディープ リンク</span><span class="sxs-lookup"><span data-stu-id="94a31-285">Deep Link consuming Subentity ID</span></span>  |<span data-ttu-id="94a31-286">Microsoft Teamsチャットからサブエンティ ID を使用するタブへのディープリンクを示すサンプル アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="94a31-286">Microsoft Teams sample app for demonstrating deeplink from bot chat to tab consuming Subentity ID.</span></span>|[<span data-ttu-id="94a31-287">View</span><span class="sxs-lookup"><span data-stu-id="94a31-287">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[<span data-ttu-id="94a31-288">View</span><span class="sxs-lookup"><span data-stu-id="94a31-288">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a><span data-ttu-id="94a31-289">関連項目</span><span class="sxs-lookup"><span data-stu-id="94a31-289">See also</span></span>

[<span data-ttu-id="94a31-290">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="94a31-290">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

