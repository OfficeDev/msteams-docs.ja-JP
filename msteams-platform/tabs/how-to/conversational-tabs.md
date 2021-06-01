---
title: 会話タブの作成
author: laujan
description: チャネル タブの会話型サブエンティティ チャットを作成する
keywords: teams タブ チャネル構成可能
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 4171265a3ef4ad917661e258dd7305f82411c5ef
ms.sourcegitcommit: 118f7261d313feeac5b398fef56a44bd90104b2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2021
ms.locfileid: "52709653"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="9d5a6-104">会話タブの作成</span><span class="sxs-lookup"><span data-stu-id="9d5a6-104">Create conversational tabs</span></span>

<span data-ttu-id="9d5a6-105">会話サブエンティティは、ユーザーがタブ全体 (エンティティとも呼ばれる) を議論する代わりに、特定のタスク、患者、販売機会などのサブエンティティに関する会話をタブ内で行う方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="9d5a6-106">従来のチャネルまたは構成可能なタブを使用すると、ユーザーはタブに関する会話を行えますが、ユーザーは、より集中した会話を望む場合があります。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user may want a more focused conversation.</span></span> <span data-ttu-id="9d5a6-107">一元的なディスカッションを行うコンテンツが多すぎる場合や、時間の間にコンテンツが変更された場合に、より集中した会話の要件が発生し、表示されるコンテンツに関係ありません。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="9d5a6-108">会話サブエンティティは、動的タブに対して、より集中した会話エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="9d5a6-109">会話型サブエンティティはチャネルでのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="9d5a6-110">ただし、個人タブまたは静的タブから使用して、チャネルに既にピン留めされているタブで会話を作成または続行できます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-110">However, they can be used from a personal or static tab to create or continue conversations in tabs that are *already* pinned to a channel.</span></span> <span data-ttu-id="9d5a6-111">静的タブは、ユーザーが複数のチャネルで発生する会話を表示およびアクセスするために 1 つの場所を提供する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-111">The static tab is useful if you wish to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d5a6-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="9d5a6-112">Prerequisites</span></span>

<span data-ttu-id="9d5a6-113">会話型サブエンティティをサポートするには、タブ Web アプリケーションがバックエンド データベース内のサブエンティティと会話間のマッピング↔する機能が必要です。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="9d5a6-114">弊社は、お客様に提供しますが、ユーザーが会話を継続するために、その情報を保存し、Teamsに戻す責任 `conversationId` `conversationId` があります。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-114">We will provide you with the `conversationId`, but it will be your responsibility to store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="9d5a6-115">新しい会話を開始する</span><span class="sxs-lookup"><span data-stu-id="9d5a6-115">Start a new conversation</span></span>

<span data-ttu-id="9d5a6-116">新しい会話を開始するには、関数を使用 `openConversation()` します。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-116">To start a new conversation, you use the `openConversation()` function.</span></span> <span data-ttu-id="9d5a6-117">会話の開始と継続は、すべてこのメソッドによって処理されます。ただし、関数への入力は、実行するアクションに応じて変わります。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-117">Starting and continuing a conversation are all handled by this method, however, the inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="9d5a6-118">ユーザーの観点から、会話を開始するか、会話を続行するために、画面の右側に会話パネルが開きます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-118">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="9d5a6-119">**openConversation は、** チャネルで会話を開始するために次の入力を受け取る。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-119">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="9d5a6-120">**subEntityId**: これは、特定のサブエンティティの ID です。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-120">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="9d5a6-121">たとえば、task-123。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-121">For example, task-123.</span></span>
* <span data-ttu-id="9d5a6-122">**entityId**: これは、作成されたタブ インスタンスの ID です。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-122">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="9d5a6-123">ID は、同じタブ インスタンスを参照することが重要です。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-123">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="9d5a6-124">**channelId**: これは、タブ インスタンスが存在するチャネルです。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-124">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="9d5a6-125">**channelId は**、チャネル タブのオプションです。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-125">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="9d5a6-126">ただし、チャネルと静的タブ間で実装を同じに維持する場合は、お勧めします。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-126">However, it is recommended if you wish to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="9d5a6-127">**title**: これは、チャット パネルでユーザーに表示されるタイトルです。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-127">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="9d5a6-128">これらの値の大部分は、API から取得 `getContext` することもできます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-128">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="9d5a6-129">これにより、会話パネルが開きます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-129">This will open the conversation panel.</span></span>

![Conversationl Sub Entities - 会話の開始](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="9d5a6-131">ユーザーが会話を開始する場合は、conversationId を取得して保存するために、そのイベントのコールバックをリッスンすることが **重要です**。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-131">If the user starts a conversation, it’s important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="9d5a6-132">オブジェクト `conversationReponse` には、開始し始めた会話に関連する情報が含まれる。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-132">The `conversationReponse` object contains information related to the conversation that was just started.</span></span> <span data-ttu-id="9d5a6-133">後で再利用するために、この応答オブジェクトのすべてのプロパティを保存することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-133">We recommend you save all the properties of this response object for reuse later.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="9d5a6-134">会話を続ける</span><span class="sxs-lookup"><span data-stu-id="9d5a6-134">Continue a conversation</span></span>

<span data-ttu-id="9d5a6-135">会話の開始後、以降の呼び出しでは、[新しいチャネル タブの会話を開始する] と同じ入力を入力する必要がありますが `openConversation()` **、conversationId も含める必要があります**。 [](#Starting a new channel tab conversation)</span><span class="sxs-lookup"><span data-stu-id="9d5a6-135">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [Starting a new channel tab conversation](#Starting a new channel tab conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="9d5a6-136">適切な会話が表示されているユーザーの会話パネルが開きます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-136">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="9d5a6-137">ユーザーは、新しいメッセージまたは受信メッセージをリアルタイムで表示できます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-137">Users are able to see new or incoming messages in real-time.</span></span>

![Conversationl Sub Entities - Continue Conversation](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="9d5a6-139">会話を強化する</span><span class="sxs-lookup"><span data-stu-id="9d5a6-139">Enhance a conversation</span></span>

<span data-ttu-id="9d5a6-140">最後に、タブがサブエンティティへのディープリンクを使用 [することが重要です](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-140">Finally, it’s important that your tab consumes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="9d5a6-141">たとえば、チャネル会話からタブ のシックレットディープリンクをクリックするとします。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-141">For example, user clicking the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="9d5a6-142">想定される動作は、ディープリンクを受信し、そのサブエンティティを開き、その特定のサブエンティティの会話パネルを開く動作です。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-142">The expected behavior is for you to receive the deeplink, open that sub-entity, and then open the conversation panel for that specific sub-entity.</span></span>

<span data-ttu-id="9d5a6-143">個人タブまたは静的タブから会話サブエンティティをサポートするには、実装について何も変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-143">To support conversational sub-entities from your personal or static tab, you do not have to change anything about your implementation.</span></span> <span data-ttu-id="9d5a6-144">既にピン留めされているチャネル タブからの会話の開始または継続のみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-144">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="9d5a6-145">静的タブをサポートすると、ユーザーがすべてのサブエンティティを操作するための 1 つの場所を提供できます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-145">Supporting static tabs allow you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="9d5a6-146">ただし、静的タブで会話ビューを開く際に適切なプロパティを持つには、チャネル内にタブが最初に作成されている場合に、 を保存することが `subEntityId` `entityId` 重要です `channelId` 。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-146">It is, however, important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel in order for you to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="9d5a6-147">会話を閉じる</span><span class="sxs-lookup"><span data-stu-id="9d5a6-147">Close a conversation</span></span>

<span data-ttu-id="9d5a6-148">関数を呼び出すことによって、会話ビューを手動で閉 `closeConversation()` じできます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-148">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="9d5a6-149">ユーザーが会話ビューを閉じたときにイベントをリッスンできます。</span><span class="sxs-lookup"><span data-stu-id="9d5a6-149">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```
