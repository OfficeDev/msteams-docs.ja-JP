---
title: 詳細なリンクを作成する
description: 詳細なリンクとアプリでの使用方法について説明します。
keywords: teams ディープリンクディープリンク
ms.openlocfilehash: 03580c4d15c82da70402d68d85b0d28f8afa670e
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801244"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a><span data-ttu-id="692fc-104">Microsoft Teams のコンテンツと機能への詳細なリンクを作成する</span><span class="sxs-lookup"><span data-stu-id="692fc-104">Create deep links to content and features in Microsoft Teams</span></span>

<span data-ttu-id="692fc-105">Teams クライアント内の情報と機能へのリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="692fc-105">You can create links to information and features within the Teams client.</span></span> <span data-ttu-id="692fc-106">この例は、役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="692fc-106">Examples of where this may be useful:</span></span>

* <span data-ttu-id="692fc-107">アプリのタブのいずれか内のコンテンツにユーザーを移動します。</span><span class="sxs-lookup"><span data-stu-id="692fc-107">Navigating the user to content within one of your app's tabs.</span></span> <span data-ttu-id="692fc-108">たとえば、アプリには、重要なアクティビティをユーザーに通知するメッセージを送信する bot がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="692fc-108">For instance, your app may have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="692fc-109">ユーザーが通知をタップすると、ディープリンクがタブに移動し、ユーザーがアクティビティの詳細を表示できるようになります。</span><span class="sxs-lookup"><span data-stu-id="692fc-109">When the user taps on the notification, the deep link navigates to the tab so the user can view more details about the activity.</span></span>
* <span data-ttu-id="692fc-110">アプリでは、必要なパラメーターでディープリンクを事前に設定することによって、チャットの作成、会議のスケジュール設定など、特定のユーザータスクを自動化または簡素化します。</span><span class="sxs-lookup"><span data-stu-id="692fc-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre-populating the deep links with required parameters.</span></span> <span data-ttu-id="692fc-111">これにより、ユーザーが情報を手動で入力する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="692fc-111">This avoids the need for users to manually enter information.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="692fc-112">タブへの詳細なリンク</span><span class="sxs-lookup"><span data-stu-id="692fc-112">Deep linking to your tab</span></span>

<span data-ttu-id="692fc-113">Teams のエンティティへの詳細なリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="692fc-113">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="692fc-114">通常、これは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。たとえば、タブにタスクリストが含まれている場合は、チームメンバーが個々のタスクへのリンクを作成して共有することがあります。</span><span class="sxs-lookup"><span data-stu-id="692fc-114">Typically, this is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list team members may create and share links to individual tasks.</span></span> <span data-ttu-id="692fc-115">このリンクをクリックすると、特定の項目を中心とするタブに移動します。</span><span class="sxs-lookup"><span data-stu-id="692fc-115">When clicked, the link navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="692fc-116">これを実装するには、UI に最適な方法で、各アイテムに "リンクのコピー" アクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="692fc-116">To implement this, you add a "copy link" action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="692fc-117">ユーザーがこのアクションを実行すると、を呼び出して、 `shareDeepLink()` クリップボードにコピーできるリンクを含むダイアログボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="692fc-117">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="692fc-118">この呼び出しを行うと、アイテムの ID も渡されます。この ID は、リンクの後に tab キーが再読み込みされたときに[コンテキスト](~/tabs/how-to/access-teams-context.md)に戻されます。</span><span class="sxs-lookup"><span data-stu-id="692fc-118">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="692fc-119">または、このトピックで後述する形式を使用して、プログラムによってディープリンクを生成することもできます。</span><span class="sxs-lookup"><span data-stu-id="692fc-119">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="692fc-120">これらのメッセージを[ボット](~/bots/what-are-bots.md)および[コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)メッセージで使用して、タブの変更やその中のアイテムについてユーザーに通知することができます。</span><span class="sxs-lookup"><span data-stu-id="692fc-120">You might want to use these in [bot](~/bots/what-are-bots.md) and [Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="692fc-121">これは、[**リンクのリンク] タブ**メニュー項目で提供されるリンクとは異なり、このタブをポイントするディープリンクのみを生成します。</span><span class="sxs-lookup"><span data-stu-id="692fc-121">This is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="692fc-122">タブ内のアイテムへの詳細なリンクを表示する</span><span class="sxs-lookup"><span data-stu-id="692fc-122">Showing a deep link to an item within your tab</span></span>

<span data-ttu-id="692fc-123">タブ内のアイテムへの詳細なリンクを含むダイアログボックスを表示するには、`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span><span class="sxs-lookup"><span data-stu-id="692fc-123">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span></span>

<span data-ttu-id="692fc-124">次のフィールドを指定します。</span><span class="sxs-lookup"><span data-stu-id="692fc-124">Provide these fields:</span></span>

* <span data-ttu-id="692fc-125">`subEntityId`&emsp;タブ内で詳細にリンクしているアイテムの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="692fc-125">`subEntityId`&emsp;A unique identifier for the item within your tab to which you are deep linking</span></span>
* <span data-ttu-id="692fc-126">`subEntityLabel`&emsp;ディープリンクの表示に使用するアイテムのラベル</span><span class="sxs-lookup"><span data-stu-id="692fc-126">`subEntityLabel`&emsp;A label for the item to use for displaying the deep link</span></span>
* <span data-ttu-id="692fc-127">`subEntityWebUrl`&emsp;クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を含むオプションフィールド</span><span class="sxs-lookup"><span data-stu-id="692fc-127">`subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab</span></span>

### <a name="generating-a-deep-link-to-your-tab"></a><span data-ttu-id="692fc-128">タブに詳細なリンクを生成する</span><span class="sxs-lookup"><span data-stu-id="692fc-128">Generating a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="692fc-129">静的タブのスコープは "personal" で、構成可能なタブの範囲は "team" です。</span><span class="sxs-lookup"><span data-stu-id="692fc-129">Static tabs have a scope of "personal" and configurable tabs have a scope of "team".</span></span> <span data-ttu-id="692fc-130">2つのタブの種類の構文は、構成可能なタブだけに `channel` コンテキストオブジェクトに関連付けられているプロパティがあるため、構文が若干異なります。</span><span class="sxs-lookup"><span data-stu-id="692fc-130">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="692fc-131">個人とチームのスコープの詳細については、「[マニフェスト](~/resources/schema/manifest-schema.md)リファレンス」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="692fc-131">See the [Manifest](~/resources/schema/manifest-schema.md) reference for more information on personal and team scopes.</span></span>
> [!NOTE]
> <span data-ttu-id="692fc-132">ディープリンクは、タブが v2.0 以降のライブラリを使用して構成されている場合にのみ正しく機能し、そのためにはエンティティ ID を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="692fc-132">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="692fc-133">エンティティ Id のないタブへの深いリンクは、タブに移動しますが、サブエンティティ ID をタブに提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="692fc-133">Deep links to tabs without entity IDs still navigate to the tab but can't provide the sub-entity ID to the tab.</span></span>

<span data-ttu-id="692fc-134">Bot、コネクタ、またはメッセージング拡張カードで使用できるディープリンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="692fc-134">Use this format for a deep link that you can use in a bot, Connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

<span data-ttu-id="692fc-135">クエリパラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="692fc-135">The query parameters are:</span></span>

* <span data-ttu-id="692fc-136">`appId`&emsp;マニフェストからの ID。たとえば、"fe4a8eba-2a31-4737-8e33-e5fae6fee194" のようになります。</span><span class="sxs-lookup"><span data-stu-id="692fc-136">`appId`&emsp;The ID from your manifest; for example, "fe4a8eba-2a31-4737-8e33-e5fae6fee194"</span></span>
* <span data-ttu-id="692fc-137">`entityId`&emsp;タブ内のアイテムの ID。タブを[構成](~/tabs/how-to/create-tab-pages/configuration-page.md)するときに指定します。たとえば、"tasklist123" のようになります。</span><span class="sxs-lookup"><span data-stu-id="692fc-137">`entityId`&emsp;The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md); for example, "tasklist123"</span></span>
* <span data-ttu-id="692fc-138">`entityWebUrl`または、 `subEntityWebUrl` &emsp; クライアントがタブのレンダリングをサポートしていない場合に使用するフォールバック URL を持つオプションフィールド。たとえば、" https://tasklist.example.com/123 " または " https://tasklist.example.com/list123/task456 "</span><span class="sxs-lookup"><span data-stu-id="692fc-138">`entityWebUrl` or `subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab; for example, "https://tasklist.example.com/123" or "https://tasklist.example.com/list123/task456"</span></span>
* <span data-ttu-id="692fc-139">`entityLabel`または、 `subEntityLabel` &emsp; タブ内のアイテムのラベルを使用して、ディープリンクを表示するときに使用します。たとえば、"タスクリスト 123" や "タスク 456" などです。</span><span class="sxs-lookup"><span data-stu-id="692fc-139">`entityLabel` or `subEntityLabel`&emsp;A label for the item in your tab, to use when displaying the deep link; for example, "Task List 123" or "Task 456"</span></span>
* <span data-ttu-id="692fc-140">`context`&emsp;次のフィールドを含む JSON オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="692fc-140">`context`&emsp;A JSON object containing the following fields:</span></span>
  * <span data-ttu-id="692fc-141">`subEntityId`&emsp;タブ_内_のアイテムの ID。たとえば、"task456" のようになります。</span><span class="sxs-lookup"><span data-stu-id="692fc-141">`subEntityId`&emsp;An ID for the item _within_ the tab; for example, "task456"</span></span>
  * <span data-ttu-id="692fc-142">`channelId`&emsp;Microsoft Teams channel ID (タブ[コンテキスト](~/tabs/how-to/access-teams-context.md)から使用可能)。たとえば、"19: cbe3683f25094106b826c9cada3afbe0@thread" です。</span><span class="sxs-lookup"><span data-stu-id="692fc-142">`channelId`&emsp;The Microsoft Teams channel ID (available from the tab [context](~/tabs/how-to/access-teams-context.md); for example, "19:cbe3683f25094106b826c9cada3afbe0@thread.skype".</span></span> <span data-ttu-id="692fc-143">このプロパティは、範囲が "team" である構成可能なタブでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="692fc-143">This property is only available in configurable tabs with a scope of "team".</span></span> <span data-ttu-id="692fc-144">これは、スコープが "personal" である静的タブでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="692fc-144">It is not available in static tabs, which have a scope of "personal".</span></span>

<span data-ttu-id="692fc-145">例:</span><span class="sxs-lookup"><span data-stu-id="692fc-145">Examples:</span></span>

* <span data-ttu-id="692fc-146">構成可能なタブ自体にリンクします。`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="692fc-146">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="692fc-147">[構成可能] タブ内のタスクアイテムへのリンク:`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="692fc-147">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="692fc-148">静的タブ自体にリンクします。`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="692fc-148">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="692fc-149">[静的] タブ内のタスクアイテムにリンクします。`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="692fc-149">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="692fc-150">すべてのクエリパラメーターが正しい URI エンコードになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="692fc-150">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="692fc-151">読みやすくするために、上記の例は含まれていませんが、指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="692fc-151">For the sake of readability, the above examples are not, but you should.</span></span> <span data-ttu-id="692fc-152">最後の例を使用します。</span><span class="sxs-lookup"><span data-stu-id="692fc-152">Using the last example:</span></span>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a><span data-ttu-id="692fc-153">タブからのディープリンクの使用</span><span class="sxs-lookup"><span data-stu-id="692fc-153">Consuming a deep link from a tab</span></span>

<span data-ttu-id="692fc-154">深いリンクに移動すると、Microsoft Teams は単にタブに移動し、Microsoft Teams の JavaScript ライブラリを使用して、サブエンティティ ID (存在する場合) を取得するためのメカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="692fc-154">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism via the Microsoft Teams JavaScript library to retrieve the sub-entity ID (if it exists).</span></span>

<span data-ttu-id="692fc-155">この [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) 呼び出しは、 `subEntityId` ディープリンクを介してタブが移動された場合に、フィールドを含むコンテキストを返します。</span><span class="sxs-lookup"><span data-stu-id="692fc-155">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab was navigated to via a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="692fc-156">タブからの詳細なリンク</span><span class="sxs-lookup"><span data-stu-id="692fc-156">Deep linking from your tab</span></span>

<span data-ttu-id="692fc-157">タブから Teams のコンテンツにディープリンクすることができます。これは、チャネル、メッセージ、別のタブなど、Teams の他のコンテンツにリンクする必要がある場合や、スケジュール設定ダイアログを開く場合にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="692fc-157">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="692fc-158">タブからディープリンクを開始するには、次のように呼び出します。</span><span class="sxs-lookup"><span data-stu-id="692fc-158">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="692fc-159">これにより、正しい URL に移動するか、スケジュール設定またはアプリのインストールダイアログを開くなど、クライアントの動作を開始することができます。</span><span class="sxs-lookup"><span data-stu-id="692fc-159">This will navigate you to the correct URL, or trigger a client action such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="692fc-160">例:</span><span class="sxs-lookup"><span data-stu-id="692fc-160">Example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="692fc-161">チャットへの詳細なリンク</span><span class="sxs-lookup"><span data-stu-id="692fc-161">Deep linking to a chat</span></span>

<span data-ttu-id="692fc-162">参加者のセットを指定することによって、ユーザー間のプライベートチャットへの詳細なリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="692fc-162">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="692fc-163">指定した参加者のチャットが存在しない場合、リンクによってユーザーは空の新しいチャットに移動されます。</span><span class="sxs-lookup"><span data-stu-id="692fc-163">If a chat doesn't exist with the specified participants, the link will navigate the user to an empty new chat.</span></span> <span data-ttu-id="692fc-164">新しいチャットは、ユーザーが最初のメッセージを送信するまで下書き状態で作成されます。</span><span class="sxs-lookup"><span data-stu-id="692fc-164">New chats will be created in draft state until the user sends the first message.</span></span> <span data-ttu-id="692fc-165">必要に応じて、チャットの名前 (まだ存在しない場合)、およびユーザーの新規作成ボックスに挿入するテキストを指定できます。</span><span class="sxs-lookup"><span data-stu-id="692fc-165">Optionally, you can specify the name of the chat (if it doesn't already exist), along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="692fc-166">この機能は、ユーザーが手動でチャットに移動したり、メッセージを入力したりする操作を実行するためのショートカットと考えることができます。</span><span class="sxs-lookup"><span data-stu-id="692fc-166">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="692fc-167">ユースケースの例として、ボットから Office 365 ユーザープロファイルをカードとして返す場合、このディープリンクを使用すると、その人物と簡単にチャットすることができます。</span><span class="sxs-lookup"><span data-stu-id="692fc-167">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generating-a-deep-link-to-a-chat"></a><span data-ttu-id="692fc-168">チャットへの詳細なリンクの生成</span><span class="sxs-lookup"><span data-stu-id="692fc-168">Generating a deep link to a chat</span></span>

<span data-ttu-id="692fc-169">Bot、コネクタ、またはメッセージング拡張カードで使用できるディープリンクには、次の形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="692fc-169">Use this format for a deep link that you can use in a bot, Connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="692fc-170">例: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="692fc-170">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="692fc-171">クエリパラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="692fc-171">The query parameters are:</span></span>

* <span data-ttu-id="692fc-172">`users`&emsp;チャットの参加者を表すユーザー Id のコンマ区切りのリスト。</span><span class="sxs-lookup"><span data-stu-id="692fc-172">`users`&emsp;The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="692fc-173">アクションを実行するユーザーは、常に参加者として含まれます。</span><span class="sxs-lookup"><span data-stu-id="692fc-173">The user performing the action is always included as a participant.</span></span> <span data-ttu-id="692fc-174">現時点では、ユーザー ID フィールドは Azure AD UserPrincipalName のみをサポートしています (通常はメールアドレス)。</span><span class="sxs-lookup"><span data-stu-id="692fc-174">The User ID field currently only supports the Azure AD UserPrincipalName (typically an email address).</span></span>
* <span data-ttu-id="692fc-175">`topicName`&emsp;3人以上のユーザーとチャットする場合は、チャットの表示名のオプションフィールド。</span><span class="sxs-lookup"><span data-stu-id="692fc-175">`topicName`&emsp;An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="692fc-176">このフィールドが指定されていない場合、チャットの表示名は参加者の名前に基づきます。</span><span class="sxs-lookup"><span data-stu-id="692fc-176">If this field is not specified, the chat's display name will be based on the names of the participants.</span></span>
* <span data-ttu-id="692fc-177">`message`&emsp;現在のユーザーの新規作成ボックスに挿入するメッセージテキストのオプションフィールドで、チャットは下書きの状態になっています。</span><span class="sxs-lookup"><span data-stu-id="692fc-177">`message`&emsp;An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="692fc-178">この深いリンクを bot と組み合わせて使用するには、カードのボタンの URL のターゲットとしてこれを指定するか、アクションの種類の [アクション] をタップし `openUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="692fc-178">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="linking-to-the-scheduling-dialog"></a><span data-ttu-id="692fc-179">[スケジュール] ダイアログにリンクする</span><span class="sxs-lookup"><span data-stu-id="692fc-179">Linking to the scheduling dialog</span></span>

> [!Note]
> <span data-ttu-id="692fc-180">この機能は現在、開発者向けプレビューに含まれています。</span><span class="sxs-lookup"><span data-stu-id="692fc-180">This feature is currently in developer preview.</span></span>

<span data-ttu-id="692fc-181">Teams クライアントの組み込みのスケジュールダイアログへの詳細なリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="692fc-181">You can create deep links to the Teams client's built-in scheduling dialog.</span></span> <span data-ttu-id="692fc-182">これは、ユーザーが予定表またはスケジュール関連のタスクを完了するのにアプリが役立つ場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="692fc-182">This is especially useful if your app helps the user complete calendar or scheduling-related tasks.</span></span>

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="692fc-183">スケジュールダイアログへの詳細なリンクの生成</span><span class="sxs-lookup"><span data-stu-id="692fc-183">Generating a deep link to the scheduling dialog</span></span>

<span data-ttu-id="692fc-184">Bot、コネクタ、またはメッセージング拡張カードで使用できるディープリンクには、次の形式を使用します。`https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="692fc-184">Use this format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="692fc-185">例: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="692fc-185">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="692fc-186">クエリパラメーターは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="692fc-186">The query parameters are:</span></span>

* <span data-ttu-id="692fc-187">`attendees`&emsp;会議の出席者を表すユーザー Id のコンマ区切りリスト (オプション)。</span><span class="sxs-lookup"><span data-stu-id="692fc-187">`attendees`&emsp;The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="692fc-188">アクションを実行するユーザーは、会議の開催者です。</span><span class="sxs-lookup"><span data-stu-id="692fc-188">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="692fc-189">現時点では、ユーザー ID フィールドは Azure AD UserPrincipalName のみをサポートしています (通常はメールアドレス)。</span><span class="sxs-lookup"><span data-stu-id="692fc-189">The User ID field currently only supports the Azure AD UserPrincipalName (typically an email address).</span></span>
* <span data-ttu-id="692fc-190">`startTime`&emsp;イベントのオプションの開始時刻。</span><span class="sxs-lookup"><span data-stu-id="692fc-190">`startTime`&emsp;The optional start time of the event.</span></span> <span data-ttu-id="692fc-191">これは、"2018-03-12T23:55:25 + 02:00" のような[長い ISO 8601 形式](https://en.wikipedia.org/wiki/ISO_8601)にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="692fc-191">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example “2018-03-12T23:55:25+02:00”.</span></span>
* <span data-ttu-id="692fc-192">`endTime`&emsp;イベントのオプションの終了時刻 (ISO 8601 形式の場合もあります)。</span><span class="sxs-lookup"><span data-stu-id="692fc-192">`endTime`&emsp;The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="692fc-193">`subject`&emsp;会議の件名のオプションフィールド。</span><span class="sxs-lookup"><span data-stu-id="692fc-193">`subject`&emsp;An optional field for the meeting subject.</span></span>
* <span data-ttu-id="692fc-194">`content`&emsp;会議の詳細フィールドのオプションフィールド。</span><span class="sxs-lookup"><span data-stu-id="692fc-194">`content`&emsp;An optional field for the meeting details field.</span></span>

<span data-ttu-id="692fc-195">現在、場所を指定することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="692fc-195">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="692fc-196">開始時刻と終了時刻を生成するときは、必ず UTC オフセット (タイムゾーン) を指定してください。</span><span class="sxs-lookup"><span data-stu-id="692fc-196">When generating your start and end times be sure to specify the UTC offset (time zones).</span></span>

<span data-ttu-id="692fc-197">この深いリンクを bot と組み合わせて使用するには、カードのボタンの URL のターゲットとしてこれを指定するか、アクションの種類の [アクション] をタップし `openUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="692fc-197">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>
