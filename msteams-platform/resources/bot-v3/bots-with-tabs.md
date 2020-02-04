---
title: ボットとタブの統合
description: タブと bot を一緒に使用する方法について説明します。
keywords: teams の bot タブの開発
ms.date: 03/15/2018
ms.openlocfilehash: 59ae8bc01f82c70dd7ea6869cb870e26acae1293
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674919"
---
# <a name="combine-bots-with-tabs"></a><span data-ttu-id="f8d43-104">ボットとタブの統合</span><span class="sxs-lookup"><span data-stu-id="f8d43-104">Combine bots with tabs</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f8d43-105">Bot とタブはうまく連動しており、多くの場合1つのバックエンドサービスに統合されています。</span><span class="sxs-lookup"><span data-stu-id="f8d43-105">Bots and tabs work well together, and are often combined into a single back-end service.</span></span> <span data-ttu-id="f8d43-106">このセクションでは、タブとボットを一緒に使用するためのベストプラクティスと一般的なパターンについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f8d43-106">This section describes best practices and common patterns for using tabs and bots together.</span></span>

## <a name="associating-user-identities-across-bot-and-tab"></a><span data-ttu-id="f8d43-107">Bot とタブの間のユーザー id の関連付け</span><span class="sxs-lookup"><span data-stu-id="f8d43-107">Associating user identities across bot and tab</span></span>

<span data-ttu-id="f8d43-108">たとえば、タブアプリケーションが独自の ID システムを使用してそのコンテンツを保護しているとします。</span><span class="sxs-lookup"><span data-stu-id="f8d43-108">For example: Suppose your tab application uses a proprietary ID system to secure its content.</span></span> <span data-ttu-id="f8d43-109">ユーザーとの対話が可能な bot もあるとします。</span><span class="sxs-lookup"><span data-stu-id="f8d43-109">Suppose you also have a bot that can interact with the user.</span></span> <span data-ttu-id="f8d43-110">通常、表示ユーザーに固有のタブにコンテンツを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f8d43-110">Typically, you’ll want to show content in the tab that is specific to the viewing user.</span></span> <span data-ttu-id="f8d43-111">課題は、システム内のユーザー ID が Microsoft Teams のユーザー ID と異なる可能性があるということです。</span><span class="sxs-lookup"><span data-stu-id="f8d43-111">The challenge is that the user ID in your system is likely different from the Microsoft Teams user ID.</span></span> <span data-ttu-id="f8d43-112">これら2つの id を関連付けるには、どうすればよいですか。</span><span class="sxs-lookup"><span data-stu-id="f8d43-112">So how do you associate these two identities?</span></span>
<span data-ttu-id="f8d43-113">通常、推奨される方法は、タブのコンテンツに認証を提供するために使用されているものと同じ id システムを使用して、ユーザーを bot で署名することです。</span><span class="sxs-lookup"><span data-stu-id="f8d43-113">In general, the recommended approach is to sign the user in with the bot using the same identity system used to provide authentication for the tab content.</span></span> <span data-ttu-id="f8d43-114">これは、通常、OAuth フローを使用してユーザーにログインする、サインインアクションによって実装できます。</span><span class="sxs-lookup"><span data-stu-id="f8d43-114">You can implement this via the sign-in action, which typically logs in the user via an OAuth flow.</span></span>

<span data-ttu-id="f8d43-115">このフローは、id プロバイダーが OAuth 2.0 プロトコルを実装している場合に最適に機能します。</span><span class="sxs-lookup"><span data-stu-id="f8d43-115">This flow works best if your identity provider implements the OAuth 2.0 protocol.</span></span> <span data-ttu-id="f8d43-116">その後、Teams のユーザー ID を、独自の id サービスからのユーザーの資格情報に関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="f8d43-116">You can then associate the Teams user ID with the user’s credentials from your own identity service.</span></span>

   ![Id の関連付け](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a><span data-ttu-id="f8d43-118">Bot からのメッセージ内のタブへの詳細なリンクの構築</span><span class="sxs-lookup"><span data-stu-id="f8d43-118">Constructing deep links to tabs in messages from your bot</span></span>

<span data-ttu-id="f8d43-119">タブを使用して、カード内に収まる数より多くのコンテンツを表示したり、タブキャンバスを使用して、複雑なフォーム入力タスクを完了する方法を提供したりできます。</span><span class="sxs-lookup"><span data-stu-id="f8d43-119">You may want to use tabs to show more content than can fit inside of a card, or provide a way to complete complex form-filling tasks using the tab canvas.</span></span> <span data-ttu-id="f8d43-120">たとえば、ユーザーが bot からカードをクリックしたときにタブに移動することを検討します。</span><span class="sxs-lookup"><span data-stu-id="f8d43-120">For example, consider navigating the user to the tab when he or she clicks on the card from your bot.</span></span> <span data-ttu-id="f8d43-121">これを行うには、ボットのメッセージをエンコードして、マークアップ経由で、または openUrl アクションの対象として[ディープリンク](~/concepts/build-and-test/deep-links.md)URL を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f8d43-121">For this to happen, you’ll need to encode your bot’s message to include a [deep link](~/concepts/build-and-test/deep-links.md) URL, either via markup or as the target of the openUrl action.</span></span>

<span data-ttu-id="f8d43-122">ディープリンクは、entityId に依存します。この値は、システム内の一意のエンティティにマッピングされる不透明な値です。</span><span class="sxs-lookup"><span data-stu-id="f8d43-122">Deep links rely on an entityId, which is an opaque value that maps to a unique entity in your system.</span></span> <span data-ttu-id="f8d43-123">タブが作成されると、チャネル内でタブが作成されたことを示す単純な状態 (たとえば、フラグ) をバックエンドに格納するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="f8d43-123">When the tab is created, you ideally store some simple state (e.g. flag) on your backend indicating the tab has been created in the channel.</span></span> <span data-ttu-id="f8d43-124">Bot がメッセージを作成するとき、そのタブに関連付けられている entityId を対象とすることができます。</span><span class="sxs-lookup"><span data-stu-id="f8d43-124">When your bot constructs a message, it can target the entityId associated with that tab.</span></span>

<span data-ttu-id="f8d43-125">**注:** 個人用チャットでは、タブは "静的" であり、アプリと共にインストールされるため、常にその存在を想定して、それに応じて深いリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f8d43-125">**Note:** in personal chats, because tabs are “static” and installed with the app, you can always assume their existence and thus construct deep links accordingly.</span></span>

## <a name="sending-notifications-for-tab-updates"></a><span data-ttu-id="f8d43-126">タブ更新の通知の送信</span><span class="sxs-lookup"><span data-stu-id="f8d43-126">Sending notifications for tab updates</span></span>

<span data-ttu-id="f8d43-127">タブ内で更新またはユーザー操作が発生するたびに、エンドユーザーに通知する必要があります。シナリオの例としては、チームメンバーにタスクまたはチケットを割り当てて、そのチームメンバーに通知します。</span><span class="sxs-lookup"><span data-stu-id="f8d43-127">Often you’ll want to notify the end user whenever an update or a user action occurs in a tab. An example scenario is assigning a task or ticket to a fellow team member and then notifying that team member.</span></span>

<span data-ttu-id="f8d43-128">このシナリオを実現するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="f8d43-128">There are two ways of achieving this scenario:</span></span>

1. <span data-ttu-id="f8d43-129">チャネル全体に通知する場合は、ボットがメッセージをチャネルに非同期で送信できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f8d43-129">If you wish to notify an entire channel your bot can asynchronously post a message to the channel.</span></span> <span data-ttu-id="f8d43-130">タブを使用して作成されていない場合、ボットが事前にタブの会話を作成する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="f8d43-130">There is no way for a bot to proactively create the tab conversation if it wasn't created with the tab.</span></span>

2. <span data-ttu-id="f8d43-131">このアクションに関係する受信者または関係者にのみ通知する場合、ボットはユーザーに対して個人のチャットメッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="f8d43-131">If you wish to only notify the recipient or interested parties involved with the action, your bot can send a personal chat message to the user.</span></span> <span data-ttu-id="f8d43-132">最初に、bot とユーザーの間の個人用会話が存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="f8d43-132">You should first check to see if a personal conversation between your bot and the user exists.</span></span> <span data-ttu-id="f8d43-133">それ以外の場合は、 `CreateConversation`を呼び出して、パーソナルチャットを開始することができます。</span><span class="sxs-lookup"><span data-stu-id="f8d43-133">If not, you can call `CreateConversation` to initiate the personal chat.</span></span>

<span data-ttu-id="f8d43-134">どちらの場合も、イベント通知を慎重に使用して、不要な更新をユーザーにスパムしないようにします。</span><span class="sxs-lookup"><span data-stu-id="f8d43-134">In both cases, use event notifications wisely and never spam the user with unnecessary updates.</span></span>
