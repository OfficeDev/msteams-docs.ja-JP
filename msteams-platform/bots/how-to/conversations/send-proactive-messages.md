---
title: プロアクティブ メッセージを送信する
description: Microsoft Teams ボットでプロアクティブ メッセージを送信する方法について説明します。
ms.topic: conceptual
ms.author: anclear
Keywords: メッセージの送信、ユーザー ID の取得、チャネル ID の取得、会話 ID の取得
ms.openlocfilehash: 44e8f3335b7ade4f4a8b1e6192802d932cbd39ed
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995842"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="61837-104">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="61837-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="61837-105">プロアクティブ メッセージとは、ユーザーからの要求に応答しないボットから送信されるメッセージです。</span><span class="sxs-lookup"><span data-stu-id="61837-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="61837-106">これには、次のようなメッセージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="61837-106">This can include messages, such as:</span></span>

* <span data-ttu-id="61837-107">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="61837-107">Welcome messages</span></span>
* <span data-ttu-id="61837-108">通知</span><span class="sxs-lookup"><span data-stu-id="61837-108">Notifications</span></span>
* <span data-ttu-id="61837-109">予定されたメッセージ</span><span class="sxs-lookup"><span data-stu-id="61837-109">Scheduled messages</span></span>

<span data-ttu-id="61837-110">ボットがユーザー、グループ チャット、またはチームにプロアクティブ メッセージを送信するには、そのボットにメッセージを送信するアクセス権が必要です。</span><span class="sxs-lookup"><span data-stu-id="61837-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="61837-111">グループ チャットまたはチームの場合、ボットを含むアプリを最初にその場所にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="61837-112">必要に[応じて、チーム](#proactively-install-your-app-using-graph)に Microsoft Graph を使用してアプリをプロアクティブに[](/microsoftteams/teams-custom-app-policies-and-settings)インストールするか、アプリ ポリシーを使用してテナントのチームとユーザーにアプリをプッシュアウトできます。</span><span class="sxs-lookup"><span data-stu-id="61837-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="61837-113">ユーザーの場合、自分でアプリをインストールしているか、アプリがインストールされているチームのメンバーである必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="61837-114">プロアクティブ メッセージの送信は、通常のメッセージの送信とは異なります。</span><span class="sxs-lookup"><span data-stu-id="61837-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="61837-115">返信に使用 `turnContext` するアクティブはありません。</span><span class="sxs-lookup"><span data-stu-id="61837-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="61837-116">メッセージを送信する前に、会話を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="61837-117">たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。</span><span class="sxs-lookup"><span data-stu-id="61837-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="61837-118">プロアクティブ メッセージングでは、新しいグループ チャットやチーム内の新しいチャネルを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="61837-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="61837-119">**プロアクティブ メッセージを送信するには**</span><span class="sxs-lookup"><span data-stu-id="61837-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="61837-120">[必要に応じて、ユーザー ID、チーム ID、またはチャネル ID](#get-the-user-id-team-id-or-channel-id)を取得します。</span><span class="sxs-lookup"><span data-stu-id="61837-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="61837-121">[必要に応じて、](#create-the-conversation)会話を作成します。</span><span class="sxs-lookup"><span data-stu-id="61837-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="61837-122">[会話ID を取得します](#get-the-conversation-id)。</span><span class="sxs-lookup"><span data-stu-id="61837-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="61837-123">[メッセージを送信します](#send-the-message)。</span><span class="sxs-lookup"><span data-stu-id="61837-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="61837-124">サンプル セクションのコード スニペット [は](#samples) 、1 対 1 の会話を作成するためのコード スニペットです。</span><span class="sxs-lookup"><span data-stu-id="61837-124">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="61837-125">1 対 1 の会話とグループまたはチャネルの両方の作業サンプルを完了するリンクについては、コード サンプルを [参照してください](#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="61837-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code sample](#code-sample).</span></span>

<span data-ttu-id="61837-126">プロアクティブ メッセージを効果的に使用するには、「プロアクティブ [メッセージングのベスト プラクティス」を参照してください](#best-practices-for-proactive-messaging)。</span><span class="sxs-lookup"><span data-stu-id="61837-126">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="61837-127">特定のシナリオでは、Graph を [使用してアプリを事前にインストールする必要があります](#proactively-install-your-app-using-graph)。</span><span class="sxs-lookup"><span data-stu-id="61837-127">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="61837-128">サンプル セクションのコード スニペット [は](#samples) 、1 対 1 の会話を作成するためのコード スニペットです。</span><span class="sxs-lookup"><span data-stu-id="61837-128">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="61837-129">1 対 1 の会話とグループまたはチャネルの両方の完全な作業サンプルについては、コード サンプルを [参照してください](#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="61837-129">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="61837-130">ユーザー ID、チーム ID、またはチャネル ID を取得する</span><span class="sxs-lookup"><span data-stu-id="61837-130">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="61837-131">チャネルに新しいスレッドまたは会話スレッドを作成するには、正しい ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="61837-131">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="61837-132">次の ID を使用して、この ID を受信または取得できます。</span><span class="sxs-lookup"><span data-stu-id="61837-132">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="61837-133">アプリが特定のコンテキストにインストールされている場合は、アクティビティを受信[ `onMembersAdded` します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="61837-133">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="61837-134">アプリがインストールされているコンテキストに新しいユーザーを追加すると、アクティビティが表示[ `onMembersAdded` されます](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="61837-134">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="61837-135">アプリがインストール [されているチーム内](~/bots/how-to/get-teams-context.md) のチャネルの一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="61837-135">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="61837-136">アプリがインストール [されているチームの](~/bots/how-to/get-teams-context.md) メンバーの一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="61837-136">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="61837-137">ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-137">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="61837-138">情報の取得方法に関係なく、新しい会話を作成するか、またはを保存 `tenantId` `userId` `channelId` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-138">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="61837-139">`teamId` を使って、チームの一般チャネルや既定のチャネルに新しい会話スレッドを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="61837-139">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="61837-140">これは `userId` 、ボット ID と特定のユーザーに固有です。</span><span class="sxs-lookup"><span data-stu-id="61837-140">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="61837-141">間のボット `userId` を再利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="61837-141">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="61837-142">は `channelId` グローバルです。</span><span class="sxs-lookup"><span data-stu-id="61837-142">The `channelId` is global.</span></span> <span data-ttu-id="61837-143">ただし、チャネルにプロアクティブ メッセージを送信するには、ボットをチームにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-143">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="61837-144">ユーザーまたはチャネル情報を取得した後、会話を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-144">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="61837-145">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="61837-145">Create the conversation</span></span>

<span data-ttu-id="61837-146">会話が存在しない場合、または会話が存在しない場合は、会話を作成する必要があります `conversationId` 。</span><span class="sxs-lookup"><span data-stu-id="61837-146">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="61837-147">会話は 1 回だけ作成し、値または `conversationId` オブジェクトを格納する必要 `conversationReference` があります。</span><span class="sxs-lookup"><span data-stu-id="61837-147">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="61837-148">会話が作成された後、会話 ID を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-148">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="61837-149">会話 ID を取得する</span><span class="sxs-lookup"><span data-stu-id="61837-149">Get the conversation ID</span></span>

<span data-ttu-id="61837-150">オブジェクトを使用 `conversationReference` するか、 `conversationId` メッセージ `tenantId` を送信します。</span><span class="sxs-lookup"><span data-stu-id="61837-150">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="61837-151">この ID は、会話を作成するか、そのコンテキストから送信された任意のアクティビティから保存することで取得できます。</span><span class="sxs-lookup"><span data-stu-id="61837-151">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="61837-152">参照用にこの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="61837-152">Store this ID for reference.</span></span>

<span data-ttu-id="61837-153">適切なアドレス情報を取得した後、メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="61837-153">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="61837-154">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="61837-154">Send the message</span></span>

<span data-ttu-id="61837-155">正しいアドレス情報を取得したので、メッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="61837-155">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="61837-156">SDK を使用している場合は `continueConversation` メソッドを使用し、直接 API を呼び出すには `conversationId` と `tenantId` を使用します。</span><span class="sxs-lookup"><span data-stu-id="61837-156">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="61837-157">メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-157">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="61837-158">サンプル セクション [を参照](#samples) するか、コード サンプル セクションに記載されているサンプル [のいずれかを使用](#code-sample) します。</span><span class="sxs-lookup"><span data-stu-id="61837-158">See the [samples](#samples) section or use one of the samples listed in the [code sample](#code-sample) section.</span></span>

<span data-ttu-id="61837-159">SDK を使用している場合は、メソッドを使用し、メッセージを送信するために直接 API 呼び出しを行 `continueConversation` `conversationId` `tenantId` う必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-159">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="61837-160">メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-160">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="61837-161">プロアクティブ メッセージを送信したので、ユーザーとボット間の情報交換を向上するために、プロアクティブ メッセージを送信しながら、次のベスト プラクティスに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-161">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="61837-162">プロアクティブ メッセージングのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="61837-162">Best practices for proactive messaging</span></span>

<span data-ttu-id="61837-163">ユーザーにプロアクティブ メッセージを送信するのは、ユーザーと効果的なコミュニケーションを行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="61837-163">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="61837-164">しかし、ユーザーの視点から、このメッセージはプロンプトが表示されないまま表示されることがあり、ウェルカム メッセージの場合、ユーザーがあなたのアプリと対話するのは初めてのことです。</span><span class="sxs-lookup"><span data-stu-id="61837-164">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="61837-165">そのため、ユーザーに迷惑メールを送信するのではなく、プロアクティブ メッセージングを使用し、ユーザーがメッセージを受信する理由を理解するのに十分な情報を提供することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="61837-165">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="61837-166">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="61837-166">Welcome messages</span></span>

<span data-ttu-id="61837-167">プロアクティブ メッセージングを使用してウェルカム メッセージをユーザーに送信する場合、ユーザーがメッセージを受信する理由に関するコンテキストはありません。</span><span class="sxs-lookup"><span data-stu-id="61837-167">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="61837-168">また、ユーザーがアプリを操作するのも初めてです。</span><span class="sxs-lookup"><span data-stu-id="61837-168">This is also the first time users interact with your app.</span></span> <span data-ttu-id="61837-169">良い第一印象を生み出す機会です。</span><span class="sxs-lookup"><span data-stu-id="61837-169">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="61837-170">最高のウェルカム メッセージには、次のことが必ず含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-170">The best welcome messages must include:</span></span>

* <span data-ttu-id="61837-171">ユーザーがメッセージを受信する理由: メッセージを受信する理由は、ユーザーに明確である必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-171">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="61837-172">ボットがチャネルにインストールされ、すべてのユーザーにウェルカム メッセージを送信した場合は、そのボットがインストールされたチャネルとインストールしたユーザーを通知します。</span><span class="sxs-lookup"><span data-stu-id="61837-172">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="61837-173">提供する機能: ユーザーは、アプリで実行できる操作と、アプリにどのような値を提供できるのかを特定できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-173">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="61837-174">次に実行する操作: ユーザーにコマンドの試用やアプリの操作を招待します。</span><span class="sxs-lookup"><span data-stu-id="61837-174">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="61837-175">ウェルカム メッセージが不十分な場合、ユーザーがボットをブロックする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="61837-175">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="61837-176">ポイントに書き込み、ウェルカム メッセージをクリアします。</span><span class="sxs-lookup"><span data-stu-id="61837-176">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="61837-177">ウェルカム メッセージが目的の効果を持たない場合は、メッセージを反復処理します。</span><span class="sxs-lookup"><span data-stu-id="61837-177">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="61837-178">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="61837-178">Notification messages</span></span>

<span data-ttu-id="61837-179">プロアクティブ メッセージングを使用して通知を送信するには、ユーザーが通知に基づいて一般的なアクションを実行するための明確なパスを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-179">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="61837-180">ユーザーが通知を受け取った理由を明確に理解してください。</span><span class="sxs-lookup"><span data-stu-id="61837-180">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="61837-181">良好な通知メッセージには、通常、次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="61837-181">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="61837-182">何が起こったか: 通知の原因を明確に示します。</span><span class="sxs-lookup"><span data-stu-id="61837-182">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="61837-183">結果は何でした: 通知を発生するために更新されたアイテムを明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-183">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="61837-184">誰が、何をトリガーしたのか: 通知の送信を引き起こしたアクションを実行したユーザーまたはアクション。</span><span class="sxs-lookup"><span data-stu-id="61837-184">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="61837-185">ユーザーが応答で実行できる操作: 通知に基づいてユーザーが簡単にアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="61837-185">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="61837-186">ユーザーがオプトアウトする方法: ユーザーが追加の通知をオプトアウトするパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-186">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="61837-187">大規模なグループのユーザー (組織など) にメッセージを送信するには、Graph を使用してアプリを事前にインストールします。</span><span class="sxs-lookup"><span data-stu-id="61837-187">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="61837-188">予定されたメッセージ</span><span class="sxs-lookup"><span data-stu-id="61837-188">Scheduled messages</span></span>

<span data-ttu-id="61837-189">プロアクティブ メッセージングを使用してスケジュールされたメッセージをユーザーに送信する場合は、タイム ゾーンがタイム ゾーンに更新されるのを確認します。</span><span class="sxs-lookup"><span data-stu-id="61837-189">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="61837-190">これにより、メッセージが関連する時刻にユーザーに配信されます。</span><span class="sxs-lookup"><span data-stu-id="61837-190">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="61837-191">通常、スケジュール メッセージには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="61837-191">Schedule messages generally include:</span></span>

* <span data-ttu-id="61837-192">ユーザーがメッセージを受信する理由: ユーザーがメッセージを受け取る理由を簡単に理解できます。</span><span class="sxs-lookup"><span data-stu-id="61837-192">Why is the user receiving the message: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="61837-193">ユーザーが次に実行できる操作: ユーザーは、メッセージの内容に基づいて必要なアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="61837-193">What can user do next: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="61837-194">Graph を使用してアプリをプロアクティブにインストール</span><span class="sxs-lookup"><span data-stu-id="61837-194">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="61837-195">Graph を使用してアプリをプロアクティブにインストールする方法は、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="61837-195">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="61837-196">アプリを以前にインストールまたは操作していないユーザーにプロアクティブにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="61837-196">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="61837-197">たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="61837-197">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="61837-198">この場合、Graph API を使用して、ユーザー向けアプリをプロアクティブにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="61837-198">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="61837-199">インストール時にアプリが受け `conversationUpdate` 取ったイベントから必要な値をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="61837-199">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="61837-200">組織のアプリ カタログまたは Teams アプリ ストア内のアプリのみをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="61837-200">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="61837-201">Graph [ドキュメントの「ユーザー向けアプリ](/graph/api/userteamwork-post-installedapps) のインストール」と「Teams with Graph でのプロアクティブ ボットのインストールと [メッセージング」を参照してください](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="61837-201">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="61837-202">GitHub プラットフォームには[Microsoft .NET framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)もあります。</span><span class="sxs-lookup"><span data-stu-id="61837-202">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="61837-203">サンプル</span><span class="sxs-lookup"><span data-stu-id="61837-203">Samples</span></span>

<span data-ttu-id="61837-204">次のコードは、Graph を使用してアプリをプロアクティブにインストールする簡単なコード サンプルを示しています。</span><span class="sxs-lookup"><span data-stu-id="61837-204">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="61837-205">C#</span><span class="sxs-lookup"><span data-stu-id="61837-205">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="61837-206">TypeScript</span><span class="sxs-lookup"><span data-stu-id="61837-206">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="61837-207">Python</span><span class="sxs-lookup"><span data-stu-id="61837-207">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="61837-208">JSON</span><span class="sxs-lookup"><span data-stu-id="61837-208">JSON</span></span>](#tab/json)

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

<span data-ttu-id="61837-209">ユーザー ID とテナント ID を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61837-209">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="61837-210">呼び出しが成功すると、API は次の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="61837-210">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="61837-211">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="61837-211">Code sample</span></span>

<span data-ttu-id="61837-212">次の表に、Teams アプリケーションに基本的な会話フローを組み込む簡単なコード サンプルと、Teams のチャネルで新しい会話スレッドを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="61837-212">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="61837-213">**サンプルの名前**</span><span class="sxs-lookup"><span data-stu-id="61837-213">**Sample Name**</span></span> | <span data-ttu-id="61837-214">**説明**</span><span class="sxs-lookup"><span data-stu-id="61837-214">**Description**</span></span> | <span data-ttu-id="61837-215">**.NET**</span><span class="sxs-lookup"><span data-stu-id="61837-215">**.NET**</span></span> | <span data-ttu-id="61837-216">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="61837-216">**Node.js**</span></span> | <span data-ttu-id="61837-217">**Python**</span><span class="sxs-lookup"><span data-stu-id="61837-217">**Python**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="61837-218">Teams での会話の基本</span><span class="sxs-lookup"><span data-stu-id="61837-218">Teams Conversation Basics</span></span>  | <span data-ttu-id="61837-219">1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="61837-219">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>| [<span data-ttu-id="61837-220">View</span><span class="sxs-lookup"><span data-stu-id="61837-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="61837-221">View</span><span class="sxs-lookup"><span data-stu-id="61837-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="61837-222">View</span><span class="sxs-lookup"><span data-stu-id="61837-222">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| <span data-ttu-id="61837-223">チャネルで新しいスレッドを開始する</span><span class="sxs-lookup"><span data-stu-id="61837-223">Start new thread in a channel</span></span> | <span data-ttu-id="61837-224">チャネルで新しいスレッドを作成する方法をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="61837-224">Demonstrates creating a new thread in a channel.</span></span> | [<span data-ttu-id="61837-225">View</span><span class="sxs-lookup"><span data-stu-id="61837-225">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="61837-226">View</span><span class="sxs-lookup"><span data-stu-id="61837-226">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="61837-227">View</span><span class="sxs-lookup"><span data-stu-id="61837-227">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="61837-228">追加のコード サンプル</span><span class="sxs-lookup"><span data-stu-id="61837-228">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61837-229">Teams のプロアクティブ メッセージング コード サンプル</span><span class="sxs-lookup"><span data-stu-id="61837-229">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="61837-230">次の手順</span><span class="sxs-lookup"><span data-stu-id="61837-230">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="61837-231">[**Teams のプロアクティブ メッセージング コードサンプル**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
> [ボット メッセージの書式設定](~/bots/how-to/format-your-bot-messages.md)</span><span class="sxs-lookup"><span data-stu-id="61837-231">[**Teams proactive messaging code samples**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
[Format your bot messages](~/bots/how-to/format-your-bot-messages.md)</span></span>
