---
title: プロアクティブ メッセージを送信する
description: Microsoft Teams ボットでプロアクティブ メッセージを送信する方法について説明します。
ms.topic: conceptual
ms.author: anclear
Keywords: メッセージの送信、ユーザー ID の取得、チャネル ID の取得、会話 ID の取得
ms.openlocfilehash: 25d5c6a1b51240c87ff0d8610a965d30f6b01095
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697054"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="6ce75-104">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="6ce75-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="6ce75-105">プロアクティブ メッセージとは、ユーザーからの要求に応答しないボットから送信されるメッセージです。</span><span class="sxs-lookup"><span data-stu-id="6ce75-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="6ce75-106">これには、次のようなメッセージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-106">This can include messages, such as:</span></span>

* <span data-ttu-id="6ce75-107">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="6ce75-107">Welcome messages</span></span>
* <span data-ttu-id="6ce75-108">通知</span><span class="sxs-lookup"><span data-stu-id="6ce75-108">Notifications</span></span>
* <span data-ttu-id="6ce75-109">予定されたメッセージ</span><span class="sxs-lookup"><span data-stu-id="6ce75-109">Scheduled messages</span></span>

<span data-ttu-id="6ce75-110">ボットがユーザー、グループ チャット、またはチームにプロアクティブ メッセージを送信するには、そのボットにメッセージを送信するアクセス権が必要です。</span><span class="sxs-lookup"><span data-stu-id="6ce75-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="6ce75-111">グループ チャットまたはチームの場合、ボットを含むアプリを最初にその場所にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="6ce75-112">必要に[応じて、チーム](#proactively-install-your-app-using-graph)に Microsoft Graph を使用してアプリをプロアクティブに[](/microsoftteams/teams-custom-app-policies-and-settings)インストールするか、アプリ ポリシーを使用してテナントのチームとユーザーにアプリをプッシュアウトできます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="6ce75-113">ユーザーの場合、自分でアプリをインストールしているか、アプリがインストールされているチームのメンバーである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="6ce75-114">プロアクティブ メッセージの送信は、通常のメッセージの送信とは異なります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="6ce75-115">返信に使用 `turnContext` するアクティブはありません。</span><span class="sxs-lookup"><span data-stu-id="6ce75-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="6ce75-116">メッセージを送信する前に、会話を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="6ce75-117">たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。</span><span class="sxs-lookup"><span data-stu-id="6ce75-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="6ce75-118">プロアクティブ メッセージングでは、新しいグループ チャットやチーム内の新しいチャネルを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="6ce75-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="6ce75-119">**プロアクティブ メッセージを送信するには**</span><span class="sxs-lookup"><span data-stu-id="6ce75-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="6ce75-120">[必要に応じて、ユーザー ID、チーム ID、またはチャネル ID](#get-the-user-id-team-id-or-channel-id)を取得します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="6ce75-121">[必要に応じて、](#create-the-conversation)会話を作成します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="6ce75-122">[会話ID を取得します](#get-the-conversation-id)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="6ce75-123">[メッセージを送信します](#send-the-message)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="6ce75-124">プロアクティブ メッセージを効果的に使用するには、「プロアクティブ [メッセージングのベスト プラクティス」を参照してください](#best-practices-for-proactive-messaging)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-124">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="6ce75-125">特定のシナリオでは、Graph を [使用してアプリを事前にインストールする必要があります](#proactively-install-your-app-using-graph)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-125">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="6ce75-126">サンプル セクションのコード スニペット [は](#samples) 、1 対 1 の会話を作成するためのコード スニペットです。</span><span class="sxs-lookup"><span data-stu-id="6ce75-126">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="6ce75-127">1 対 1 の会話とグループまたはチャネルの両方の完全な作業サンプルについては、コード サンプルを [参照してください](#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-127">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="6ce75-128">ユーザー ID、チーム ID、またはチャネル ID を取得する</span><span class="sxs-lookup"><span data-stu-id="6ce75-128">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="6ce75-129">チャネルに新しいスレッドまたは会話スレッドを作成するには、正しい ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="6ce75-129">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="6ce75-130">次の ID を使用して、この ID を受信または取得できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-130">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="6ce75-131">アプリが特定のコンテキストにインストールされている場合は、アクティビティを受信[ `onMembersAdded` します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-131">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="6ce75-132">アプリがインストールされているコンテキストに新しいユーザーを追加すると、アクティビティが表示[ `onMembersAdded` されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-132">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="6ce75-133">アプリがインストール [されているチーム内](~/bots/how-to/get-teams-context.md) のチャネルの一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-133">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="6ce75-134">アプリがインストール [されているチームの](~/bots/how-to/get-teams-context.md) メンバーの一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-134">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="6ce75-135">ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-135">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="6ce75-136">情報の取得方法に関係なく、新しい会話を作成するか、またはを保存 `tenantId` `userId` `channelId` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-136">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="6ce75-137">`teamId` を使って、チームの一般チャネルや既定のチャネルに新しい会話スレッドを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-137">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="6ce75-138">これは `userId` 、ボット ID と特定のユーザーに固有です。</span><span class="sxs-lookup"><span data-stu-id="6ce75-138">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="6ce75-139">間のボット `userId` を再利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="6ce75-139">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="6ce75-140">は `channelId` グローバルです。</span><span class="sxs-lookup"><span data-stu-id="6ce75-140">The `channelId` is global.</span></span> <span data-ttu-id="6ce75-141">ただし、チャネルにプロアクティブ メッセージを送信するには、ボットをチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-141">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="6ce75-142">ユーザーまたはチャネル情報を取得した後、会話を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-142">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="6ce75-143">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="6ce75-143">Create the conversation</span></span>

<span data-ttu-id="6ce75-144">会話が存在しない場合、または会話が存在しない場合は、会話を作成する必要があります `conversationId` 。</span><span class="sxs-lookup"><span data-stu-id="6ce75-144">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="6ce75-145">会話は 1 回だけ作成し、値または `conversationId` オブジェクトを格納する必要 `conversationReference` があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-145">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="6ce75-146">会話が作成された後、会話 ID を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-146">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="6ce75-147">会話 ID を取得する</span><span class="sxs-lookup"><span data-stu-id="6ce75-147">Get the conversation ID</span></span>

<span data-ttu-id="6ce75-148">オブジェクトを使用 `conversationReference` するか、 `conversationId` メッセージ `tenantId` を送信します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-148">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="6ce75-149">この ID は、会話を作成するか、そのコンテキストから送信された任意のアクティビティから保存することで取得できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-149">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="6ce75-150">参照用にこの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-150">Store this ID for reference.</span></span>

<span data-ttu-id="6ce75-151">適切なアドレス情報を取得した後、メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-151">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="6ce75-152">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="6ce75-152">Send the message</span></span>

<span data-ttu-id="6ce75-153">SDK を使用している場合は、メソッドを使用し、メッセージを送信するために直接 API 呼び出しを行 `continueConversation` `conversationId` `tenantId` う必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-153">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="6ce75-154">メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-154">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="6ce75-155">プロアクティブ メッセージを送信したので、ユーザーとボット間の情報交換を向上するために、プロアクティブ メッセージを送信しながら、次のベスト プラクティスに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-155">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="6ce75-156">プロアクティブ メッセージングのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="6ce75-156">Best practices for proactive messaging</span></span>

<span data-ttu-id="6ce75-157">ユーザーにプロアクティブ メッセージを送信するのは、ユーザーと効果的なコミュニケーションを行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-157">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="6ce75-158">しかし、ユーザーの視点から、このメッセージはプロンプトが表示されないまま表示されることがあり、ウェルカム メッセージの場合、ユーザーがあなたのアプリと対話するのは初めてのことです。</span><span class="sxs-lookup"><span data-stu-id="6ce75-158">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="6ce75-159">そのため、ユーザーに迷惑メールを送信するのではなく、プロアクティブ メッセージングを使用し、ユーザーがメッセージを受信する理由を理解するのに十分な情報を提供することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="6ce75-159">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="6ce75-160">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="6ce75-160">Welcome messages</span></span>

<span data-ttu-id="6ce75-161">プロアクティブ メッセージングを使用してウェルカム メッセージをユーザーに送信する場合、ユーザーがメッセージを受信する理由に関するコンテキストはありません。</span><span class="sxs-lookup"><span data-stu-id="6ce75-161">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="6ce75-162">また、ユーザーがアプリを操作するのも初めてです。</span><span class="sxs-lookup"><span data-stu-id="6ce75-162">This is also the first time users interact with your app.</span></span> <span data-ttu-id="6ce75-163">良い第一印象を生み出す機会です。</span><span class="sxs-lookup"><span data-stu-id="6ce75-163">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="6ce75-164">最高のウェルカム メッセージには、次のことが必ず含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-164">The best welcome messages must include:</span></span>

* <span data-ttu-id="6ce75-165">ユーザーがメッセージを受信する理由: メッセージを受信する理由は、ユーザーに明確である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-165">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="6ce75-166">ボットがチャネルにインストールされ、すべてのユーザーにウェルカム メッセージを送信した場合は、そのボットがインストールされたチャネルとインストールしたユーザーを通知します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-166">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="6ce75-167">提供する機能: ユーザーは、アプリで実行できる操作と、アプリにどのような値を提供できるのかを特定できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-167">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="6ce75-168">次に実行する操作: ユーザーにコマンドの試用やアプリの操作を招待します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-168">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="6ce75-169">ウェルカム メッセージが不十分な場合、ユーザーがボットをブロックする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-169">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="6ce75-170">ポイントに書き込み、ウェルカム メッセージをクリアします。</span><span class="sxs-lookup"><span data-stu-id="6ce75-170">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="6ce75-171">ウェルカム メッセージが目的の効果を持たない場合は、メッセージを反復処理します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-171">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="6ce75-172">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="6ce75-172">Notification messages</span></span>

<span data-ttu-id="6ce75-173">プロアクティブ メッセージングを使用して通知を送信するには、ユーザーが通知に基づいて一般的なアクションを実行するための明確なパスを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-173">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="6ce75-174">ユーザーが通知を受け取った理由を明確に理解してください。</span><span class="sxs-lookup"><span data-stu-id="6ce75-174">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="6ce75-175">良好な通知メッセージには、通常、次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-175">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="6ce75-176">何が起こったか: 通知の原因を明確に示します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-176">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="6ce75-177">結果は何でした: 通知を発生するために更新されたアイテムを明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-177">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="6ce75-178">誰が、何をトリガーしたのか: 通知の送信を引き起こしたアクションを実行したユーザーまたはアクション。</span><span class="sxs-lookup"><span data-stu-id="6ce75-178">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="6ce75-179">ユーザーが応答で実行できる操作: 通知に基づいてユーザーが簡単にアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-179">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="6ce75-180">ユーザーがオプトアウトする方法: ユーザーが追加の通知をオプトアウトするパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-180">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="6ce75-181">大規模なグループのユーザー (組織など) にメッセージを送信するには、Graph を使用してアプリを事前にインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ce75-181">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="6ce75-182">予定されたメッセージ</span><span class="sxs-lookup"><span data-stu-id="6ce75-182">Scheduled messages</span></span>

<span data-ttu-id="6ce75-183">プロアクティブ メッセージングを使用してスケジュールされたメッセージをユーザーに送信する場合は、タイム ゾーンがタイム ゾーンに更新されるのを確認します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-183">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="6ce75-184">これにより、メッセージが関連する時刻にユーザーに配信されます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-184">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="6ce75-185">通常、スケジュール メッセージには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-185">Schedule messages generally include:</span></span>

* <span data-ttu-id="6ce75-186">**ユーザーがメッセージを受信** する理由 : ユーザーがメッセージを受け取る理由を簡単に理解できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-186">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="6ce75-187">**ユーザーが次に実行できる** 操作: ユーザーは、メッセージの内容に基づいて必要なアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-187">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="6ce75-188">Graph を使用してアプリをプロアクティブにインストール</span><span class="sxs-lookup"><span data-stu-id="6ce75-188">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="6ce75-189">Graph を使用してアプリをプロアクティブにインストールする方法は、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="6ce75-189">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="6ce75-190">アプリを以前にインストールまたは操作していないユーザーにプロアクティブにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-190">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="6ce75-191">たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="6ce75-191">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="6ce75-192">この場合、Graph API を使用して、ユーザー向けアプリをプロアクティブにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-192">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="6ce75-193">インストール時にアプリが受け `conversationUpdate` 取ったイベントから必要な値をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="6ce75-193">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="6ce75-194">組織のアプリ カタログまたは Teams アプリ ストア内のアプリのみをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="6ce75-194">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="6ce75-195">Graph [ドキュメントの「ユーザー向けアプリ](/graph/api/userteamwork-post-installedapps) のインストール」と「Teams with Graph でのプロアクティブ ボットのインストールと [メッセージング」を参照してください](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="6ce75-195">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="6ce75-196">GitHub プラットフォームには[Microsoft .NET framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)もあります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-196">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="6ce75-197">サンプル</span><span class="sxs-lookup"><span data-stu-id="6ce75-197">Samples</span></span>

<span data-ttu-id="6ce75-198">次のコードは、Graph を使用してアプリをプロアクティブにインストールする簡単なコード サンプルを示しています。</span><span class="sxs-lookup"><span data-stu-id="6ce75-198">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="6ce75-199">C#</span><span class="sxs-lookup"><span data-stu-id="6ce75-199">C#</span></span>](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="6ce75-200">TypeScript</span><span class="sxs-lookup"><span data-stu-id="6ce75-200">TypeScript</span></span>](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[<span data-ttu-id="6ce75-201">Python</span><span class="sxs-lookup"><span data-stu-id="6ce75-201">Python</span></span>](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[<span data-ttu-id="6ce75-202">JSON</span><span class="sxs-lookup"><span data-stu-id="6ce75-202">JSON</span></span>](#tab/json)

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

<span data-ttu-id="6ce75-203">ユーザー ID とテナント ID を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ce75-203">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="6ce75-204">呼び出しが成功すると、API は次の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-204">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="6ce75-205">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="6ce75-205">Code sample</span></span>

<span data-ttu-id="6ce75-206">次の表に、Teams アプリケーションに基本的な会話フローを組み込む簡単なコード サンプルと、Teams のチャネルで新しい会話スレッドを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-206">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="6ce75-207">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="6ce75-207">Sample name</span></span>           | <span data-ttu-id="6ce75-208">説明</span><span class="sxs-lookup"><span data-stu-id="6ce75-208">Description</span></span>                                                                      | <span data-ttu-id="6ce75-209">.NET</span><span class="sxs-lookup"><span data-stu-id="6ce75-209">.NET</span></span>    | <span data-ttu-id="6ce75-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="6ce75-210">Node.js</span></span>   | <span data-ttu-id="6ce75-211">Python</span><span class="sxs-lookup"><span data-stu-id="6ce75-211">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="6ce75-212">Teams の会話の基本</span><span class="sxs-lookup"><span data-stu-id="6ce75-212">Teams conversation basics</span></span>  | <span data-ttu-id="6ce75-213">1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-213">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="6ce75-214">View</span><span class="sxs-lookup"><span data-stu-id="6ce75-214">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="6ce75-215">View</span><span class="sxs-lookup"><span data-stu-id="6ce75-215">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="6ce75-216">View</span><span class="sxs-lookup"><span data-stu-id="6ce75-216">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="6ce75-217">チャネルで新しいスレッドを開始する</span><span class="sxs-lookup"><span data-stu-id="6ce75-217">Start new thread in a channel</span></span>     | <span data-ttu-id="6ce75-218">チャネルで新しいスレッドを作成する方法をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="6ce75-218">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="6ce75-219">View</span><span class="sxs-lookup"><span data-stu-id="6ce75-219">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="6ce75-220">View</span><span class="sxs-lookup"><span data-stu-id="6ce75-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="6ce75-221">View</span><span class="sxs-lookup"><span data-stu-id="6ce75-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="6ce75-222">追加のコード サンプル</span><span class="sxs-lookup"><span data-stu-id="6ce75-222">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ce75-223">Teams のプロアクティブ メッセージング コード サンプル</span><span class="sxs-lookup"><span data-stu-id="6ce75-223">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="6ce75-224">次の手順</span><span class="sxs-lookup"><span data-stu-id="6ce75-224">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ce75-225">ボット メッセージの書式設定</span><span class="sxs-lookup"><span data-stu-id="6ce75-225">Format your bot messages</span></span>](~/bots/how-to/format-your-bot-messages.md)
