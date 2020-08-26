---
title: プロアクティブ メッセージを送信する
author: clearab
description: Microsoft Teams bot で予防的なメッセージを送信する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874850"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="70add-103">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="70add-103">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="70add-104">予防的なメッセージとは、ユーザーからの要求に直接応答していない bot によって送信されるメッセージのことです。</span><span class="sxs-lookup"><span data-stu-id="70add-104">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="70add-105">これには、次のようなメッセージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="70add-105">This can include messages like:</span></span>

* <span data-ttu-id="70add-106">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="70add-106">Welcome messages</span></span>
* <span data-ttu-id="70add-107">通知</span><span class="sxs-lookup"><span data-stu-id="70add-107">Notifications</span></span>
* <span data-ttu-id="70add-108">スケジュールされたメッセージ</span><span class="sxs-lookup"><span data-stu-id="70add-108">Scheduled messages</span></span>

<span data-ttu-id="70add-109">Bot が積極的なメッセージを送信するためには、メッセージの送信先のユーザー、グループチャット、またはチームにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-109">In order for your bot to send a proactive message, it must have access to the user, group chat, or team that you wish to send the message to.</span></span> <span data-ttu-id="70add-110">グループチャットまたはチームの場合は、ボットを含むアプリを最初にその場所にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-110">For a group chat or team, this means the app that contains your bot must first be installed to that location.</span></span> <span data-ttu-id="70add-111">必要に応じて、チームで [グラフを使用してアプリを予防的にインストール](#proactively-install-your-app-using-graph) するか、 [アプリポリシー](/microsoftteams/teams-custom-app-policies-and-settings) を使用してテナント内の teams とユーザーにアプリをプッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="70add-111">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team if necessary, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="70add-112">ユーザーの場合は、アプリをそのユーザー用にインストールするか、アプリがインストールされているチームの一部である必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-112">For users, your app either needs to be installed for that user, or your user needs to be part of a team where your app is installed.</span></span>

<span data-ttu-id="70add-113">積極的なメッセージを送信することは、返信に使用するアクティブがない場合に、通常のメッセージを送信することとは異なり `turnContext` ます。</span><span class="sxs-lookup"><span data-stu-id="70add-113">Sending a proactive message is different than sending a regular message in that you won't have an active `turnContext` to use for a reply.</span></span> <span data-ttu-id="70add-114">メッセージを送信する前に、会話 (新しいワンツーワンチャット、チャネル内の新しい会話スレッドなど) を作成する必要がある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="70add-114">You may also need to create the conversation (for example a new one-to-one chat, or a new conversation thread in a channel) before sending the message.</span></span> <span data-ttu-id="70add-115">事前メッセージを使用してチームに新しいグループチャットまたは新しいチャネルを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="70add-115">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="70add-116">プロアクティブなメッセージを送信するには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-116">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="70add-117">[ユーザー id またはチーム/チャネル ID を取得](#get-the-user-id-or-teamchannel-id) します (必要な場合)。</span><span class="sxs-lookup"><span data-stu-id="70add-117">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="70add-118">[会話スレッドまたは会話スレッドを作成](#create-the-conversation) します (必要な場合)。</span><span class="sxs-lookup"><span data-stu-id="70add-118">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="70add-119">[会話 ID を取得](#get-the-conversation-id)します。</span><span class="sxs-lookup"><span data-stu-id="70add-119">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="70add-120">[メッセージを送信](#send-the-message)します。</span><span class="sxs-lookup"><span data-stu-id="70add-120">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="70add-121">1対1の会話を作成するには、以下の「 [例](#examples) 」セクションのコードスニペットを参照してください。1対1の会話とグループ/チャネルの両方に対して作業用のサンプルを完全に実行するには、「 [参照](#references) 」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="70add-121">The code snippets in the [examples](#examples) section below are for creating a one-to-one conversation, see the [references](#references) section for links to complete working samples for both one-to-once conversations and group/channels.</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="70add-122">ユーザー ID またはチーム/チャネル ID を取得する</span><span class="sxs-lookup"><span data-stu-id="70add-122">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="70add-123">チャネルで新しい会話スレッドまたは会話スレッドを作成する必要がある場合は、最初に会話を作成するための適切な ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="70add-123">If you need to create a new conversation or conversation thread in a channel you'll first need the right ID to create the conversation.</span></span> <span data-ttu-id="70add-124">この ID を取得または取得するには、複数の方法があります。</span><span class="sxs-lookup"><span data-stu-id="70add-124">You can receive/retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="70add-125">アプリが特定のコンテキストでインストールされている場合は、 [ `onMembersAdded` アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)が表示されます。</span><span class="sxs-lookup"><span data-stu-id="70add-125">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="70add-126">アプリがインストールされているコンテキストに新しいユーザーが追加されると、 [ `onMembersAdded` アクティビティ](~/bots/how-to/conversations/subscribe-to-conversation-events.md)が表示されます。</span><span class="sxs-lookup"><span data-stu-id="70add-126">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="70add-127">アプリがインストールされているチーム内の [チャネルの一覧](~/bots/how-to/get-teams-context.md) を取得できます。</span><span class="sxs-lookup"><span data-stu-id="70add-127">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="70add-128">アプリがインストールされているチームの [メンバーの一覧](~/bots/how-to/get-teams-context.md) を取得できます。</span><span class="sxs-lookup"><span data-stu-id="70add-128">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="70add-129">お客様が受け取るすべてのアクティビティに必要な情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="70add-129">Every Activity your bot receives will contain the necessary information.</span></span>

<span data-ttu-id="70add-130">情報を取得する方法に関係なく、 `tenantId` `userId` 新しい会話を作成するために、とのどちらか一方またはを格納する必要があり `channelId` ます。</span><span class="sxs-lookup"><span data-stu-id="70add-130">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` in order to create a new conversation.</span></span> <span data-ttu-id="70add-131">を使用して、 `teamId` チームの一般または既定のチャネルに新しい会話スレッドを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="70add-131">You can also use the `teamId` to create a new conversation thread in the general/default channel of a team.</span></span>

<span data-ttu-id="70add-132">は `userId` Bot Id と特定のユーザーに固有のものであり、ボット間で使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="70add-132">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="70add-133">`channelId`はグローバルですが、積極的なメッセージをチャネルに送信する前に、その bot をチームにインストールする_必要があり_ます。</span><span class="sxs-lookup"><span data-stu-id="70add-133">The `channelId` is global, however your bot _must_ be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="70add-134">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="70add-134">Create the conversation</span></span>

<span data-ttu-id="70add-135">ユーザー/チャネル情報を取得したら、会話を作成する必要があります (または、不明な場合 `conversationId` )。</span><span class="sxs-lookup"><span data-stu-id="70add-135">Once you have the user/channel information, you'll need to create the conversation if it doesn't already exist (or you don't know the `conversationId`).</span></span> <span data-ttu-id="70add-136">会話を作成するのは1回だけにしてください。 `conversationId` 今後使用する値またはオブジェクトを保存してください `conversationReference` 。</span><span class="sxs-lookup"><span data-stu-id="70add-136">You should only create the conversation once; make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="70add-137">会話 ID を取得する</span><span class="sxs-lookup"><span data-stu-id="70add-137">Get the conversation ID</span></span>

<span data-ttu-id="70add-138">会話が作成されたら、オブジェクトまたはを使用して `conversationReference` `conversationId` メッセージを送信し `tenantId` ます。</span><span class="sxs-lookup"><span data-stu-id="70add-138">Once the conversation has been created, you will use either the `conversationReference` object or the `conversationId` and the `tenantId` to send the message.</span></span> <span data-ttu-id="70add-139">この Id は、会話を作成するか、そのコンテキストから送信されたすべてのアクティビティから保存することによって取得できます。</span><span class="sxs-lookup"><span data-stu-id="70add-139">You can get this Id by either creating the conversation, or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="70add-140">この Id が格納されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="70add-140">Make certain that you store this Id.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="70add-141">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="70add-141">Send the message</span></span>

<span data-ttu-id="70add-142">これで、適切な住所情報が得られたので、メッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="70add-142">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="70add-143">SDK を使用している場合は、メソッドを使用して、 `continueConversation` およびを `conversationId` 直接 API 呼び出しを行うようにし `tenantId` ます。</span><span class="sxs-lookup"><span data-stu-id="70add-143">If you're using the SDK, you'll do so using the `continueConversation` method,and the `conversationId` and `tenantId` to make a direct API call.</span></span>  <span data-ttu-id="70add-144">メッセージを正常に送信するには、適切に設定する必要があり `conversationParameters` ます。以下の [例](#examples) を参照するか、「 [参照](#references) 」セクションに記載されているサンプルのいずれかを使用してください。</span><span class="sxs-lookup"><span data-stu-id="70add-144">You'll need to set the `conversationParameters` correctly to successfully send your message - see the [examples](#examples) below or use one of the samples listed in the [references](#references) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="70add-145">事前メッセージのベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="70add-145">Best practices for proactive messaging</span></span>

<span data-ttu-id="70add-146">事前にメッセージをユーザーに送信することは、ユーザーとの通信に非常に効果的な方法となります。</span><span class="sxs-lookup"><span data-stu-id="70add-146">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="70add-147">ただし、このメッセージは完全に表示されないように表示されるため、ウェルカムメッセージの場合はアプリを初めて操作したときになります。</span><span class="sxs-lookup"><span data-stu-id="70add-147">However, from their perspective this message can appear completely unprompted and, in the case of welcome messages, it will be the first time they've interacted with your app.</span></span> <span data-ttu-id="70add-148">そのため、この機能を多用しない (ユーザーにスパムを行わない) ことと、ユーザーが伝達されている理由をユーザーが理解できる情報を提供することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="70add-148">As such, it is very important to use this functionality sparingly (don't spam your users) and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="70add-149">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="70add-149">Welcome messages</span></span>

<span data-ttu-id="70add-150">事前メッセージを使用して、ユーザーにウェルカムメッセージを送信する場合は、メッセージを受信する多くのユーザーにとって、そのメッセージを受信する理由のコンテキストはないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="70add-150">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there will be no context for why they are receiving it.</span></span> <span data-ttu-id="70add-151">これは、アプリを初めて使用したときにも使用されます。最初の印象を得ることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="70add-151">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="70add-152">推奨されるウェルカムメッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="70add-152">The best welcome messages will include:</span></span>

* <span data-ttu-id="70add-153">**ユーザーがメッセージを受信する理由。**</span><span class="sxs-lookup"><span data-stu-id="70add-153">**Why a user is receiving the message.**</span></span> <span data-ttu-id="70add-154">ユーザーがメッセージを受信する理由を明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-154">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="70add-155">Bot がチャネルにインストールされていて、すべてのユーザーにウェルカムメッセージを送信した場合は、インストールされているチャネルと、インストールされている可能性のあるチャネルを知らせます。</span><span class="sxs-lookup"><span data-stu-id="70add-155">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="70add-156">**何を提供するか。**</span><span class="sxs-lookup"><span data-stu-id="70add-156">**What do you offer.**</span></span> <span data-ttu-id="70add-157">アプリでできること</span><span class="sxs-lookup"><span data-stu-id="70add-157">What can they do with your app?</span></span> <span data-ttu-id="70add-158">どのような値にすることができますか。</span><span class="sxs-lookup"><span data-stu-id="70add-158">What value can you bring to them?</span></span>
* <span data-ttu-id="70add-159">**次の手順を実行します。**</span><span class="sxs-lookup"><span data-stu-id="70add-159">**What should they do next.**</span></span> <span data-ttu-id="70add-160">コマンドを試したり、何らかの方法でアプリを操作したりするように招待します。</span><span class="sxs-lookup"><span data-stu-id="70add-160">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="70add-161">重要ではないウェルカムメッセージは、ユーザーが bot をブロックする可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="70add-161">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="70add-162">ウェルカムメッセージの作成には、十分な時間を費やす必要があります。また、必要な効果を持っていない場合は、それらに対して反復処理を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-162">You should spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="70add-163">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="70add-163">Notification messages</span></span>

<span data-ttu-id="70add-164">事前メッセージを使用して通知を送信する場合は、ユーザーが通知に基づいて一般的な操作を実行するための明確なパスを持っていることと、通知が発生した理由を明確に理解していることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-164">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="70add-165">適切な通知メッセージには、通常次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="70add-165">Good notification messages will generally include:</span></span>

* <span data-ttu-id="70add-166">**どうしたのですか。**</span><span class="sxs-lookup"><span data-stu-id="70add-166">**What happened.**</span></span> <span data-ttu-id="70add-167">通知を発生させた理由を明確に示します。</span><span class="sxs-lookup"><span data-stu-id="70add-167">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="70add-168">**結果は何ですか。**</span><span class="sxs-lookup"><span data-stu-id="70add-168">**What was the result.**</span></span> <span data-ttu-id="70add-169">通知を発生させるためにアイテムまたはアイテムが更新されたことを明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-169">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="70add-170">**誰がトリガーしたか。**</span><span class="sxs-lookup"><span data-stu-id="70add-170">**Who/what triggered it.**</span></span> <span data-ttu-id="70add-171">通知が送信された原因となった操作を実行したユーザーまたは対象。</span><span class="sxs-lookup"><span data-stu-id="70add-171">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="70add-172">**ユーザーが応答で実行できること。**</span><span class="sxs-lookup"><span data-stu-id="70add-172">**What can users do in response.**</span></span> <span data-ttu-id="70add-173">ユーザーが通知に基づいて操作を簡単に実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="70add-173">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="70add-174">**ユーザーはどのようにして脱退できますか。** ユーザーが追加の通知をオプトアウトするためのパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-174">**How can users opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="70add-175">Graph を使用してアプリを事前にインストールする</span><span class="sxs-lookup"><span data-stu-id="70add-175">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="70add-176">Microsoft Graph を使用してアプリを事前にインストールするのは、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="70add-176">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="70add-177">場合によっては、既にインストールされていない、またはアプリと対話していないメッセージユーザーを予防的に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-177">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="70add-178">たとえば、 [会社の communicator](~/samples/app-templates.md#company-communicator) を使用して組織全体にメッセージを送信するとします。</span><span class="sxs-lookup"><span data-stu-id="70add-178">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="70add-179">このシナリオでは、Graph API を使用して、ユーザー用のアプリを事前にインストールし、 `conversationUpdate` インストール時にアプリが受け取るイベントから必要な値をキャッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="70add-179">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="70add-180">組織のアプリカタログまたは Teams アプリストアにあるアプリのみをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="70add-180">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="70add-181">[Microsoft graph を使用する Teams で](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)は、graph のドキュメントの「[ユーザー用アプリのインストール](/graph/teams-proactive-messaging)」および「事前のボットのインストールとメッセージング」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="70add-181">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="70add-182">GitHub プラットフォームには、 [Microsoft .net framework サンプル](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  もあります。</span><span class="sxs-lookup"><span data-stu-id="70add-182">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="70add-183">例</span><span class="sxs-lookup"><span data-stu-id="70add-183">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="70add-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="70add-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="70add-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="70add-185">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="70add-186">Python</span><span class="sxs-lookup"><span data-stu-id="70add-186">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="70add-187">JSON</span><span class="sxs-lookup"><span data-stu-id="70add-187">JSON</span></span>](#tab/json)

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

<span data-ttu-id="70add-188">ユーザー ID とテナント ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70add-188">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="70add-189">呼び出しが成功すると、API は次の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="70add-189">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="references"></a><span data-ttu-id="70add-190">関連情報</span><span class="sxs-lookup"><span data-stu-id="70add-190">References</span></span>

<span data-ttu-id="70add-191">以下に、公式な予防的なメッセージングサンプルを示します。</span><span class="sxs-lookup"><span data-stu-id="70add-191">The official proactive messaging samples are listed below.</span></span>

|  <span data-ttu-id="70add-192">いいえ。</span><span class="sxs-lookup"><span data-stu-id="70add-192">No.</span></span>  | <span data-ttu-id="70add-193">サンプル名</span><span class="sxs-lookup"><span data-stu-id="70add-193">Sample Name</span></span>           | <span data-ttu-id="70add-194">説明</span><span class="sxs-lookup"><span data-stu-id="70add-194">Description</span></span>                                                                      | <span data-ttu-id="70add-195">.NET</span><span class="sxs-lookup"><span data-stu-id="70add-195">.NET</span></span>    | <span data-ttu-id="70add-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="70add-196">JavaScript</span></span>   | <span data-ttu-id="70add-197">Python</span><span class="sxs-lookup"><span data-stu-id="70add-197">Python</span></span>  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="70add-198">57</span><span class="sxs-lookup"><span data-stu-id="70add-198">57</span></span>|<span data-ttu-id="70add-199">Teams の会話の基礎</span><span class="sxs-lookup"><span data-stu-id="70add-199">Teams Conversation Basics</span></span>  | <span data-ttu-id="70add-200">1対1の事前メッセージを送信するなど、Teams での会話の基本を示します。</span><span class="sxs-lookup"><span data-stu-id="70add-200">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="70add-201">.NET &nbsp; コア</span><span class="sxs-lookup"><span data-stu-id="70add-201">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="70add-202">JavaScript</span><span class="sxs-lookup"><span data-stu-id="70add-202">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="70add-203">Python</span><span class="sxs-lookup"><span data-stu-id="70add-203">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="70add-204">58</span><span class="sxs-lookup"><span data-stu-id="70add-204">58</span></span>|<span data-ttu-id="70add-205">チャネルで新しいスレッドを開始する</span><span class="sxs-lookup"><span data-stu-id="70add-205">Start new thread in a channel</span></span>     | <span data-ttu-id="70add-206">チャネルに新しいスレッドを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="70add-206">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="70add-207">.NET &nbsp; コア</span><span class="sxs-lookup"><span data-stu-id="70add-207">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="70add-208">JavaScript</span><span class="sxs-lookup"><span data-stu-id="70add-208">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="70add-209">Python</span><span class="sxs-lookup"><span data-stu-id="70add-209">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

<span data-ttu-id="70add-210">次の例は、(オブジェクトを使用せずに) 事前にメッセージを送信するために必要な最小限の情報を示して `conversationReference` います。</span><span class="sxs-lookup"><span data-stu-id="70add-210">The sample below demonstrates the minimal amount of information needed to send a proactive message (without using a `conversationReference` object).</span></span> <span data-ttu-id="70add-211">このサンプルは、REST API 呼び出しを直接使用している場合や、完全なオブジェクトが格納されていない場合に役立ち `conversationReference` ます。</span><span class="sxs-lookup"><span data-stu-id="70add-211">This sample can be useful if you're using REST API calls directly, or haven't been storing full `conversationReference` objects.</span></span>

* [<span data-ttu-id="70add-212">Teams の予防的なメッセージング</span><span class="sxs-lookup"><span data-stu-id="70add-212">Teams Proactive Messaging</span></span>](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a><span data-ttu-id="70add-213">その他のコードを表示する</span><span class="sxs-lookup"><span data-stu-id="70add-213">View additional code</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="70add-214">**Teams の予防的なメッセージングコードサンプル**</span><span class="sxs-lookup"><span data-stu-id="70add-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>