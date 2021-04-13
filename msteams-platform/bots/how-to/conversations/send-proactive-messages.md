---
title: プロアクティブ メッセージを送信する
description: Microsoft Teams ボットを使用して、プロアクティブメッセージを送信する方法について説明します。
ms.topic: overview
ms.author: anclear
Keywords: メッセージの送信、ユーザー ID の取得、チャネル ID の取得、会話 ID の取得
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654294"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="b8694-104">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="b8694-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="b8694-105">プロアクティブ メッセージとは、ユーザーからのリクエストに直接応答しないボットによって送信されるメッセージのことです。</span><span class="sxs-lookup"><span data-stu-id="b8694-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="b8694-106">これには、次のようなメッセージを含むことができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-106">This can include messages like:</span></span>

* <span data-ttu-id="b8694-107">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="b8694-107">Welcome messages</span></span>
* <span data-ttu-id="b8694-108">通知</span><span class="sxs-lookup"><span data-stu-id="b8694-108">Notifications</span></span>
* <span data-ttu-id="b8694-109">予定されたメッセージ</span><span class="sxs-lookup"><span data-stu-id="b8694-109">Scheduled messages</span></span>

<span data-ttu-id="b8694-110">ボットがプロアクティブ メッセージを送信するには、メッセージを送信したいユーザー、グループ チャット、またはチームにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="b8694-111">グループ チャットやチームの場合は、最初にボットを含むアプリをその場所にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="b8694-112">必要に応じて、チーム内で [Graph を使用してアプリをプロアクティブにインストール](#proactively-install-your-app-using-graph)したり、[アプリ ポリシー](/microsoftteams/teams-custom-app-policies-and-settings)を使用して、テナント内のチームやユーザーにアプリをプッシュしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="b8694-113">ユーザーの場合、自分でアプリをインストールしているか、アプリがインストールされているチームのメンバーである必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="b8694-114">プロアクティブ メッセージを送ることは、通常のメッセージを送ることとは異なります。</span><span class="sxs-lookup"><span data-stu-id="b8694-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="b8694-115">その中で、返信に使うアクティブな `turnContext` はありません。</span><span class="sxs-lookup"><span data-stu-id="b8694-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="b8694-116">また、メッセージを送信する前に会話を作成する必要がある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="b8694-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="b8694-117">たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。</span><span class="sxs-lookup"><span data-stu-id="b8694-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="b8694-118">プロアクティブ メッセージングでは、新しいグループ チャットやチーム内の新しいチャネルを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="b8694-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="b8694-119">大局的には、プロアクティブ メッセージを送信するために完了する必要がある手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b8694-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="b8694-120">[ユーザー ID またはチーム/チャネル ID を取得します](#get-the-user-id-or-teamchannel-id) (必要な場合)。</span><span class="sxs-lookup"><span data-stu-id="b8694-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="b8694-121">[会話または会話スレッドを作成します](#create-the-conversation) (必要な場合)。</span><span class="sxs-lookup"><span data-stu-id="b8694-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="b8694-122">[会話ID を取得します](#get-the-conversation-id)。</span><span class="sxs-lookup"><span data-stu-id="b8694-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="b8694-123">[メッセージを送信します](#send-the-message)。</span><span class="sxs-lookup"><span data-stu-id="b8694-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="b8694-124">[サンプル](#examples)セクションのコード スニペットは、1 対 1 の会話を作成するためのものです。</span><span class="sxs-lookup"><span data-stu-id="b8694-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="b8694-125">1 対 1 の会話とグループやチャネルの両方に向けた完全な作業サンプルへのリンクについては、[コード サンプル](#code-samples)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b8694-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="b8694-126">ユーザー ID またはチーム/チャネル ID を取得する</span><span class="sxs-lookup"><span data-stu-id="b8694-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="b8694-127">チャネルで新しい会話や会話スレッドを作成するには、適切な ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="b8694-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="b8694-128">この ID は複数の方法で受信または取得することができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="b8694-129">アプリが特定のコンテキストでインストールされると、[`onMembersAdded`アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)を受信します。</span><span class="sxs-lookup"><span data-stu-id="b8694-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="b8694-130">アプリがインストールされているコンテキストに新しいユーザーが追加されると、[`onMembersAdded`アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)を受信します。</span><span class="sxs-lookup"><span data-stu-id="b8694-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="b8694-131">アプリがインストールされているチームで[チャネルのリスト](~/bots/how-to/get-teams-context.md)を取得することができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="b8694-132">アプリがインストールされているチームで[メンバー リスト](~/bots/how-to/get-teams-context.md)を取得することができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="b8694-133">ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="b8694-134">情報を取得する方法に関わらず、`tenantId`、`userId`、`channelId` のいずれかを保存しておかないと、新たな会話が作成されません。</span><span class="sxs-lookup"><span data-stu-id="b8694-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="b8694-135">`teamId` を使って、チームの一般チャネルや既定のチャネルに新しい会話スレッドを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="b8694-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="b8694-136">`userId` はあなたのボット ID と特定のユーザーに固有のもので、ボット間で再利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="b8694-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="b8694-137">`channelId` はグローバルですが、チャネルにプロアクティブ メッセージを送信するには、お使いのボットがチームにインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="b8694-138">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="b8694-138">Create the conversation</span></span>

<span data-ttu-id="b8694-139">ユーザーやチャネルの情報を取得した後、既に存在していない場合や `conversationId` が不明である場合は会話を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="b8694-140">会話は一度だけ作成し、今後使用する `conversationId` の値または `conversationReference` のオブジェクトを保存するようにしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="b8694-141">会話 ID を取得する</span><span class="sxs-lookup"><span data-stu-id="b8694-141">Get the conversation ID</span></span>

<span data-ttu-id="b8694-142">会話が作成されたら、`conversationReference` オブジェクト、または `conversationId` と `tenantId` を使用してメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="b8694-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="b8694-143">この ID は、会話を作成するか、そのコンテキストから送信されたアクティビティから保存することで取得することができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="b8694-144">この ID を必ず保存してください。</span><span class="sxs-lookup"><span data-stu-id="b8694-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="b8694-145">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="b8694-145">Send the message</span></span>

<span data-ttu-id="b8694-146">正しいアドレス情報を取得したので、メッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="b8694-147">SDK を使用している場合は `continueConversation` メソッドを使用し、直接 API を呼び出すには `conversationId` と `tenantId` を使用します。</span><span class="sxs-lookup"><span data-stu-id="b8694-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="b8694-148">メッセージを正常に送信するには、`conversationParameters` を正しく設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="b8694-149">[サンプル](#examples)セクションを参照するか、[コード サンプル](#code-samples)セクションに記載されているサンプルの 1 つを使用してください。</span><span class="sxs-lookup"><span data-stu-id="b8694-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="b8694-150">プロアクティブ メッセージングのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="b8694-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="b8694-151">ユーザーにプロアクティブ メッセージを送信するのは、ユーザーと効果的なコミュニケーションを行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b8694-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="b8694-152">しかし、ユーザーの視点から、このメッセージはプロンプトが表示されないまま表示されることがあり、ウェルカム メッセージの場合、ユーザーがあなたのアプリと対話するのは初めてのことです。</span><span class="sxs-lookup"><span data-stu-id="b8694-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="b8694-153">したがって、この機能は頻繁に使用せず、ユーザーにスパムを送らないようにし、ユーザーがメッセージを送信する理由を理解するために十分な情報を提供することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="b8694-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="b8694-154">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="b8694-154">Welcome messages</span></span>

<span data-ttu-id="b8694-155">プロアクティブ メッセージを使用してユーザーにウェルカム メッセージを送信する場合は、メッセージを受信する多くのユーザーにとってメッセージを受信する理由のコンテキストがないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="b8694-156">ユーザーがあなたのアプリと対話するのは初めてであることにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="b8694-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="b8694-157">あなたの第一印象を良くするチャンスです。</span><span class="sxs-lookup"><span data-stu-id="b8694-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="b8694-158">最高のウェルカム メッセージには、次のことが必ず含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="b8694-159">**ユーザがメッセージを受信する理由。**</span><span class="sxs-lookup"><span data-stu-id="b8694-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="b8694-160">メッセージを受信する理由が、ユーザーにとって非常に明確でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="b8694-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="b8694-161">あなたのボットがチャネルにインストールされていて、すべてのユーザーにウェルカム メッセージを送信した場合は、どのチャネルにインストールされ、誰がインストールしたのかを通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="b8694-162">**提示する内容。**</span><span class="sxs-lookup"><span data-stu-id="b8694-162">**What do you offer.**</span></span> <span data-ttu-id="b8694-163">ユーザーはあなたのアプリで何ができるのでしょうか?</span><span class="sxs-lookup"><span data-stu-id="b8694-163">What can they do with your app?</span></span> <span data-ttu-id="b8694-164">ユーザーはどのような価値を得られるのでしょうか?</span><span class="sxs-lookup"><span data-stu-id="b8694-164">What value can you bring to them?</span></span>
* <span data-ttu-id="b8694-165">**ユーザーが次にするべきこと。**</span><span class="sxs-lookup"><span data-stu-id="b8694-165">**What should they do next.**</span></span> <span data-ttu-id="b8694-166">コマンドを試すように招待したり、何らかの方法でアプリと対話したりします。</span><span class="sxs-lookup"><span data-stu-id="b8694-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="b8694-167">ウェルカム メッセージが不十分な場合、ユーザーはあなたのボットをブロックする可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b8694-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="b8694-168">ウェルカム メッセージを作成するのに時間をかけ、望ましい効果が得られない場合は、それを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="b8694-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="b8694-169">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="b8694-169">Notification messages</span></span>

<span data-ttu-id="b8694-170">プロアクティブ メッセージを使用して通知を送信するときは、ユーザーが通知に基づいて一般的な操作を行うための明確な道筋を示し、通知が発生した理由をユーザーに明確に理解させなければなりません。</span><span class="sxs-lookup"><span data-stu-id="b8694-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="b8694-171">優れた通知メッセージには、一般的に以下のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="b8694-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="b8694-172">**何が起こったのですか。**</span><span class="sxs-lookup"><span data-stu-id="b8694-172">**What happened.**</span></span> <span data-ttu-id="b8694-173">何が原因で通知が発生したのかを明確に示しています。</span><span class="sxs-lookup"><span data-stu-id="b8694-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="b8694-174">**結果はどうでしたか。**</span><span class="sxs-lookup"><span data-stu-id="b8694-174">**What was the result.**</span></span> <span data-ttu-id="b8694-175">どのような項目や物事が更新されて通知が発生したのかを明確にしなければなりません。</span><span class="sxs-lookup"><span data-stu-id="b8694-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="b8694-176">**誰が/何がトリガーになったのですか。**</span><span class="sxs-lookup"><span data-stu-id="b8694-176">**Who/what triggered it.**</span></span> <span data-ttu-id="b8694-177">誰が、または何をして、通知を送信されることになったのか。</span><span class="sxs-lookup"><span data-stu-id="b8694-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="b8694-178">**ユーザーが対応できることは何ですか。**</span><span class="sxs-lookup"><span data-stu-id="b8694-178">**What can users do in response.**</span></span> <span data-ttu-id="b8694-179">ユーザーが通知に基づいてアクションを取ることを容易にします。</span><span class="sxs-lookup"><span data-stu-id="b8694-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="b8694-180">**ユーザーがオプトアウトするにはどうすればいいですか。** ユーザーが追加の通知をオプトアウトするためのパスを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="b8694-181">予定されたメッセージ</span><span class="sxs-lookup"><span data-stu-id="b8694-181">Scheduled messages</span></span>

<span data-ttu-id="b8694-182">プロアクティブ メッセージングを使用してスケジュールされたメッセージをユーザーに送信する場合は、タイム ゾーンがタイム ゾーンに更新されるのを確認します。</span><span class="sxs-lookup"><span data-stu-id="b8694-182">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="b8694-183">これにより、メッセージが関連する時刻にユーザーに配信されます。</span><span class="sxs-lookup"><span data-stu-id="b8694-183">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="b8694-184">通常、スケジュール メッセージには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b8694-184">Schedule messages generally include:</span></span>

* <span data-ttu-id="b8694-185">**ユーザーがメッセージを受信** する理由 : ユーザーがメッセージを受け取る理由を簡単に理解できます。</span><span class="sxs-lookup"><span data-stu-id="b8694-185">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="b8694-186">**ユーザーが次に実行できる** 操作: ユーザーは、メッセージの内容に基づいて必要なアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="b8694-186">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="b8694-187">Graph を使用してアプリをプロアクティブにインストール</span><span class="sxs-lookup"><span data-stu-id="b8694-187">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="b8694-188">Microsoft Graph を使用したアプリのプロアクティブ インストールは、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="b8694-188">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="b8694-189">場合によっては、以前にアプリをインストールしていない、またはアプリと対話していないユーザーにプロアクティブにメッセージを送る必要があるかもしれません。</span><span class="sxs-lookup"><span data-stu-id="b8694-189">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="b8694-190">たとえば、[社内コミュニケーター](~/samples/app-templates.md#company-communicator)を使用して、組織全体にメッセージを送信する必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="b8694-190">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="b8694-191">このシナリオでは、Graph API を使用してアプリをユーザーにプロアクティブにインストールし、インストール時にアプリが受信する `conversationUpdate` イベントから必要な値をキャッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="b8694-191">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="b8694-192">組織のアプリ カタログまたは Teams アプリ ストアにあるアプリのみインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b8694-192">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="b8694-193">Graph ドキュメントの「[ユーザー向けアプリのインストール](/graph/api/userteamwork-post-installedapps)」および「[Microsoft Graph を使用した Teams でのプロアクティブ　ボットのインストールとメッセージング](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b8694-193">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="b8694-194">GitHub プラットフォームには[Microsoft .NET framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)もあります。</span><span class="sxs-lookup"><span data-stu-id="b8694-194">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="b8694-195">例</span><span class="sxs-lookup"><span data-stu-id="b8694-195">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b8694-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b8694-196">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="b8694-197">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b8694-197">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="b8694-198">Python</span><span class="sxs-lookup"><span data-stu-id="b8694-198">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="b8694-199">JSON</span><span class="sxs-lookup"><span data-stu-id="b8694-199">JSON</span></span>](#tab/json)

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

<span data-ttu-id="b8694-200">ユーザー ID とテナント ID を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b8694-200">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="b8694-201">呼び出しに成功した場合、API は以下の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="b8694-201">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="b8694-202">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="b8694-202">Code samples</span></span>

<span data-ttu-id="b8694-203">公式プロアクティブ メッセージングのサンプルは以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b8694-203">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="b8694-204">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="b8694-204">Sample Name</span></span>           | <span data-ttu-id="b8694-205">説明</span><span class="sxs-lookup"><span data-stu-id="b8694-205">Description</span></span>                                                                      | <span data-ttu-id="b8694-206">.NET</span><span class="sxs-lookup"><span data-stu-id="b8694-206">.NET</span></span>    | <span data-ttu-id="b8694-207">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8694-207">JavaScript</span></span>   | <span data-ttu-id="b8694-208">Python</span><span class="sxs-lookup"><span data-stu-id="b8694-208">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="b8694-209">Teams での会話の基本</span><span class="sxs-lookup"><span data-stu-id="b8694-209">Teams Conversation Basics</span></span>  | <span data-ttu-id="b8694-210">1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="b8694-210">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="b8694-211">.NET&nbsp;Core</span><span class="sxs-lookup"><span data-stu-id="b8694-211">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="b8694-212">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8694-212">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="b8694-213">Python</span><span class="sxs-lookup"><span data-stu-id="b8694-213">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="b8694-214">チャネルで新しいスレッドを開始する</span><span class="sxs-lookup"><span data-stu-id="b8694-214">Start new thread in a channel</span></span>     | <span data-ttu-id="b8694-215">チャネルで新しいスレッドを作成する方法をご紹介します。</span><span class="sxs-lookup"><span data-stu-id="b8694-215">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="b8694-216">.NET&nbsp;Core</span><span class="sxs-lookup"><span data-stu-id="b8694-216">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="b8694-217">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8694-217">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="b8694-218">Python</span><span class="sxs-lookup"><span data-stu-id="b8694-218">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="b8694-219">その他のコード サンプルを見る</span><span class="sxs-lookup"><span data-stu-id="b8694-219">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b8694-220">**Teams のプロアクティブ メッセージング コード サンプル**</span><span class="sxs-lookup"><span data-stu-id="b8694-220">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
