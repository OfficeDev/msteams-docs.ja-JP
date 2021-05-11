---
title: ボットとタブを組み合わせる
description: タブとボットを一緒に使用する方法について説明します。
keywords: teams ボットのタブ開発
ms.topic: conceptual
localization_priority: Normal
ms.date: 03/15/2018
ms.openlocfilehash: b33d0bfcae4b522fc9e0c7d17b3d082979a62647
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020626"
---
# <a name="combine-bots-with-tabs"></a><span data-ttu-id="f545c-104">ボットとタブを組み合わせる</span><span class="sxs-lookup"><span data-stu-id="f545c-104">Combine bots with tabs</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f545c-105">ボットとタブはうまく機能し、多くの場合、単一のバック エンド サービスに組み合わされます。</span><span class="sxs-lookup"><span data-stu-id="f545c-105">Bots and tabs work well together, and are often combined into a single back-end service.</span></span> <span data-ttu-id="f545c-106">このセクションでは、タブとボットを一緒に使用するためのベスト プラクティスと一般的なパターンについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f545c-106">This section describes best practices and common patterns for using tabs and bots together.</span></span>

## <a name="associating-user-identities-across-bot-and-tab"></a><span data-ttu-id="f545c-107">ボットとタブ間でのユーザー ID の関連付け</span><span class="sxs-lookup"><span data-stu-id="f545c-107">Associating user identities across bot and tab</span></span>

<span data-ttu-id="f545c-108">たとえば、タブ アプリケーションが独自の ID システムを使用してコンテンツをセキュリティで保護するとします。</span><span class="sxs-lookup"><span data-stu-id="f545c-108">For example: Suppose your tab application uses a proprietary ID system to secure its content.</span></span> <span data-ttu-id="f545c-109">また、ユーザーと対話できるボットが用意されているとします。</span><span class="sxs-lookup"><span data-stu-id="f545c-109">Suppose you also have a bot that can interact with the user.</span></span> <span data-ttu-id="f545c-110">通常、表示ユーザーに固有のコンテンツをタブに表示します。</span><span class="sxs-lookup"><span data-stu-id="f545c-110">Typically, you’ll want to show content in the tab that is specific to the viewing user.</span></span> <span data-ttu-id="f545c-111">難しいのは、システム内のユーザー ID がユーザー ID と異なるMicrosoft Teamsです。</span><span class="sxs-lookup"><span data-stu-id="f545c-111">The challenge is that the user ID in your system is likely different from the Microsoft Teams user ID.</span></span> <span data-ttu-id="f545c-112">では、これら 2 つの ID を関連付ける方法は?</span><span class="sxs-lookup"><span data-stu-id="f545c-112">So how do you associate these two identities?</span></span>
<span data-ttu-id="f545c-113">一般に、推奨される方法は、タブ コンテンツの認証を提供するために使用されるのと同じ ID システムを使用してボットでユーザーにサインインする方法です。</span><span class="sxs-lookup"><span data-stu-id="f545c-113">In general, the recommended approach is to sign the user in with the bot using the same identity system used to provide authentication for the tab content.</span></span> <span data-ttu-id="f545c-114">これは、通常、OAuth フローを介してユーザーにログインするサインイン アクションを使用して実装できます。</span><span class="sxs-lookup"><span data-stu-id="f545c-114">You can implement this via the sign-in action, which typically logs in the user via an OAuth flow.</span></span>

<span data-ttu-id="f545c-115">このフローは、ID プロバイダーが OAuth 2.0 プロトコルを実装している場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="f545c-115">This flow works best if your identity provider implements the OAuth 2.0 protocol.</span></span> <span data-ttu-id="f545c-116">その後、ユーザー ID Teamsユーザー ID を、自分の ID サービスからのユーザーの資格情報に関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="f545c-116">You can then associate the Teams user ID with the user’s credentials from your own identity service.</span></span>

   ![ID の関連付け](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a><span data-ttu-id="f545c-118">ボットからのメッセージ内のタブへのディープ リンクの作成</span><span class="sxs-lookup"><span data-stu-id="f545c-118">Constructing deep links to tabs in messages from your bot</span></span>

<span data-ttu-id="f545c-119">タブを使用して、カード内に収まらないコンテンツを表示したり、タブ キャンバスを使用して複雑なフォーム入力タスクを完了したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f545c-119">You may want to use tabs to show more content than can fit inside of a card, or provide a way to complete complex form-filling tasks using the tab canvas.</span></span> <span data-ttu-id="f545c-120">たとえば、ボットからカードをクリックすると、ユーザーをタブに移動できます。</span><span class="sxs-lookup"><span data-stu-id="f545c-120">For example, consider navigating the user to the tab when he or she clicks on the card from your bot.</span></span> <span data-ttu-id="f545c-121">このためには、ボットのメッセージをエンコードして、マークアップまたは openUrl アクションのターゲットとしてディープ リンク [URL](~/concepts/build-and-test/deep-links.md) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f545c-121">For this to happen, you’ll need to encode your bot’s message to include a [deep link](~/concepts/build-and-test/deep-links.md) URL, either via markup or as the target of the openUrl action.</span></span>

<span data-ttu-id="f545c-122">ディープ リンクは entityId に依存します。これは、システム内の一意のエンティティにマップされる不透明な値です。</span><span class="sxs-lookup"><span data-stu-id="f545c-122">Deep links rely on an entityId, which is an opaque value that maps to a unique entity in your system.</span></span> <span data-ttu-id="f545c-123">タブが作成されると、タブがチャネル内に作成されたことを示す単純な状態 (フラグなど) をバックエンドに保存するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="f545c-123">When the tab is created, you ideally store some simple state (e.g. flag) on your backend indicating the tab has been created in the channel.</span></span> <span data-ttu-id="f545c-124">ボットがメッセージを作成すると、そのタブに関連付けられた entityId をターゲットにできます。</span><span class="sxs-lookup"><span data-stu-id="f545c-124">When your bot constructs a message, it can target the entityId associated with that tab.</span></span>

<span data-ttu-id="f545c-125">**注:** 個人用チャットでは、タブは "静的" であり、アプリと一緒にインストールされますので、常にそれらの存在を前提として、したがって、必要に応じてディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f545c-125">**Note:** in personal chats, because tabs are “static” and installed with the app, you can always assume their existence and thus construct deep links accordingly.</span></span>

## <a name="sending-notifications-for-tab-updates"></a><span data-ttu-id="f545c-126">タブ更新の通知の送信</span><span class="sxs-lookup"><span data-stu-id="f545c-126">Sending notifications for tab updates</span></span>

<span data-ttu-id="f545c-127">多くの場合、タブで更新またはユーザー操作が発生するたびにエンド ユーザーに通知する必要があります。たとえば、タスクまたはチケットを仲間のチーム メンバーに割り当て、そのチーム メンバーに通知します。</span><span class="sxs-lookup"><span data-stu-id="f545c-127">Often you’ll want to notify the end user whenever an update or a user action occurs in a tab. An example scenario is assigning a task or ticket to a fellow team member and then notifying that team member.</span></span>

<span data-ttu-id="f545c-128">このシナリオを実現するには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="f545c-128">There are two ways of achieving this scenario:</span></span>

1. <span data-ttu-id="f545c-129">チャネル全体に通知する場合、ボットはチャネルにメッセージを非同期的に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="f545c-129">If you wish to notify an entire channel your bot can asynchronously post a message to the channel.</span></span> <span data-ttu-id="f545c-130">ボットがタブで作成されなかった場合、ボットが積極的にタブ会話を作成する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="f545c-130">There is no way for a bot to proactively create the tab conversation if it wasn't created with the tab.</span></span>

2. <span data-ttu-id="f545c-131">アクションに関連する受信者または関係者にのみ通知する場合、ボットはユーザーに個人のチャット メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="f545c-131">If you wish to only notify the recipient or interested parties involved with the action, your bot can send a personal chat message to the user.</span></span> <span data-ttu-id="f545c-132">まず、ボットとユーザーの間の個人的な会話が存在するかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f545c-132">You should first check to see if a personal conversation between your bot and the user exists.</span></span> <span data-ttu-id="f545c-133">設定されていない場合は、電話で `CreateConversation` 個人チャットを開始できます。</span><span class="sxs-lookup"><span data-stu-id="f545c-133">If not, you can call `CreateConversation` to initiate the personal chat.</span></span>

<span data-ttu-id="f545c-134">どちらの場合も、イベント通知を賢明に使用し、不要な更新プログラムでユーザーに迷惑メールを送信しない。</span><span class="sxs-lookup"><span data-stu-id="f545c-134">In both cases, use event notifications wisely and never spam the user with unnecessary updates.</span></span>
