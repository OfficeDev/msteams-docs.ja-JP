---
title: Microsoft Teams のボット
author: clearab
description: Microsoft Teams のボットの概要。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 70240b7396fc5e7a77749dc4e7326bfb30ea4415
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020892"
---
# <a name="bots-in-microsoft-teams"></a><span data-ttu-id="dede8-103">Microsoft Teams のボット</span><span class="sxs-lookup"><span data-stu-id="dede8-103">Bots in Microsoft Teams</span></span>

<span data-ttu-id="dede8-104">チャットボットまたは会話型ボットとも呼ばれるボットは、顧客サービスやサポート スタッフなど、ユーザーが実行する簡単で繰り返し自動化されたタスクを実行するアプリです。</span><span class="sxs-lookup"><span data-stu-id="dede8-104">A bot also referred to as a chatbot or conversational bot is an app that runs simple and repetitive automated tasks performed by the users, such as customer service or support staff.</span></span> <span data-ttu-id="dede8-105">日常的に使用されるボットの例としては、天気に関する情報を提供するボット、夕食の予約、旅行情報の提供などのボットがあります。</span><span class="sxs-lookup"><span data-stu-id="dede8-105">Examples of bots in everyday use include, bots that provide information about the weather, make dinner reservations, or provide travel information.</span></span> <span data-ttu-id="dede8-106">ボットの対話は、簡単な質問と回答、またはサービスへのアクセスを提供する複雑な会話です。</span><span class="sxs-lookup"><span data-stu-id="dede8-106">A bot interaction can be a quick question and answer, or it can be a complex conversation that provides access to services.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

<span data-ttu-id="dede8-107">会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。</span><span class="sxs-lookup"><span data-stu-id="dede8-107">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span>

![テキストを使用してボットを呼び出す](~/assets/images/invokebotwithtext.png)

![カードを使用してボットを呼び出す](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

<span data-ttu-id="dede8-110">会話型ボットは非常に柔軟性が高く、いくつかの簡単なコマンド、または複雑な人工知能による自然言語処理タスクを処理できます。</span><span class="sxs-lookup"><span data-stu-id="dede8-110">Conversational bots are incredibly flexible and can be scoped to handle a few simple commands, or complex, artificial-intelligence-powered, and natural-language-processing tasks.</span></span> <span data-ttu-id="dede8-111">大きなアプリケーションの 1 つの側面、または完全にスタンドアロンの場合があります。</span><span class="sxs-lookup"><span data-stu-id="dede8-111">They can be one aspect of a larger application, or be completely stand-alone.</span></span>

<span data-ttu-id="dede8-112">便利なボットを作成するには、カード、テキスト、タスク モジュールの適切な組み合わせを見つけることが重要です。</span><span class="sxs-lookup"><span data-stu-id="dede8-112">Finding the right mix of cards, text, and task modules are key to create a useful bot.</span></span> <span data-ttu-id="dede8-113">次の図は、テキスト カードと対話型カードの両方を使用して、1 対 1 のチャットでボットと会話するユーザーを示しています。</span><span class="sxs-lookup"><span data-stu-id="dede8-113">The following image shows a user conversing with a bot in a one-to-one chat using both, text and interactive cards:</span></span>

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="FAQ ボットのサンプル" border="true":::

<span data-ttu-id="dede8-115">ユーザーとボットの間のすべての操作は、アクティビティとして表されます。</span><span class="sxs-lookup"><span data-stu-id="dede8-115">Every interaction between the user and the bot is represented as an activity.</span></span> <span data-ttu-id="dede8-116">ボットがアクティビティを受け取った場合、ボットはアクティビティ ハンドラーに渡します。</span><span class="sxs-lookup"><span data-stu-id="dede8-116">When a bot receives an activity, it passes it on to its activity handlers.</span></span> <span data-ttu-id="dede8-117">詳細については、「ボット アクティビティ [ハンドラー」を参照してください](~/bots/bot-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="dede8-117">For more information, see [bot activity handlers](~/bots/bot-basics.md).</span></span> 

<span data-ttu-id="dede8-118">さらに、ボットは会話型インターフェイスを持つアプリです。</span><span class="sxs-lookup"><span data-stu-id="dede8-118">In addition, bots are apps that have a conversational interface.</span></span> <span data-ttu-id="dede8-119">テキスト、対話型カード、音声を使用してボットを操作できます。</span><span class="sxs-lookup"><span data-stu-id="dede8-119">You can interact with a bot using text, interactive cards, and speech.</span></span> <span data-ttu-id="dede8-120">ボットの動作は、会話がチャネルまたはグループ チャットの会話か、1 対 1 の会話かによって異なります。</span><span class="sxs-lookup"><span data-stu-id="dede8-120">A bot behaves differently depending on whether the conversation is a channel or group chat conversation, or it is a one-to-one conversation.</span></span> <span data-ttu-id="dede8-121">会話はボット フレームワーク コネクタを介して処理されます。</span><span class="sxs-lookup"><span data-stu-id="dede8-121">Conversations are handled through the Bot Framework connector.</span></span> <span data-ttu-id="dede8-122">詳細については、「会話の基本 [」を参照してください](~/bots/how-to/conversations/conversation-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="dede8-122">For more information, see [conversation basics](~/bots/how-to/conversations/conversation-basics.md).</span></span>

<span data-ttu-id="dede8-123">ボットには、関連するコンテンツにアクセスしてボットエクスペリエンスを強化するために、ユーザー プロファイルの詳細などのコンテキスト情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="dede8-123">Your bot requires contextual information, such as user profile details to access relevant content and enhance the bot experience.</span></span> <span data-ttu-id="dede8-124">詳細については [、「Get Teams context 」を参照してください](~/bots/how-to/get-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="dede8-124">For more information, see [get Teams context](~/bots/how-to/get-teams-context.md).</span></span> 

<span data-ttu-id="dede8-125">Graph API または Teams ボット API を使用して、ボットを介してファイルを送受信することもできます。</span><span class="sxs-lookup"><span data-stu-id="dede8-125">You can also send and receive files through the bot using Graph APIs or Teams bot APIs.</span></span> <span data-ttu-id="dede8-126">詳細については、「ボットを介 [してファイルを送受信する」を参照してください](~/bots/how-to/bots-filesv4.md)。</span><span class="sxs-lookup"><span data-stu-id="dede8-126">For more information, see [send and receive files through the bot](~/bots/how-to/bots-filesv4.md).</span></span>

<span data-ttu-id="dede8-127">さらに、レート制限は、Teams アプリケーションに使用されるボットを最適化するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="dede8-127">In addition, rate limiting is used to optimize bots used for your Teams application.</span></span> <span data-ttu-id="dede8-128">Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求のレート制限を提供します。</span><span class="sxs-lookup"><span data-stu-id="dede8-128">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="dede8-129">詳細については、「Teams でのレート [制限を使用してボットを最適化する」を参照してください](~/bots/how-to/rate-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="dede8-129">For more information, see [optimize your bot with rate limiting in Teams](~/bots/how-to/rate-limit.md).</span></span>

<span data-ttu-id="dede8-130">通話およびオンライン会議用の Microsoft Graph API を使用すると、Microsoft Teams アプリは音声とビデオを使用してユーザーと対話できます。</span><span class="sxs-lookup"><span data-stu-id="dede8-130">With Microsoft Graph APIs for calls and online meetings, Microsoft Teams apps can now interact with users using voice and video.</span></span> <span data-ttu-id="dede8-131">詳細については、「通話と [会議ボット」を参照してください](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dede8-131">For more information, see [calls and meetings bots](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span> 

<span data-ttu-id="dede8-132">Teams ボット API を使用して、チャットまたはチームの 1 つ以上のメンバーの情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="dede8-132">You can use the Teams bot APIs to get information for one or more members of a chat or team.</span></span> <span data-ttu-id="dede8-133">詳細については、「チームまたはチャット メンバーをフェッチする Teams ボット API の変更 [」を参照してください](~/resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="dede8-133">For more information, see [changes to Teams bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="dede8-134">関連項目</span><span class="sxs-lookup"><span data-stu-id="dede8-134">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dede8-135">Teams のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="dede8-135">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a><span data-ttu-id="dede8-136">次の手順</span><span class="sxs-lookup"><span data-stu-id="dede8-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dede8-137">ボットと SDK</span><span class="sxs-lookup"><span data-stu-id="dede8-137">Bots and SDKs</span></span>](~/bots/bot-features.md)
