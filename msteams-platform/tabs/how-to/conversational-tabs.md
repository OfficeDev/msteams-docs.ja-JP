---
title: 会話タブを作成する
author: surbhigupta
description: チャネル タブの会話型サブエンティティ チャットを作成する
keywords: teams タブ チャネル構成可能
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: fbc5e90842c892cfb7e14f845563d7d2ffb397bb
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140265"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="0007e-104">会話タブを作成する</span><span class="sxs-lookup"><span data-stu-id="0007e-104">Create conversational tabs</span></span>

<span data-ttu-id="0007e-105">会話サブエンティティは、ユーザーがタブ全体 (エンティティとも呼ばれる) を議論する代わりに、特定のタスク、患者、販売機会などのサブエンティティに関する会話をタブ内で行う方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="0007e-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="0007e-106">従来のチャネルまたは構成可能なタブを使用すると、ユーザーはタブに関する会話を行えますが、ユーザーは、より集中した会話を必要とします。</span><span class="sxs-lookup"><span data-stu-id="0007e-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user requires a more focused conversation.</span></span> <span data-ttu-id="0007e-107">一元的なディスカッションを行うコンテンツが多すぎる場合、または時間の間にコンテンツが変更され、表示されるコンテンツに関係のない会話になる場合、より集中した会話の要件が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0007e-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or because the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="0007e-108">会話サブエンティティは、動的タブに対して、より集中した会話エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="0007e-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="0007e-109">会話型サブエンティティはチャネルでのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="0007e-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="0007e-110">これらは、個人用タブまたは静的タブから使用して、チャネルに既にピン留めされているタブで会話を作成または続行できます。</span><span class="sxs-lookup"><span data-stu-id="0007e-110">They can be used from a personal or static tab to create or continue conversations in tabs that are already pinned to a channel.</span></span> <span data-ttu-id="0007e-111">静的タブは、ユーザーが複数のチャネルで発生する会話を表示およびアクセスするために 1 つの場所を提供する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="0007e-111">The static tab is useful if you want to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0007e-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="0007e-112">Prerequisites</span></span>

<span data-ttu-id="0007e-113">会話型サブエンティティをサポートするには、タブ Web アプリケーションがバックエンド データベース内のサブエンティティと会話間のマッピング↔する機能が必要です。</span><span class="sxs-lookup"><span data-stu-id="0007e-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="0007e-114">は指定されますが、ユーザーが会話を続行するには、Teamsを保存して返 `conversationId` `conversationId` す必要があります。</span><span class="sxs-lookup"><span data-stu-id="0007e-114">The `conversationId` is provided, but you must store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="0007e-115">新しい会話を開始する</span><span class="sxs-lookup"><span data-stu-id="0007e-115">Start a new conversation</span></span>

<span data-ttu-id="0007e-116">新しい会話を開始するには、関数を使用 `openConversation()` します。</span><span class="sxs-lookup"><span data-stu-id="0007e-116">To start a new conversation, use the `openConversation()` function.</span></span> <span data-ttu-id="0007e-117">会話の開始と続行はすべて、このメソッドによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="0007e-117">Starting and continuing a conversation are all handled by this method.</span></span> <span data-ttu-id="0007e-118">関数への入力は、実行するアクションに応じて変わります。</span><span class="sxs-lookup"><span data-stu-id="0007e-118">The inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="0007e-119">ユーザーの観点から、会話を開始するか、会話を続行するために、画面の右側に会話パネルが開きます。</span><span class="sxs-lookup"><span data-stu-id="0007e-119">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="0007e-120">**openConversation は、** チャネルで会話を開始するために次の入力を受け取る。</span><span class="sxs-lookup"><span data-stu-id="0007e-120">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="0007e-121">**subEntityId**: これは、特定のサブエンティティの ID です。</span><span class="sxs-lookup"><span data-stu-id="0007e-121">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="0007e-122">たとえば、task-123。</span><span class="sxs-lookup"><span data-stu-id="0007e-122">For example, task-123.</span></span>
* <span data-ttu-id="0007e-123">**entityId**: これは、作成されたタブ インスタンスの ID です。</span><span class="sxs-lookup"><span data-stu-id="0007e-123">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="0007e-124">ID は、同じタブ インスタンスを参照することが重要です。</span><span class="sxs-lookup"><span data-stu-id="0007e-124">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="0007e-125">**channelId**: これは、タブ インスタンスが存在するチャネルです。</span><span class="sxs-lookup"><span data-stu-id="0007e-125">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="0007e-126">**channelId は**、チャネル タブのオプションです。</span><span class="sxs-lookup"><span data-stu-id="0007e-126">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="0007e-127">ただし、チャネルと静的タブ間で実装を同じにしておきたい場合は、お勧めします。</span><span class="sxs-lookup"><span data-stu-id="0007e-127">However, it is recommended if you want to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="0007e-128">**title**: これは、チャット パネルでユーザーに表示されるタイトルです。</span><span class="sxs-lookup"><span data-stu-id="0007e-128">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="0007e-129">これらの値の大部分は、API から取得 `getContext` することもできます。</span><span class="sxs-lookup"><span data-stu-id="0007e-129">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="0007e-130">次の図は、会話パネルを示しています。</span><span class="sxs-lookup"><span data-stu-id="0007e-130">The following image shows the conversation panel:</span></span>

![会話サブエンティティ - 会話の開始](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="0007e-132">ユーザーが会話を開始する場合は、conversationId を取得して保存するために、そのイベントのコールバックをリッスンすることが **重要です**。</span><span class="sxs-lookup"><span data-stu-id="0007e-132">If the user starts a conversation, it is important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="0007e-133">オブジェクト `conversationResponse` には、開始された会話に関連する情報が含まれる。</span><span class="sxs-lookup"><span data-stu-id="0007e-133">The `conversationResponse` object contains information related to the conversation that was started.</span></span> <span data-ttu-id="0007e-134">後で使用するために、この応答オブジェクトのすべてのプロパティを保存してください。</span><span class="sxs-lookup"><span data-stu-id="0007e-134">It is recommended that you save all the properties of this response object for later use.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="0007e-135">会話を続ける</span><span class="sxs-lookup"><span data-stu-id="0007e-135">Continue a conversation</span></span>

<span data-ttu-id="0007e-136">会話の開始後、以降の呼び出しでは、新しい会話を開始する場合と同じ入力を入力する必要がありますが `openConversation()` **、conversationId も含める必要があります**。 [](#start-a-new-conversation)</span><span class="sxs-lookup"><span data-stu-id="0007e-136">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [start a new conversation](#start-a-new-conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="0007e-137">適切な会話が表示されているユーザーの会話パネルが開きます。</span><span class="sxs-lookup"><span data-stu-id="0007e-137">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="0007e-138">ユーザーは、新しいメッセージまたは受信メッセージをリアルタイムで表示できます。</span><span class="sxs-lookup"><span data-stu-id="0007e-138">Users are able to see new or incoming messages in real-time.</span></span>

<span data-ttu-id="0007e-139">次の図は、適切な会話を含む会話パネルを示しています。</span><span class="sxs-lookup"><span data-stu-id="0007e-139">The following image shows the conversation panel with the appropriate conversation:</span></span>

![会話サブエンティティ - 会話の継続](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="0007e-141">会話を強化する</span><span class="sxs-lookup"><span data-stu-id="0007e-141">Enhance a conversation</span></span>

<span data-ttu-id="0007e-142">タブにサブエンティティへのディープリンクが [含まれる必要があります](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="0007e-142">It is important that your tab includes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="0007e-143">たとえば、チャネル会話からタブ シックレット ディープリンクを選択したユーザー。</span><span class="sxs-lookup"><span data-stu-id="0007e-143">For example, user selecting the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="0007e-144">想定される動作は、ディープリンクを受信し、そのサブエンティティを開き、そのサブエンティティの会話パネルを開きます。</span><span class="sxs-lookup"><span data-stu-id="0007e-144">The expected behavior is to receive the deeplink, open that sub-entity, and then open the conversation panel for that sub-entity.</span></span>

<span data-ttu-id="0007e-145">個人タブまたは静的タブから会話サブエンティティをサポートするには、実装で何も変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="0007e-145">To support conversational sub-entities from your personal or static tab, you do not have to change anything in your implementation.</span></span> <span data-ttu-id="0007e-146">既にピン留めされているチャネル タブからの会話の開始または継続のみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="0007e-146">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="0007e-147">静的タブをサポートすることで、ユーザーがすべてのサブエンティティを操作するための 1 つの場所を提供できます。</span><span class="sxs-lookup"><span data-stu-id="0007e-147">Supporting static tabs allows you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="0007e-148">静的タブで会話ビューを開く際に適切なプロパティを持つには、チャネル内にタブが最初に作成されている場合に、 を保存することが `subEntityId` `entityId` `channelId` 重要です。</span><span class="sxs-lookup"><span data-stu-id="0007e-148">It is important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="0007e-149">会話を閉じる</span><span class="sxs-lookup"><span data-stu-id="0007e-149">Close a conversation</span></span>

<span data-ttu-id="0007e-150">関数を呼び出すことによって、会話ビューを手動で閉 `closeConversation()` じできます。</span><span class="sxs-lookup"><span data-stu-id="0007e-150">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="0007e-151">ユーザーが会話ビューを閉じたときにイベントをリッスンできます。</span><span class="sxs-lookup"><span data-stu-id="0007e-151">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="see-also"></a><span data-ttu-id="0007e-152">関連項目</span><span class="sxs-lookup"><span data-stu-id="0007e-152">See also</span></span>

* [<span data-ttu-id="0007e-153">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="0007e-153">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="0007e-154">前提条件</span><span class="sxs-lookup"><span data-stu-id="0007e-154">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="0007e-155">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="0007e-155">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="0007e-156">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="0007e-156">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="0007e-157">コンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="0007e-157">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="0007e-158">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="0007e-158">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="0007e-159">タブの削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="0007e-159">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="0007e-160">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="0007e-160">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="0007e-161">タブのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="0007e-161">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="0007e-162">アダプティブ カードを使用してタブをビルドする</span><span class="sxs-lookup"><span data-stu-id="0007e-162">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="0007e-163">タブのリンクの展開とステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="0007e-163">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)

## <a name="next-step"></a><span data-ttu-id="0007e-164">次の手順</span><span class="sxs-lookup"><span data-stu-id="0007e-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0007e-165">タブ余白の変更</span><span class="sxs-lookup"><span data-stu-id="0007e-165">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)