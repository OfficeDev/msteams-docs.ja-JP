---
title: Bot でメッセージを送受信する
description: Microsoft Teams でボットを使用してメッセージを送受信する方法について説明します。
keywords: teams の bot メッセージ
ms.date: 05/20/2019
ms.openlocfilehash: 864473c7f502d96987a48e5837840236c45f59c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675113"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="620bc-104">Microsoft Teams bot との会話</span><span class="sxs-lookup"><span data-stu-id="620bc-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="620bc-105">会話とは、ボットと1人以上のユーザーとの間で送信される一連のメッセージのことです。</span><span class="sxs-lookup"><span data-stu-id="620bc-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="620bc-106">Teams には、次の3種類の会話 (スコープとも呼ばれる) があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="620bc-107">`teams`チャネルの会話とも呼ばれ、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="620bc-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="620bc-108">`personal`ボットと1人のユーザーとの会話。</span><span class="sxs-lookup"><span data-stu-id="620bc-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="620bc-109">`groupChat`ボットと2人以上のユーザーとの間でチャットを行います。</span><span class="sxs-lookup"><span data-stu-id="620bc-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="620bc-110">Bot は、関係する会話の種類に応じて、微妙に動作が異なります。</span><span class="sxs-lookup"><span data-stu-id="620bc-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="620bc-111">[チャネルおよびグループチャットの会話に含まれる bot](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)は、ユーザーがチャネルで bot を呼び出すようにボットに言及する必要があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="620bc-112">[単一のユーザー会話のボットで](~/resources/bot-v3/bot-conversations/bots-conv-personal.md)は、@ メンションは必要ありません。ユーザーは単に入力できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="620bc-113">Bot が特定のスコープで機能するためには、マニフェストでその範囲をサポートするようにリストされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="620bc-114">スコープは[マニフェストの参照](~/resources/schema/manifest-schema.md)で定義され、さらに詳しく説明されています。</span><span class="sxs-lookup"><span data-stu-id="620bc-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="620bc-115">事前メッセージ</span><span class="sxs-lookup"><span data-stu-id="620bc-115">Proactive messages</span></span>

<span data-ttu-id="620bc-116">Bot は、会話に参加したり、1つ開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="620bc-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="620bc-117">ほとんどの通信は、別のメッセージに応答します。</span><span class="sxs-lookup"><span data-stu-id="620bc-117">Most communication is in response to another message.</span></span> <span data-ttu-id="620bc-118">Bot が会話を開始した場合は、"*予防的メッセージ*" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="620bc-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="620bc-119">例:</span><span class="sxs-lookup"><span data-stu-id="620bc-119">Examples include:</span></span>

* <span data-ttu-id="620bc-120">ウェルカムメッセージ</span><span class="sxs-lookup"><span data-stu-id="620bc-120">Welcome messages</span></span>
* <span data-ttu-id="620bc-121">イベント通知</span><span class="sxs-lookup"><span data-stu-id="620bc-121">Event notifications</span></span>
* <span data-ttu-id="620bc-122">ポーリングメッセージ</span><span class="sxs-lookup"><span data-stu-id="620bc-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="620bc-123">会話の基礎</span><span class="sxs-lookup"><span data-stu-id="620bc-123">Conversation basics</span></span>

<span data-ttu-id="620bc-124">各メッセージは、 `Activity`型`messageType: message`のオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="620bc-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="620bc-125">ユーザーがメッセージを送信すると、Teams がメッセージを bot に投稿します。具体的には、ユーザーは bot のメッセージングエンドポイントに JSON オブジェクトを送信します。</span><span class="sxs-lookup"><span data-stu-id="620bc-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="620bc-126">Bot は、メッセージを調べて、その種類を特定し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="620bc-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="620bc-127">Bot は、イベントスタイルのメッセージもサポートします。</span><span class="sxs-lookup"><span data-stu-id="620bc-127">Bots also support event-style messages.</span></span> <span data-ttu-id="620bc-128">詳細については、「 [Microsoft Teams のハンドル bot イベント](~/resources/bot-v3/bots-notifications.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="620bc-129">音声認識は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="620bc-129">Speech is currently not supported.</span></span>

<span data-ttu-id="620bc-130">メッセージは、すべてのスコープ間で同じようにほとんど同じですが、UI での bot へのアクセス方法と、その背後で知っておく必要がある相違点には違いがあります。</span><span class="sxs-lookup"><span data-stu-id="620bc-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="620bc-131">基本的な会話は Bot フレームワークコネクタを介して処理されます。これは、ボットが Teams やその他のチャネルと通信できるようにするための1つの REST API です。</span><span class="sxs-lookup"><span data-stu-id="620bc-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="620bc-132">Bot ビルダー SDK は、この API への簡単なアクセス、会話フローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを簡単に組み込むための簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="620bc-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="620bc-133">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="620bc-133">Message content</span></span>

<span data-ttu-id="620bc-134">Bot は、リッチテキスト、画像、およびカードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="620bc-135">ユーザーは bot にリッチテキストと画像を送信できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="620bc-136">Bot が [Microsoft Teams の設定] ページで処理できるコンテンツの種類を指定できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="620bc-137">Format</span><span class="sxs-lookup"><span data-stu-id="620bc-137">Format</span></span> | <span data-ttu-id="620bc-138">ユーザーから bot</span><span class="sxs-lookup"><span data-stu-id="620bc-138">From user to bot</span></span>  | <span data-ttu-id="620bc-139">Bot からユーザー</span><span class="sxs-lookup"><span data-stu-id="620bc-139">From bot to user</span></span> |  <span data-ttu-id="620bc-140">メモ</span><span class="sxs-lookup"><span data-stu-id="620bc-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="620bc-141">リッチ テキスト </span><span class="sxs-lookup"><span data-stu-id="620bc-141">Rich text</span></span> | <span data-ttu-id="620bc-142">✔</span><span class="sxs-lookup"><span data-stu-id="620bc-142">✔</span></span> | <span data-ttu-id="620bc-143">✔</span><span class="sxs-lookup"><span data-stu-id="620bc-143">✔</span></span> |  |
| <span data-ttu-id="620bc-144">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="620bc-144">Pictures</span></span> | <span data-ttu-id="620bc-145">✔</span><span class="sxs-lookup"><span data-stu-id="620bc-145">✔</span></span> | <span data-ttu-id="620bc-146">✔</span><span class="sxs-lookup"><span data-stu-id="620bc-146">✔</span></span> | <span data-ttu-id="620bc-147">最高1024×1024、1 MB (PNG、JPEG、または GIF 形式)アニメーション GIF はサポートされていません</span><span class="sxs-lookup"><span data-stu-id="620bc-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="620bc-148">Lcc</span><span class="sxs-lookup"><span data-stu-id="620bc-148">Cards</span></span> | <span data-ttu-id="620bc-149">✖</span><span class="sxs-lookup"><span data-stu-id="620bc-149">✖</span></span> | <span data-ttu-id="620bc-150">✔</span><span class="sxs-lookup"><span data-stu-id="620bc-150">✔</span></span> | <span data-ttu-id="620bc-151">サポートされているカードについては、 [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="620bc-152">絵文字</span><span class="sxs-lookup"><span data-stu-id="620bc-152">Emojis</span></span> | <span data-ttu-id="620bc-153">✖</span><span class="sxs-lookup"><span data-stu-id="620bc-153">✖</span></span> | <span data-ttu-id="620bc-154">✔</span><span class="sxs-lookup"><span data-stu-id="620bc-154">✔</span></span> | <span data-ttu-id="620bc-155">現在、Teams は utf-16 を介して絵文字をサポートしています (grinning フェイスの U + 1f600 など)</span><span class="sxs-lookup"><span data-stu-id="620bc-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="620bc-156">Bot フレームワークによってサポートされる bot の相互作用の種類 (teams の基礎となる bot) の詳細については、bot[ビルダー sdk for .net](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0)および[ボット builder sdk for node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)のドキュメントの bot フレームワークのドキュメントを[参照して](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0)ください。</span><span class="sxs-lookup"><span data-stu-id="620bc-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="620bc-157">メッセージの書式設定</span><span class="sxs-lookup"><span data-stu-id="620bc-157">Message formatting</span></span>

<span data-ttu-id="620bc-158">メッセージのテキストコンテンツの[`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message)表示方法を`message`制御するには、のオプションのプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="620bc-159">Bot メッセージでサポートされている書式の詳細な説明については、「[メッセージ形式](~/resources/bot-v3/bots-message-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="620bc-160">オプション[`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message)のプロパティを設定して、メッセージのテキストコンテンツの表示方法を制御することができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="620bc-161">Teams におけるテキストの書式設定のサポートの詳細については、 [bot メッセージのテキスト形式](~/resources/bot-v3/bots-text-formats.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="620bc-162">メッセージ内のカードの書式設定の詳細については、「[カードの書式](~/task-modules-and-cards/cards/cards-format.md)設定」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="620bc-163">画像メッセージ</span><span class="sxs-lookup"><span data-stu-id="620bc-163">Picture messages</span></span>

<span data-ttu-id="620bc-164">画像は、メッセージに添付ファイルを追加することによって送信されます。</span><span class="sxs-lookup"><span data-stu-id="620bc-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="620bc-165">添付ファイルの詳細については、[ボットフレームワークのドキュメント](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="620bc-166">画像は最大1024×1024で、PNG、JPEG、または GIF 形式の 1 MB にすることができます。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="620bc-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="620bc-167">XML を使用して、各画像の高さと幅を指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="620bc-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="620bc-168">Markdown を使用する場合、画像のサイズは既定で256×256に設定されています。</span><span class="sxs-lookup"><span data-stu-id="620bc-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="620bc-169">例:</span><span class="sxs-lookup"><span data-stu-id="620bc-169">For example:</span></span>

* <span data-ttu-id="620bc-170">使え`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="620bc-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="620bc-171">使用しない `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="620bc-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="620bc-172">メッセージの受信</span><span class="sxs-lookup"><span data-stu-id="620bc-172">Receiving messages</span></span>

<span data-ttu-id="620bc-173">どのスコープが宣言されているかに応じて、bot は次のコンテキストでメッセージを受信できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="620bc-174">**個人チャット**ユーザーは、チャット履歴で追加された bot を選択するか、新しいチャットの [宛先] ボックスにその名前またはアプリ ID を入力するだけで、自分のボットでプライベートな会話を操作できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="620bc-175">**チャネル**チームに追加された bot ("@_botname_") はチャネルで言及できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="620bc-176">チャネル内の bot への追加の応答には、bot に言及する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="620bc-177">記載されていない場合、返信には応答しません。</span><span class="sxs-lookup"><span data-stu-id="620bc-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="620bc-178">受信メッセージの場合、bot は型[`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) `messageType: message`のオブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="620bc-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) object of type `messageType: message`.</span></span> <span data-ttu-id="620bc-179">このオブジェクト`Activity`には、bot に送信される[チャネルの更新](~/resources/bot-v3/bots-notifications.md#channel-updates)など、他の種類の`message`情報を含めることができますが、この型は bot とユーザーの間の通信を表します。</span><span class="sxs-lookup"><span data-stu-id="620bc-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="620bc-180">Bot は、ユーザーメッセージ`Text`だけでなく、ユーザーに関するその他の情報、メッセージの送信元、Teams 情報を含むペイロードを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="620bc-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="620bc-181">注:</span><span class="sxs-lookup"><span data-stu-id="620bc-181">Of note:</span></span>

* <span data-ttu-id="620bc-182">`timestamp`協定世界時 (UTC) でのメッセージの日付と時刻</span><span class="sxs-lookup"><span data-stu-id="620bc-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="620bc-183">`localTimestamp`送信者のタイムゾーンにおけるメッセージの日付と時刻</span><span class="sxs-lookup"><span data-stu-id="620bc-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="620bc-184">`channelId`常に "msteams"。</span><span class="sxs-lookup"><span data-stu-id="620bc-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="620bc-185">これは、teams チャネルではなく bot フレームワークチャネルを参照します。</span><span class="sxs-lookup"><span data-stu-id="620bc-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="620bc-186">`from.id`Bot に対して、そのユーザーの一意で暗号化された ID。アプリでユーザーデータを格納する必要がある場合は、キーとして適しています。</span><span class="sxs-lookup"><span data-stu-id="620bc-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="620bc-187">Bot に対して一意であり、ボットインスタンス外では、そのユーザーを特定するために任意の方法で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="620bc-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="620bc-188">`channelData.tenant.id`ユーザーのテナント ID。</span><span class="sxs-lookup"><span data-stu-id="620bc-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="620bc-189">`from.id`は bot に対して一意であり、bot インスタンス外では、そのユーザーを特定するために任意の方法で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="620bc-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="620bc-190">チャネルとプライベートな相互作用を bot と組み合わせる</span><span class="sxs-lookup"><span data-stu-id="620bc-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="620bc-191">チャネルを操作する場合、ユーザーとの特定の会話をオフラインにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="620bc-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="620bc-192">たとえば、ユーザーが一連のチームメンバーとのスケジュール設定など、複雑なタスクをコーディネートしようとしているとします。</span><span class="sxs-lookup"><span data-stu-id="620bc-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="620bc-193">一連の対話がチャネルに表示されるのではなく、ユーザーに個人用チャットメッセージを送信することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="620bc-194">Bot は、状態を失わずに、個人会話とチャネル会話間でユーザーを簡単に移行できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="620bc-195">他のチームメンバーに通知するために、相互作用の完了時にチャネルを更新することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="620bc-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="620bc-196">完全な受信スキーマの例</span><span class="sxs-lookup"><span data-stu-id="620bc-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="620bc-197">受信メッセージのテキストフィールドには、メンションが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="620bc-198">適切に確認して、ストリップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="620bc-199">詳細については、「[メンション](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="620bc-200">Teams チャネルデータ</span><span class="sxs-lookup"><span data-stu-id="620bc-200">Teams channel data</span></span>

<span data-ttu-id="620bc-201">この`channelData`オブジェクトには Teams 固有の情報が含まれており、チームおよびチャネル id の最終ソースとなります。</span><span class="sxs-lookup"><span data-stu-id="620bc-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="620bc-202">これらの id は、ローカルストレージのキーとしてキャッシュして使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="620bc-203">この`channelData`オブジェクトは、チャネルの外側で行われるため、個人の会話のメッセージには含まれません。</span><span class="sxs-lookup"><span data-stu-id="620bc-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="620bc-204">Bot に送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="620bc-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="620bc-205">`eventType`Teams イベントの種類。[チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="620bc-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="620bc-206">`tenant.id`Azure Active Directory テナント ID。すべてのコンテキストで渡される</span><span class="sxs-lookup"><span data-stu-id="620bc-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="620bc-207">`team`チャネルコンテキストでのみ渡され、個人用チャットには渡されません。</span><span class="sxs-lookup"><span data-stu-id="620bc-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="620bc-208">`id`チャネルの GUID</span><span class="sxs-lookup"><span data-stu-id="620bc-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="620bc-209">`name`チームの名前。[チームの名前変更イベント](~/resources/bot-v3/bots-notifications.md#team-name-updates)の場合にのみ渡される</span><span class="sxs-lookup"><span data-stu-id="620bc-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="620bc-210">`channel`Bot が言及された場合、または bot が追加されている teams のチャネルでイベントが発生した場合に、チャネルコンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="620bc-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="620bc-211">`id`チャネルの GUID</span><span class="sxs-lookup"><span data-stu-id="620bc-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="620bc-212">`name`チャネル名。[チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="620bc-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="620bc-213">`channelData.teamsTeamId`予定.</span><span class="sxs-lookup"><span data-stu-id="620bc-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="620bc-214">このプロパティは、下位互換性のためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="620bc-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="620bc-215">`channelData.teamsChannelId`予定.</span><span class="sxs-lookup"><span data-stu-id="620bc-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="620bc-216">このプロパティは、下位互換性のためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="620bc-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="620bc-217">ChannelData オブジェクトの例 (Channeldata イベント)</span><span class="sxs-lookup"><span data-stu-id="620bc-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="620bc-218">.NET の例</span><span class="sxs-lookup"><span data-stu-id="620bc-218">.NET example</span></span>

<span data-ttu-id="620bc-219">Teams[の NuGet パッケージ](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)には、teams 固有の情報にアクセス`TeamsChannelData`するためのプロパティを公開する特別なオブジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="620bc-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="620bc-220">メッセージへの返信の送信</span><span class="sxs-lookup"><span data-stu-id="620bc-220">Sending replies to messages</span></span>

<span data-ttu-id="620bc-221">既存のメッセージに返信するには[`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) 、.net また[`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities)は node.js で呼び出します。</span><span class="sxs-lookup"><span data-stu-id="620bc-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) in Node.js.</span></span> <span data-ttu-id="620bc-222">Bot ビルダー SDK は、すべての詳細を処理します。</span><span class="sxs-lookup"><span data-stu-id="620bc-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="620bc-223">REST API の使用を選択する場合は、 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0)エンドポイントを呼び出すこともできます。</span><span class="sxs-lookup"><span data-stu-id="620bc-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) endpoint.</span></span>

<span data-ttu-id="620bc-224">メッセージコンテンツ自体には、単純なテキスト、または Bot フレームワーク提供の[カードおよびカードアクション](~/task-modules-and-cards/cards/cards-actions.md)を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="620bc-225">送信スキーマでは、受信したものと同じ`serviceUrl`を常に使用する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="620bc-226">の`serviceUrl`値は安定していますが、変更される可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="620bc-227">新しいメッセージが到着すると、ボットはに格納されて`serviceUrl`いる値を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="620bc-228">メッセージを更新する</span><span class="sxs-lookup"><span data-stu-id="620bc-228">Updating messages</span></span>

<span data-ttu-id="620bc-229">Bot は、メッセージを送信した後、メッセージをデータの静的なスナップショットにするのではなく、メッセージを送信した後にメッセージを動的に更新することができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="620bc-230">動的メッセージ更新は、投票の更新、ボタンの押した後の使用可能なアクションの変更、またはその他の非同期状態の変更などのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="620bc-231">新しいメッセージは、元の種類と一致する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="620bc-231">The new message need not match the original in type.</span></span> <span data-ttu-id="620bc-232">たとえば、元のメッセージに添付ファイルが含まれていた場合、新しいメッセージは単純なテキストメッセージにすることができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="620bc-233">単一添付ファイルメッセージおよびカルーセルレイアウトで送信されたコンテンツのみを更新できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="620bc-234">リストレイアウトに複数の添付ファイルがあるメッセージへの更新の送信はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="620bc-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="620bc-235">REST API</span><span class="sxs-lookup"><span data-stu-id="620bc-235">REST API</span></span>

<span data-ttu-id="620bc-236">メッセージ更新を発行するには、特定のアクティビティ ID を`/v3/conversations/<conversationId>/activities/<activityId>/`使用して、エンドポイントに対する PUT 要求を実行するだけです。</span><span class="sxs-lookup"><span data-stu-id="620bc-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="620bc-237">このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="620bc-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="620bc-238">.NET の例</span><span class="sxs-lookup"><span data-stu-id="620bc-238">.NET example</span></span>

<span data-ttu-id="620bc-239">Bot ビルダー SDK の`UpdateActivityAsync`メソッドを使用して、既存のメッセージを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="620bc-240">Node.js の例</span><span class="sxs-lookup"><span data-stu-id="620bc-240">Node.js example</span></span>

<span data-ttu-id="620bc-241">Bot ビルダー SDK の`session.connector.update`メソッドを使用して、既存のメッセージを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="620bc-242">会話の開始 (事前メッセージ)</span><span class="sxs-lookup"><span data-stu-id="620bc-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="620bc-243">ユーザーとの間で個人の会話を作成したり、チームの bot のチャネルで新しい返信チェーンを開始したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="620bc-244">これにより、ユーザーに対して、最初に bot との連絡を開始させずに、ユーザーにメッセージを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="620bc-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="620bc-245">詳細については、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="620bc-245">For more information, see the following topics:</span></span>

<span data-ttu-id="620bc-246">Bot が開始した会話に関する一般的な情報については、「[予防的なメッセージング」を](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="620bc-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="620bc-247">メッセージの削除</span><span class="sxs-lookup"><span data-stu-id="620bc-247">Deleting messages</span></span>

<span data-ttu-id="620bc-248">メッセージは、 [BOTBUILDER SDK](/bot-framework/bot-builder-overview-getstarted)のコネクタ[`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete)メソッドを使用して削除できます。</span><span class="sxs-lookup"><span data-stu-id="620bc-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
