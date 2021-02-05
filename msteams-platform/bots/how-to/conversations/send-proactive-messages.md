---
title: プロアクティブ メッセージを送信する
description: は、Microsoft Teams ボットでプロアクティブ メッセージを送信する方法について説明します。
ms.topic: overview
ms.author: anclear
Keywords: ユーザー ID チャネル ID 会話 ID を取得するメッセージを送信する
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103606"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="037dd-104">プロアクティブ メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="037dd-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="037dd-105">プロアクティブ メッセージとは、ユーザーからの要求に直接応答しないボットによって送信されるメッセージです。</span><span class="sxs-lookup"><span data-stu-id="037dd-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="037dd-106">これには、次のようなメッセージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="037dd-106">This can include messages like:</span></span>

* <span data-ttu-id="037dd-107">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="037dd-107">Welcome messages</span></span>
* <span data-ttu-id="037dd-108">通知</span><span class="sxs-lookup"><span data-stu-id="037dd-108">Notifications</span></span>
* <span data-ttu-id="037dd-109">スケジュールされたメッセージ</span><span class="sxs-lookup"><span data-stu-id="037dd-109">Scheduled messages</span></span>

<span data-ttu-id="037dd-110">ボットがプロアクティブ メッセージを送信するには、メッセージを送信するユーザー、グループ チャット、またはチームにアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="037dd-111">グループ チャットまたはチームの場合は、ボットを含むアプリを最初にその場所にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="037dd-112">必要に[応じて、Graph](#proactively-install-your-app-using-graph)を使用してアプリを事前にチームにインストールするか[](/microsoftteams/teams-custom-app-policies-and-settings)、アプリ ポリシーを使用してテナント内のチームとユーザーにアプリをプッシュできます。</span><span class="sxs-lookup"><span data-stu-id="037dd-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="037dd-113">ユーザーの場合は、ユーザー用にアプリをインストールするか、アプリがインストールされているチームの一部である必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="037dd-114">プロアクティブ メッセージの送信は、通常のメッセージの送信とは異なります。</span><span class="sxs-lookup"><span data-stu-id="037dd-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="037dd-115">その場合、返信に使用 `turnContext` するアクティブはありません。</span><span class="sxs-lookup"><span data-stu-id="037dd-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="037dd-116">メッセージを送信する前に会話を作成する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="037dd-117">たとえば、新しい 1 対 1 のチャットやチャネル内の新しい会話スレッドなどです。</span><span class="sxs-lookup"><span data-stu-id="037dd-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="037dd-118">プロアクティブ メッセージングを使用するチームで、新しいグループ チャットや新しいチャネルを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="037dd-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="037dd-119">プロアクティブ メッセージを送信するために完了する必要がある手順の大きなレベルは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="037dd-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="037dd-120">[ユーザー ID またはチーム/チャネル ID を取得します](#get-the-user-id-or-teamchannel-id) (必要な場合)。</span><span class="sxs-lookup"><span data-stu-id="037dd-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="037dd-121">[会話または会話スレッドを作成します](#create-the-conversation) (必要な場合)。</span><span class="sxs-lookup"><span data-stu-id="037dd-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="037dd-122">[会話 ID を取得します](#get-the-conversation-id)。</span><span class="sxs-lookup"><span data-stu-id="037dd-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="037dd-123">[メッセージを送信します](#send-the-message)。</span><span class="sxs-lookup"><span data-stu-id="037dd-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="037dd-124">例セクションのコード [スニペットは](#examples) 、1 対 1 の会話を作成するためのスニペットです。</span><span class="sxs-lookup"><span data-stu-id="037dd-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="037dd-125">1 対 1 の会話とグループまたはチャネルの両方の作業サンプルを完了するリンクについては、コード サンプルを [参照してください](#code-samples)。</span><span class="sxs-lookup"><span data-stu-id="037dd-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="037dd-126">ユーザー ID またはチーム/チャネル ID を取得する</span><span class="sxs-lookup"><span data-stu-id="037dd-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="037dd-127">チャネルで新しい会話または会話スレッドを作成するには、正しい ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="037dd-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="037dd-128">この ID は、次の複数の方法で受信または取得できます。</span><span class="sxs-lookup"><span data-stu-id="037dd-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="037dd-129">アプリが特定のコンテキストでインストールされている場合、アクティビティを受信[ `onMembersAdded` します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="037dd-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="037dd-130">アプリがインストールされているコンテキストに新しいユーザーが追加された場合、アクティビティを受信[ `onMembersAdded` します](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="037dd-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="037dd-131">アプリがインストール [されているチーム内の](~/bots/how-to/get-teams-context.md) チャネルの一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="037dd-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="037dd-132">アプリがインストール [されているチームの](~/bots/how-to/get-teams-context.md) メンバーの一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="037dd-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="037dd-133">ボットが受け取るすべてのアクティビティには、必要な情報が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="037dd-134">情報を取得する方法に関係なく、新しい会話を保存するか、新しい会話を作成 `tenantId` `userId` `channelId` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="037dd-135">また、チームの一 `teamId` 般的なチャネルまたは既定のチャネルで新しい会話スレッドを作成するためにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="037dd-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="037dd-136">ボット ID と特定のユーザーに対して一意であり、ボット間 `userId` で再使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="037dd-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="037dd-137">グローバルですが、チャネルにプロアクティブ メッセージを送信する前に、ボットをチームに `channelId` インストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="037dd-138">会話を作成する</span><span class="sxs-lookup"><span data-stu-id="037dd-138">Create the conversation</span></span>

<span data-ttu-id="037dd-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId` .</span><span class="sxs-lookup"><span data-stu-id="037dd-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="037dd-140">会話は 1 回だけ作成し、将来使用する値またはオブジェクト `conversationId` `conversationReference` を保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="037dd-141">会話 ID を取得する</span><span class="sxs-lookup"><span data-stu-id="037dd-141">Get the conversation ID</span></span>

<span data-ttu-id="037dd-142">会話が作成された後、オブジェクトを使用 `conversationReference` するか、メッセージ `conversationId` を `tenantId` 送信します。</span><span class="sxs-lookup"><span data-stu-id="037dd-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="037dd-143">この ID は、会話を作成するか、そのコンテキストから送信されたアクティビティから保存することで取得できます。</span><span class="sxs-lookup"><span data-stu-id="037dd-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="037dd-144">この ID を保存してください。</span><span class="sxs-lookup"><span data-stu-id="037dd-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="037dd-145">メッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="037dd-145">Send the message</span></span>

<span data-ttu-id="037dd-146">適切なアドレス情報が得たので、メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="037dd-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="037dd-147">SDK を使用している場合は、メソッドを使用して直接 API 呼び出しを行 `continueConversation` `conversationId` `tenantId` います。</span><span class="sxs-lookup"><span data-stu-id="037dd-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="037dd-148">メッセージを正常に `conversationParameters` 送信するには、正しく設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="037dd-149">例の [セクションを参照](#examples) するか、コード サンプル セクションに記載されているサンプル [のいずれかを使用](#code-samples) してください。</span><span class="sxs-lookup"><span data-stu-id="037dd-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="037dd-150">プロアクティブ メッセージングのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="037dd-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="037dd-151">プロアクティブ メッセージをユーザーに送信する方法は、ユーザーと通信するための非常に効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="037dd-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="037dd-152">ただし、ユーザーの観点からは、このメッセージは完全に処理されていないと表示される可能性があります。ウェルカム メッセージの場合は、アプリを初めて操作します。</span><span class="sxs-lookup"><span data-stu-id="037dd-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="037dd-153">したがって、この機能は、ユーザーに迷惑メールを送信し、メッセージが送信される理由をユーザーが理解するのに十分な情報を提供するために、この機能を使用することが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="037dd-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="037dd-154">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="037dd-154">Welcome messages</span></span>

<span data-ttu-id="037dd-155">プロアクティブ メッセージングを使用してユーザーにウェルカム メッセージを送信する場合、メッセージを受信するほとんどのユーザーに対して、メッセージを受信する理由に関するコンテキストがないという念頭に置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="037dd-156">これは、ユーザーがアプリを初めて操作する場合にも行います。</span><span class="sxs-lookup"><span data-stu-id="037dd-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="037dd-157">第一印象を良くする機会です。</span><span class="sxs-lookup"><span data-stu-id="037dd-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="037dd-158">最適なウェルカム メッセージには、次のものが含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="037dd-159">**ユーザーがメッセージを受信する理由。**</span><span class="sxs-lookup"><span data-stu-id="037dd-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="037dd-160">ユーザーがメッセージを受信する理由は非常に明確である必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="037dd-161">ボットがチャネルにインストールされ、すべてのユーザーにウェルカム メッセージを送信した場合は、ボットがインストールされているチャネルと、インストールされている可能性のあるユーザーを知らせる必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="037dd-162">**何を提供します。**</span><span class="sxs-lookup"><span data-stu-id="037dd-162">**What do you offer.**</span></span> <span data-ttu-id="037dd-163">アプリで何ができるか。</span><span class="sxs-lookup"><span data-stu-id="037dd-163">What can they do with your app?</span></span> <span data-ttu-id="037dd-164">どのような価値を持ち込むか。</span><span class="sxs-lookup"><span data-stu-id="037dd-164">What value can you bring to them?</span></span>
* <span data-ttu-id="037dd-165">**次に何を行う必要があります。**</span><span class="sxs-lookup"><span data-stu-id="037dd-165">**What should they do next.**</span></span> <span data-ttu-id="037dd-166">コマンドを試したり、何らかの方法でアプリを操作したりします。</span><span class="sxs-lookup"><span data-stu-id="037dd-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="037dd-167">ウェルカム メッセージが不十分な場合は、ユーザーがボットをブロックする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="037dd-168">ウェルカム メッセージの作成に十分な時間を費やし、望ましい効果が得ない場合は繰り返します。</span><span class="sxs-lookup"><span data-stu-id="037dd-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="037dd-169">通知メッセージ</span><span class="sxs-lookup"><span data-stu-id="037dd-169">Notification messages</span></span>

<span data-ttu-id="037dd-170">プロアクティブ メッセージングを使用して通知を送信する場合は、通知に基づいて共通のアクションを実行するための明確なパスと、通知が発生した理由を明確に理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="037dd-171">通常、良好な通知メッセージには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="037dd-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="037dd-172">**どうしたのですか。**</span><span class="sxs-lookup"><span data-stu-id="037dd-172">**What happened.**</span></span> <span data-ttu-id="037dd-173">通知の原因を明確に示します。</span><span class="sxs-lookup"><span data-stu-id="037dd-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="037dd-174">**結果は何でしたか。**</span><span class="sxs-lookup"><span data-stu-id="037dd-174">**What was the result.**</span></span> <span data-ttu-id="037dd-175">通知を発生するために更新されたアイテムまたはアイテムを明確に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="037dd-176">**誰が何をトリガーしたのか。**</span><span class="sxs-lookup"><span data-stu-id="037dd-176">**Who/what triggered it.**</span></span> <span data-ttu-id="037dd-177">通知の送信を引き起こしたアクションを実行したユーザーまたはアクション。</span><span class="sxs-lookup"><span data-stu-id="037dd-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="037dd-178">**ユーザーが応答で実行できる操作。**</span><span class="sxs-lookup"><span data-stu-id="037dd-178">**What can users do in response.**</span></span> <span data-ttu-id="037dd-179">通知に基づいてユーザーが簡単にアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="037dd-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="037dd-180">**ユーザーがオプトアウトする方法。** ユーザーが追加の通知をオプトアウトするパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="037dd-181">Graph を使用してアプリを事前にインストールする</span><span class="sxs-lookup"><span data-stu-id="037dd-181">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="037dd-182">Microsoft Graph を使用してアプリを事前にインストールする機能は、現在ベータ版です。</span><span class="sxs-lookup"><span data-stu-id="037dd-182">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="037dd-183">以前にアプリをインストールまたは操作していないユーザーに事前にメッセージを送信する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-183">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="037dd-184">たとえば、会社のコミュニケーター [を使用](~/samples/app-templates.md#company-communicator) して組織全体にメッセージを送信する場合です。</span><span class="sxs-lookup"><span data-stu-id="037dd-184">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="037dd-185">このシナリオでは、Graph API を使用してユーザー用のアプリを事前にインストールし、インストール時にアプリが受け取ったイベントから必要な値を `conversationUpdate` キャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="037dd-185">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="037dd-186">組織のアプリ カタログまたは Teams アプリ ストアにあるアプリのみをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="037dd-186">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="037dd-187">Graph [ドキュメントのユーザー向けアプリの](/graph/api/userteamwork-post-installedapps) インストールと、Microsoft Graph を使用した Teams でのプロアクティブ ボットのインストール [とメッセージングに関するページをご覧ください](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="037dd-187">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="037dd-188">GitHub プラットフォーム [には、Microsoft .NET フレームワーク](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) のサンプルも用意されています。</span><span class="sxs-lookup"><span data-stu-id="037dd-188">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="037dd-189">例</span><span class="sxs-lookup"><span data-stu-id="037dd-189">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="037dd-190">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="037dd-190">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="037dd-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="037dd-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="037dd-192">Python</span><span class="sxs-lookup"><span data-stu-id="037dd-192">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="037dd-193">JSON</span><span class="sxs-lookup"><span data-stu-id="037dd-193">JSON</span></span>](#tab/json)

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

<span data-ttu-id="037dd-194">ユーザー ID とテナント ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="037dd-194">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="037dd-195">呼び出しが成功すると、API は次の応答オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="037dd-195">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="037dd-196">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="037dd-196">Code samples</span></span>

<span data-ttu-id="037dd-197">公式のプロアクティブ メッセージングのサンプルは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="037dd-197">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="037dd-198">サンプル名</span><span class="sxs-lookup"><span data-stu-id="037dd-198">Sample Name</span></span>           | <span data-ttu-id="037dd-199">説明</span><span class="sxs-lookup"><span data-stu-id="037dd-199">Description</span></span>                                                                      | <span data-ttu-id="037dd-200">.NET</span><span class="sxs-lookup"><span data-stu-id="037dd-200">.NET</span></span>    | <span data-ttu-id="037dd-201">JavaScript</span><span class="sxs-lookup"><span data-stu-id="037dd-201">JavaScript</span></span>   | <span data-ttu-id="037dd-202">Python</span><span class="sxs-lookup"><span data-stu-id="037dd-202">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="037dd-203">Teams 会話の基本</span><span class="sxs-lookup"><span data-stu-id="037dd-203">Teams Conversation Basics</span></span>  | <span data-ttu-id="037dd-204">1 対 1 のプロアクティブ メッセージの送信など、Teams での会話の基本を示します。</span><span class="sxs-lookup"><span data-stu-id="037dd-204">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="037dd-205">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="037dd-205">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="037dd-206">JavaScript</span><span class="sxs-lookup"><span data-stu-id="037dd-206">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="037dd-207">Python</span><span class="sxs-lookup"><span data-stu-id="037dd-207">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="037dd-208">チャネルで新しいスレッドを開始する</span><span class="sxs-lookup"><span data-stu-id="037dd-208">Start new thread in a channel</span></span>     | <span data-ttu-id="037dd-209">チャネルで新しいスレッドを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="037dd-209">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="037dd-210">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="037dd-210">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="037dd-211">JavaScript</span><span class="sxs-lookup"><span data-stu-id="037dd-211">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="037dd-212">Python</span><span class="sxs-lookup"><span data-stu-id="037dd-212">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="037dd-213">その他のコード サンプルを表示する</span><span class="sxs-lookup"><span data-stu-id="037dd-213">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="037dd-214">**Teams プロアクティブ メッセージングのコード サンプル**</span><span class="sxs-lookup"><span data-stu-id="037dd-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
