---
title: ボットを使用してメッセージを送受信する
description: Microsoft Teams でボットを使用してメッセージを送受信する方法について説明します。
ms.topic: overview
keywords: チームボット メッセージ
ms.date: 05/20/2019
ms.openlocfilehash: 20c285a0cd06ac929d628edbc059b2a00b937eec
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014118"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="68192-104">Microsoft Teams ボットと会話する</span><span class="sxs-lookup"><span data-stu-id="68192-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="68192-105">会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。</span><span class="sxs-lookup"><span data-stu-id="68192-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="68192-106">Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。</span><span class="sxs-lookup"><span data-stu-id="68192-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="68192-107">`teams` チャネル会話とも呼ばれる、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="68192-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="68192-108">`personal` ボットと 1 人のユーザーの会話。</span><span class="sxs-lookup"><span data-stu-id="68192-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="68192-109">`groupChat` ボットと 2 人以上のユーザーの間でチャットします。</span><span class="sxs-lookup"><span data-stu-id="68192-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="68192-110">ボットの動作は、関連する会話の種類によって少し異なります。</span><span class="sxs-lookup"><span data-stu-id="68192-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="68192-111">[チャネルとグループ チャットの会話の](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) ボットでは、ユーザーがチャネルでボットを呼び出す @ メンションをする必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="68192-112">[単一ユーザーの会話のボットには](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) @ メンションは不要です。ユーザーは入力できます。</span><span class="sxs-lookup"><span data-stu-id="68192-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="68192-113">ボットが特定のスコープで動作するには、そのスコープをサポートするとしてマニフェストに一覧表示される必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="68192-114">スコープはマニフェスト リファレンスで定義され、詳 [しい説明を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="68192-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="68192-115">プロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="68192-115">Proactive messages</span></span>

<span data-ttu-id="68192-116">ボットは会話に参加するか、会話を開始できます。</span><span class="sxs-lookup"><span data-stu-id="68192-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="68192-117">ほとんどの通信は、別のメッセージに対する応答です。</span><span class="sxs-lookup"><span data-stu-id="68192-117">Most communication is in response to another message.</span></span> <span data-ttu-id="68192-118">ボットが会話を開始する場合は、プロアクティブ メッセージ *と呼ばれる。*</span><span class="sxs-lookup"><span data-stu-id="68192-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="68192-119">たとえば、次のような情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="68192-119">Examples include:</span></span>

* <span data-ttu-id="68192-120">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="68192-120">Welcome messages</span></span>
* <span data-ttu-id="68192-121">イベント通知</span><span class="sxs-lookup"><span data-stu-id="68192-121">Event notifications</span></span>
* <span data-ttu-id="68192-122">メッセージのポーリング</span><span class="sxs-lookup"><span data-stu-id="68192-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="68192-123">会話の基本</span><span class="sxs-lookup"><span data-stu-id="68192-123">Conversation basics</span></span>

<span data-ttu-id="68192-124">各メッセージは `messageType: message` 型の `Activity` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="68192-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="68192-125">ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。</span><span class="sxs-lookup"><span data-stu-id="68192-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="68192-126">ボットがメッセージを調べて種類を特定し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="68192-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="68192-127">ボットは、イベント スタイルのメッセージもサポートします。</span><span class="sxs-lookup"><span data-stu-id="68192-127">Bots also support event-style messages.</span></span> <span data-ttu-id="68192-128">詳細 [については、「Microsoft Teams でのボット イベントの処理](~/resources/bot-v3/bots-notifications.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="68192-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="68192-129">現在、音声はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="68192-129">Speech is currently not supported.</span></span>

<span data-ttu-id="68192-130">メッセージの大部分は、すべてのスコープで同じですが、ボットが UI でアクセスされる方法と、知る必要がある背後での違いがあります。</span><span class="sxs-lookup"><span data-stu-id="68192-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="68192-131">基本的な会話は、ボットが Teams や他のチャネルと通信するための単一の REST API である Bot Framework Connector を通じて処理されます。</span><span class="sxs-lookup"><span data-stu-id="68192-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="68192-132">Bot Builder SDK は、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="68192-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="68192-133">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="68192-133">Message content</span></span>

<span data-ttu-id="68192-134">ボットは、リッチ テキスト、画像、カードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="68192-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="68192-135">ユーザーは、リッチ テキストと画像をボットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="68192-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="68192-136">ボットが処理できるコンテンツの種類は、ボットの Microsoft Teams 設定ページで指定できます。</span><span class="sxs-lookup"><span data-stu-id="68192-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="68192-137">フォーマット</span><span class="sxs-lookup"><span data-stu-id="68192-137">Format</span></span> | <span data-ttu-id="68192-138">ユーザーからボットへ</span><span class="sxs-lookup"><span data-stu-id="68192-138">From user to bot</span></span>  | <span data-ttu-id="68192-139">ボットからユーザーへ</span><span class="sxs-lookup"><span data-stu-id="68192-139">From bot to user</span></span> |  <span data-ttu-id="68192-140">Notes</span><span class="sxs-lookup"><span data-stu-id="68192-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="68192-141">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="68192-141">Rich text</span></span> | <span data-ttu-id="68192-142">✔</span><span class="sxs-lookup"><span data-stu-id="68192-142">✔</span></span> | <span data-ttu-id="68192-143">✔</span><span class="sxs-lookup"><span data-stu-id="68192-143">✔</span></span> |  |
| <span data-ttu-id="68192-144">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="68192-144">Pictures</span></span> | <span data-ttu-id="68192-145">✔</span><span class="sxs-lookup"><span data-stu-id="68192-145">✔</span></span> | <span data-ttu-id="68192-146">✔</span><span class="sxs-lookup"><span data-stu-id="68192-146">✔</span></span> | <span data-ttu-id="68192-147">最大 1024×1024 および 1 MB (PNG、JPEG、または GIF 形式)。アニメーション GIF はサポートされていません</span><span class="sxs-lookup"><span data-stu-id="68192-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="68192-148">カード</span><span class="sxs-lookup"><span data-stu-id="68192-148">Cards</span></span> | <span data-ttu-id="68192-149">✖</span><span class="sxs-lookup"><span data-stu-id="68192-149">✖</span></span> | <span data-ttu-id="68192-150">✔</span><span class="sxs-lookup"><span data-stu-id="68192-150">✔</span></span> | <span data-ttu-id="68192-151">サポートされている [カードについては、Teams カード](~/task-modules-and-cards/cards/cards-reference.md) リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="68192-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="68192-152">Emojis</span><span class="sxs-lookup"><span data-stu-id="68192-152">Emojis</span></span> | <span data-ttu-id="68192-153">✖</span><span class="sxs-lookup"><span data-stu-id="68192-153">✖</span></span> | <span data-ttu-id="68192-154">✔</span><span class="sxs-lookup"><span data-stu-id="68192-154">✔</span></span> | <span data-ttu-id="68192-155">Teams は現在、UTF-16 を介して絵文字をサポートしています (顔のくびくびくをする U+1F600 など)</span><span class="sxs-lookup"><span data-stu-id="68192-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="68192-156">Bot Framework でサポートされるボット操作の種類 (チーム内のボットの基に基づく) の詳細については、Bot Builder [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) [SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0)および bot Builder SDK for [Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)のドキュメントの会話フローと関連概念に関する Bot Framework のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="68192-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="68192-157">メッセージの書式設定</span><span class="sxs-lookup"><span data-stu-id="68192-157">Message formatting</span></span>

<span data-ttu-id="68192-158">a のオプション [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) のプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 `message` を制御できます。</span><span class="sxs-lookup"><span data-stu-id="68192-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="68192-159">ボット [メッセージでサポート](~/resources/bot-v3/bots-message-format.md) されている書式設定の詳細については、「メッセージの書式設定」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="68192-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="68192-160">オプションのプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) を制御できます。</span><span class="sxs-lookup"><span data-stu-id="68192-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="68192-161">Teams がチームでテキストの書式設定をサポートする方法の詳細については、「ボット メッセージのテキスト [の書式設定」を参照してください](~/resources/bot-v3/bots-text-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="68192-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="68192-162">メッセージ内のカードの書式設定の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="68192-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="68192-163">画像メッセージ</span><span class="sxs-lookup"><span data-stu-id="68192-163">Picture messages</span></span>

<span data-ttu-id="68192-164">画像は、メッセージに添付ファイルを追加することで送信されます。</span><span class="sxs-lookup"><span data-stu-id="68192-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="68192-165">添付ファイルの詳細については、Bot Framework のドキュメント [を参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)。</span><span class="sxs-lookup"><span data-stu-id="68192-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="68192-166">画像は、PNG、JPEG、GIF 形式で最大 1024×1024 および 1 MB です。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="68192-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="68192-167">XML を使用して各イメージの高さと幅を指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="68192-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="68192-168">Markdown を使用する場合、画像サイズの既定値は 256×256 です。</span><span class="sxs-lookup"><span data-stu-id="68192-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="68192-169">以下に例を示します。</span><span class="sxs-lookup"><span data-stu-id="68192-169">For example:</span></span>

* <span data-ttu-id="68192-170">`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` を使う</span><span class="sxs-lookup"><span data-stu-id="68192-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="68192-171">使用しない `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="68192-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="68192-172">メッセージの受信</span><span class="sxs-lookup"><span data-stu-id="68192-172">Receiving messages</span></span>

<span data-ttu-id="68192-173">宣言されているスコープに応じて、ボットは次のコンテキストでメッセージを受信できます。</span><span class="sxs-lookup"><span data-stu-id="68192-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="68192-174">**個人用チャット** ユーザーは、チャット履歴で追加されたボットを選択するか、新しいチャットの [To:] ボックスに名前またはアプリ ID を入力するだけで、ボットとのプライベート会話で対話できます。</span><span class="sxs-lookup"><span data-stu-id="68192-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="68192-175">**チャネル** ボットがチームに追加されている場合は、チャネルでボットを言及 ("@_botname_") できます。</span><span class="sxs-lookup"><span data-stu-id="68192-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="68192-176">チャネル内のボットに対する追加の返信には、ボットのメンションが必要です。</span><span class="sxs-lookup"><span data-stu-id="68192-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="68192-177">記載されていない返信には応答しない。</span><span class="sxs-lookup"><span data-stu-id="68192-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="68192-178">受信メッセージの場合、ボットは種類の [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) オブジェクトを受信します `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="68192-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) object of type `messageType: message`.</span></span> <span data-ttu-id="68192-179">オブジェクトには、ボットに送信されるチャネルの更新など、他の種類の情報を含めすることもできますが、この型はボットとユーザーの間の `Activity` [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` 通信を表します。</span><span class="sxs-lookup"><span data-stu-id="68192-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="68192-180">ボットは、ユーザー メッセージと、ユーザーに関するその他の情報、メッセージのソース、および Teams 情報を含むペイロード `Text` を受信します。</span><span class="sxs-lookup"><span data-stu-id="68192-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="68192-181">次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="68192-181">Of note:</span></span>

* <span data-ttu-id="68192-182">`timestamp` 協定世界時 (UTC) でのメッセージの日時</span><span class="sxs-lookup"><span data-stu-id="68192-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="68192-183">`localTimestamp` 送信者のタイム ゾーンでのメッセージの日時</span><span class="sxs-lookup"><span data-stu-id="68192-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="68192-184">`channelId` 常に "msteams" です。</span><span class="sxs-lookup"><span data-stu-id="68192-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="68192-185">これは、チーム チャネルではなくボット フレームワーク チャネルを指します。</span><span class="sxs-lookup"><span data-stu-id="68192-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="68192-186">`from.id` ボットのそのユーザーの一意で暗号化された ID。アプリでユーザー データを保存する必要がある場合にキーとして適しています。</span><span class="sxs-lookup"><span data-stu-id="68192-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="68192-187">ボットに固有の機能であり、そのユーザーを識別するための意味のある方法でボット インスタンスの外部で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="68192-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="68192-188">`channelData.tenant.id` ユーザーのテナント ID。</span><span class="sxs-lookup"><span data-stu-id="68192-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="68192-189">`from.id` はボットに固有であり、そのユーザーを識別するための意味のある方法でボット インスタンスの外部で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="68192-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="68192-190">チャネルとプライベート操作をボットと組み合わせる</span><span class="sxs-lookup"><span data-stu-id="68192-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="68192-191">チャネルで操作する場合、ボットは、ユーザーとの特定の会話をオフラインにした方が良い必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="68192-192">たとえば、ユーザーがチーム メンバーのセットとのスケジュール設定などの複雑なタスクを調整しようとしているとします。</span><span class="sxs-lookup"><span data-stu-id="68192-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="68192-193">一連の操作全体がチャネルに表示されるのではなく、ユーザーに個人用チャット メッセージを送信する方法を検討してください。</span><span class="sxs-lookup"><span data-stu-id="68192-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="68192-194">ボットは、状態を失わずに、個人会話とチャネル会話の間でユーザーを簡単に移行できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="68192-195">他のチーム メンバーに通知する操作が完了したら、チャネルを更新することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="68192-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="68192-196">完全な受信スキーマの例</span><span class="sxs-lookup"><span data-stu-id="68192-196">Full inbound schema example</span></span>

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> <span data-ttu-id="68192-197">受信メッセージのテキスト フィールドにメンションが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="68192-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="68192-198">それらのチェックと取り除きを正しく行ってください。</span><span class="sxs-lookup"><span data-stu-id="68192-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="68192-199">詳細については、「メンション [」を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。</span><span class="sxs-lookup"><span data-stu-id="68192-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="68192-200">Teams チャネル データ</span><span class="sxs-lookup"><span data-stu-id="68192-200">Teams channel data</span></span>

<span data-ttu-id="68192-201">オブジェクトには Teams 固有の情報が含まれているので、チームとチャネルの ID の確定的 `channelData` なソースです。</span><span class="sxs-lookup"><span data-stu-id="68192-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="68192-202">これらの ID をキャッシュし、ローカル ストレージのキーとして使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="68192-203">オブジェクトはチャネルの外部で行うので、個人の会話の `channelData` メッセージには含まれません。</span><span class="sxs-lookup"><span data-stu-id="68192-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="68192-204">ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="68192-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="68192-205">`eventType` Teams イベントの種類:チャネル変更イベントの場合 [にのみ渡されます。](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="68192-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="68192-206">`tenant.id` Azure Active Directory テナント ID;すべてのコンテキストで渡される</span><span class="sxs-lookup"><span data-stu-id="68192-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="68192-207">`team` チャネル コンテキストでのみ渡されます。個人用チャットでは渡されます。</span><span class="sxs-lookup"><span data-stu-id="68192-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="68192-208">`id` チャネルの GUID</span><span class="sxs-lookup"><span data-stu-id="68192-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="68192-209">`name` チームの名前。チームの名前変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="68192-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="68192-210">`channel` ボットが言及されている場合、またはボットが追加されたチームのチャネルのイベントに対して、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="68192-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="68192-211">`id` チャネルの GUID</span><span class="sxs-lookup"><span data-stu-id="68192-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="68192-212">`name` チャネル名チャネル変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#channel-updates)。</span><span class="sxs-lookup"><span data-stu-id="68192-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="68192-213">`channelData.teamsTeamId` 非推奨。</span><span class="sxs-lookup"><span data-stu-id="68192-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="68192-214">このプロパティは、下位互換性のためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="68192-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="68192-215">`channelData.teamsChannelId` 非推奨。</span><span class="sxs-lookup"><span data-stu-id="68192-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="68192-216">このプロパティは、下位互換性のためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="68192-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="68192-217">channelData オブジェクトの例 (channelCreated イベント)</span><span class="sxs-lookup"><span data-stu-id="68192-217">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a><span data-ttu-id="68192-218">.NET の例</span><span class="sxs-lookup"><span data-stu-id="68192-218">.NET example</span></span>

<span data-ttu-id="68192-219">[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージは、Teams 固有の情報にアクセスするプロパティを公開する特殊 `TeamsChannelData` なオブジェクトを提供します。</span><span class="sxs-lookup"><span data-stu-id="68192-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="68192-220">メッセージへの返信の送信</span><span class="sxs-lookup"><span data-stu-id="68192-220">Sending replies to messages</span></span>

<span data-ttu-id="68192-221">既存のメッセージに返信するには、.NET または既存のメッセージを呼び [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) 出Node.js。</span><span class="sxs-lookup"><span data-stu-id="68192-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) in Node.js.</span></span> <span data-ttu-id="68192-222">Bot Builder SDK は、すべての詳細を処理します。</span><span class="sxs-lookup"><span data-stu-id="68192-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="68192-223">REST API を使用する場合は、エンドポイントを呼び出 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) す方法も可能です。</span><span class="sxs-lookup"><span data-stu-id="68192-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) endpoint.</span></span>

<span data-ttu-id="68192-224">メッセージコンテンツ自体には、単純なテキストや Bot Framework で提供されるカードとカード [アクションの一部を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="68192-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="68192-225">送信スキーマでは、受信したスキーマと常に同じ値 `serviceUrl` を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="68192-226">値は安定する `serviceUrl` 傾向がありますが、変化する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="68192-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="68192-227">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="68192-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="68192-228">メッセージの更新</span><span class="sxs-lookup"><span data-stu-id="68192-228">Updating messages</span></span>

<span data-ttu-id="68192-229">メッセージをデータの静的スナップショットにするのではなく、ボットは送信後にインラインでメッセージを動的に更新できます。</span><span class="sxs-lookup"><span data-stu-id="68192-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="68192-230">ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオで、動的メッセージの更新を使用できます。</span><span class="sxs-lookup"><span data-stu-id="68192-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="68192-231">新しいメッセージは、種類が元のメッセージと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-231">The new message need not match the original in type.</span></span> <span data-ttu-id="68192-232">たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージは単純なテキスト メッセージになります。</span><span class="sxs-lookup"><span data-stu-id="68192-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="68192-233">単一添付メッセージとカルーセル レイアウトで送信されたコンテンツのみを更新できます。</span><span class="sxs-lookup"><span data-stu-id="68192-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="68192-234">リスト レイアウトで複数の添付ファイルを持つメッセージへの更新の投稿はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="68192-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="68192-235">REST API</span><span class="sxs-lookup"><span data-stu-id="68192-235">REST API</span></span>

<span data-ttu-id="68192-236">メッセージ更新を発行するには、特定のアクティビティ ID を使用してエンドポイントに対して PUT `/v3/conversations/<conversationId>/activities/<activityId>/` 要求を実行します。</span><span class="sxs-lookup"><span data-stu-id="68192-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="68192-237">このシナリオを完了するには、元の POST 呼び出しによって返されたアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="68192-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="68192-238">.NET の例</span><span class="sxs-lookup"><span data-stu-id="68192-238">.NET example</span></span>

<span data-ttu-id="68192-239">Bot Builder `UpdateActivityAsync` SDK のメソッドを使用して、既存のメッセージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="68192-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a><span data-ttu-id="68192-240">Node.js例</span><span class="sxs-lookup"><span data-stu-id="68192-240">Node.js example</span></span>

<span data-ttu-id="68192-241">Bot Builder `session.connector.update` SDK のメソッドを使用して、既存のメッセージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="68192-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="68192-242">会話を開始する (プロアクティブ メッセージング)</span><span class="sxs-lookup"><span data-stu-id="68192-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="68192-243">ユーザーとの個人的な会話を作成したり、チーム ボットのチャネルで新しい返信チェーンを開始することができます。</span><span class="sxs-lookup"><span data-stu-id="68192-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="68192-244">これにより、最初にボットとの連絡を開始することなく、ユーザーにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="68192-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="68192-245">詳細については、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="68192-245">For more information, see the following topics:</span></span>

<span data-ttu-id="68192-246">ボット [によって開始される会話の詳細については、「](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) ボットのプロアクティブ メッセージング」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="68192-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="68192-247">メッセージの削除</span><span class="sxs-lookup"><span data-stu-id="68192-247">Deleting messages</span></span>

<span data-ttu-id="68192-248">メッセージは BotBuilder SDK のコネクタ [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) メソッドを使用 [して削除できます](/bot-framework/bot-builder-overview-getstarted)。</span><span class="sxs-lookup"><span data-stu-id="68192-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
