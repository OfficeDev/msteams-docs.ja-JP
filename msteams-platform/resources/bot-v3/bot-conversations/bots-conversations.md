---
title: ボットを使用してメッセージを送受信する
description: ボットを使用してメッセージを送受信する方法について説明Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: teams ボット メッセージ
ms.date: 05/20/2019
ms.openlocfilehash: efa7658aef87650e360c79523ac1c282dc4814fd
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630461"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="a7998-104">ボットと会話Microsoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="a7998-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="a7998-105">会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。</span><span class="sxs-lookup"><span data-stu-id="a7998-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="a7998-106">Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="a7998-107">`teams` チャネル会話とも呼ばれる、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a7998-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="a7998-108">`personal` ボットと 1 人のユーザーの会話。</span><span class="sxs-lookup"><span data-stu-id="a7998-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="a7998-109">`groupChat` ボットと 2 人以上のユーザーとのチャット。</span><span class="sxs-lookup"><span data-stu-id="a7998-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="a7998-110">ボットの動作は、関係する会話の種類に応じて少し異なります。</span><span class="sxs-lookup"><span data-stu-id="a7998-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="a7998-111">[チャネルチャットとグループ チャット会話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) のボットでは、ユーザーがチャネル@mentionボットを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="a7998-112">[単一のユーザーの会話の](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) ボットでは、@mentionを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @mention -  the user can just type.</span></span>

<span data-ttu-id="a7998-113">ボットが特定のスコープで動作するには、マニフェスト内のそのスコープをサポートするとして一覧表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="a7998-114">スコープはマニフェストリファレンスで定義され、さらに [説明されています](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="a7998-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="a7998-115">プロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="a7998-115">Proactive messages</span></span>

<span data-ttu-id="a7998-116">ボットは、会話に参加するか、会話を開始できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="a7998-117">ほとんどの通信は、別のメッセージに応答します。</span><span class="sxs-lookup"><span data-stu-id="a7998-117">Most communication is in response to another message.</span></span> <span data-ttu-id="a7998-118">ボットが会話を開始した場合は、プロアクティブ メッセージと *呼ばれる。*</span><span class="sxs-lookup"><span data-stu-id="a7998-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="a7998-119">たとえば、次のような情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a7998-119">Examples include:</span></span>

* <span data-ttu-id="a7998-120">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="a7998-120">Welcome messages</span></span>
* <span data-ttu-id="a7998-121">イベント通知</span><span class="sxs-lookup"><span data-stu-id="a7998-121">Event notifications</span></span>
* <span data-ttu-id="a7998-122">ポーリング メッセージ</span><span class="sxs-lookup"><span data-stu-id="a7998-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="a7998-123">会話の基本</span><span class="sxs-lookup"><span data-stu-id="a7998-123">Conversation basics</span></span>

<span data-ttu-id="a7998-124">各メッセージは `messageType: message` 型の `Activity` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="a7998-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="a7998-125">ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。</span><span class="sxs-lookup"><span data-stu-id="a7998-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="a7998-126">ボットはメッセージを調べて、その種類を特定し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="a7998-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="a7998-127">ボットは、イベント スタイルのメッセージもサポートします。</span><span class="sxs-lookup"><span data-stu-id="a7998-127">Bots also support event-style messages.</span></span> <span data-ttu-id="a7998-128">詳細については、「ボット イベントを[処理する」を参照Microsoft Teams。](~/resources/bot-v3/bots-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="a7998-128">For more information, see [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md).</span></span> <span data-ttu-id="a7998-129">音声は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a7998-129">Speech is currently not supported.</span></span>

<span data-ttu-id="a7998-130">メッセージはほとんどの場合、すべてのスコープで同じですが、ボットが UI でアクセスされる方法と、知る必要があるシーンの背後での違いがあります。</span><span class="sxs-lookup"><span data-stu-id="a7998-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="a7998-131">基本的な会話は、ボット フレームワーク コネクタ (1 つの REST API) を介して処理され、ボットが他のチャネルと通信Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="a7998-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="a7998-132">ボット ビルダー SDK は、この API への簡単なアクセス、会話のフローと状態を管理するための追加機能、自然言語処理 (NLP) などの認知サービスを組み込む簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="a7998-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="a7998-133">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="a7998-133">Message content</span></span>

<span data-ttu-id="a7998-134">ボットはリッチ テキスト、画像、カードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="a7998-135">ユーザーは、リッチ テキストと画像をボットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="a7998-136">ボットで処理できるコンテンツの種類は、ボットの [Microsoft Teams設定] ページで指定できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="a7998-137">Format</span><span class="sxs-lookup"><span data-stu-id="a7998-137">Format</span></span> | <span data-ttu-id="a7998-138">ユーザーからボットへ</span><span class="sxs-lookup"><span data-stu-id="a7998-138">From user to bot</span></span>  | <span data-ttu-id="a7998-139">ボットからユーザーへ</span><span class="sxs-lookup"><span data-stu-id="a7998-139">From bot to user</span></span> |  <span data-ttu-id="a7998-140">Notes</span><span class="sxs-lookup"><span data-stu-id="a7998-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="a7998-141">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="a7998-141">Rich text</span></span> | <span data-ttu-id="a7998-142">✔</span><span class="sxs-lookup"><span data-stu-id="a7998-142">✔</span></span> | <span data-ttu-id="a7998-143">✔</span><span class="sxs-lookup"><span data-stu-id="a7998-143">✔</span></span> |  |
| <span data-ttu-id="a7998-144">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="a7998-144">Pictures</span></span> | <span data-ttu-id="a7998-145">✔</span><span class="sxs-lookup"><span data-stu-id="a7998-145">✔</span></span> | <span data-ttu-id="a7998-146">✔</span><span class="sxs-lookup"><span data-stu-id="a7998-146">✔</span></span> | <span data-ttu-id="a7998-147">最大 1024× 1024 および 1 MB (PNG、JPEG、または GIF 形式)。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a7998-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported.</span></span> |
| <span data-ttu-id="a7998-148">カード</span><span class="sxs-lookup"><span data-stu-id="a7998-148">Cards</span></span> | <span data-ttu-id="a7998-149">✖</span><span class="sxs-lookup"><span data-stu-id="a7998-149">✖</span></span> | <span data-ttu-id="a7998-150">✔</span><span class="sxs-lookup"><span data-stu-id="a7998-150">✔</span></span> | <span data-ttu-id="a7998-151">サポートされている[カードについてはTeamsカード リファレンス](~/task-modules-and-cards/cards/cards-reference.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7998-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="a7998-152">絵文字</span><span class="sxs-lookup"><span data-stu-id="a7998-152">Emojis</span></span> | <span data-ttu-id="a7998-153">✖</span><span class="sxs-lookup"><span data-stu-id="a7998-153">✖</span></span> | <span data-ttu-id="a7998-154">✔</span><span class="sxs-lookup"><span data-stu-id="a7998-154">✔</span></span> | <span data-ttu-id="a7998-155">Teamsは現在、顔をニヤリと笑う U+1F600 など、UTF-16 経由で絵文字をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a7998-155">Teams currently supports emojis via UTF-16 such as, U+1F600 for grinning face.</span></span> |
|

<span data-ttu-id="a7998-156">チーム内のボットが基にしているボット フレームワークでサポートされるボット操作の種類の詳細については、ボット ビルダー [SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true)およびボット ビルダー SDK for Node.jsのドキュメントの会話フローと関連する概念に関するボット フレームワーク[のドキュメントを参照](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)してください。 [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a7998-156">For more information on the types of bot interaction supported by the Bot Framework, which bots in teams are based on, see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="a7998-157">メッセージの書式設定</span><span class="sxs-lookup"><span data-stu-id="a7998-157">Message formatting</span></span>

<span data-ttu-id="a7998-158">a の省略可能なプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) `message` を制御できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="a7998-159">ボット [メッセージでサポートされている](~/resources/bot-v3/bots-message-format.md) 書式設定の詳細については、「メッセージの書式設定」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7998-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="a7998-160">省略可能なプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) を制御できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="a7998-161">チームでテキストの書式設定をTeamsする方法の詳細については、「ボット メッセージの[テキストの書式設定」を参照してください](~/resources/bot-v3/bots-text-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="a7998-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="a7998-162">メッセージ内のカードの書式設定の詳細については、「カードの書式設定」 [を参照してください](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="a7998-162">For more information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="a7998-163">ピクチャ メッセージ</span><span class="sxs-lookup"><span data-stu-id="a7998-163">Picture messages</span></span>

<span data-ttu-id="a7998-164">画像は、メッセージに添付ファイルを追加して送信されます。</span><span class="sxs-lookup"><span data-stu-id="a7998-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="a7998-165">添付ファイルの詳細については、Bot Framework のドキュメント [を参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a7998-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="a7998-166">画像は、PNG、JPEG、または GIF 形式× 1024、1024、1 MB 以下の値を使用できます。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a7998-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="a7998-167">XML を使用して、各イメージの高さと幅を指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a7998-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="a7998-168">Markdown を使用する場合、画像サイズの既定値は 256 ×256 です。</span><span class="sxs-lookup"><span data-stu-id="a7998-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="a7998-169">例:</span><span class="sxs-lookup"><span data-stu-id="a7998-169">For example:</span></span>

* <span data-ttu-id="a7998-170">`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` を使う</span><span class="sxs-lookup"><span data-stu-id="a7998-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="a7998-171">使用しない `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="a7998-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages&quot;></a><span data-ttu-id=&quot;a7998-172&quot;>メッセージの受信</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;a7998-172&quot;>Receiving messages</span></span>

<span data-ttu-id=&quot;a7998-173&quot;>宣言されているスコープに応じて、ボットは次のコンテキストでメッセージを受信できます。</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;a7998-173&quot;>Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id=&quot;a7998-174&quot;>**個人用チャット** ユーザーは、チャット履歴で追加されたボットを選択するか、新しいチャットの [To:] ボックスに名前またはアプリ ID を入力するだけで、ボットとのプライベート会話で対話できます。</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;a7998-174&quot;>**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id=&quot;a7998-175&quot;>**チャネル** ボットがチームに追加されている場合は、チャネルにボット (&quot;@_botname_") を指定できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="a7998-176">チャネル内のボットに対する追加の返信には、ボットのメンションが必要です。</span><span class="sxs-lookup"><span data-stu-id="a7998-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="a7998-177">これは、記載されていない返信には応答しない。</span><span class="sxs-lookup"><span data-stu-id="a7998-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="a7998-178">受信メッセージの場合、ボットは種類 [の Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) オブジェクトを受け取ります `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="a7998-178">For incoming messages, your bot receives an [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object of type `messageType: message`.</span></span> <span data-ttu-id="a7998-179">オブジェクトには、ボットに送信されるチャネル更新など、他の種類の情報を含めすることもできますが、この型はボットとユーザーの間 `Activity` [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` の通信を表します。</span><span class="sxs-lookup"><span data-stu-id="a7998-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="a7998-180">ボットは、ユーザー メッセージ、ユーザーに関するその他の情報、メッセージのソース、およびユーザー情報を含む `Text` ペイロードをTeamsします。</span><span class="sxs-lookup"><span data-stu-id="a7998-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="a7998-181">注:</span><span class="sxs-lookup"><span data-stu-id="a7998-181">Of note:</span></span>

* <span data-ttu-id="a7998-182">`timestamp` 協定世界時 (UTC) のメッセージの日付と時刻。</span><span class="sxs-lookup"><span data-stu-id="a7998-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC).</span></span>
* <span data-ttu-id="a7998-183">`localTimestamp` 送信者のタイム ゾーン内のメッセージの日付と時刻。</span><span class="sxs-lookup"><span data-stu-id="a7998-183">`localTimestamp` The date and time of the message in the time zone of the sender.</span></span>
* <span data-ttu-id="a7998-184">`channelId` 常に "msteams" 。</span><span class="sxs-lookup"><span data-stu-id="a7998-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="a7998-185">これは、チーム チャネルではなく、ボット フレームワーク チャネルを指します。</span><span class="sxs-lookup"><span data-stu-id="a7998-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="a7998-186">`from.id` ボットのユーザーの一意で暗号化された ID。アプリがユーザー データを保存する必要がある場合は、キーとして適しています。</span><span class="sxs-lookup"><span data-stu-id="a7998-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="a7998-187">これはボットにとって一意であり、そのユーザーを識別する意味のある方法でボット インスタンスの外部で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="a7998-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>
* <span data-ttu-id="a7998-188">`channelData.tenant.id` ユーザーのテナント ID。</span><span class="sxs-lookup"><span data-stu-id="a7998-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="a7998-189">`from.id` はボットにとって一意であり、そのユーザーを識別する意味のある方法でボット インスタンスの外部で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="a7998-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="a7998-190">チャネルとプライベート操作をボットと組み合わせる</span><span class="sxs-lookup"><span data-stu-id="a7998-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="a7998-191">チャネルで操作する場合、ボットはユーザーとの特定の会話をオフラインにした方が良い必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="a7998-192">たとえば、ユーザーがチーム メンバーのセットとのスケジュール設定など、複雑なタスクを調整しようとしているとします。</span><span class="sxs-lookup"><span data-stu-id="a7998-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="a7998-193">一連の操作全体をチャネルに表示するのではなく、ユーザーに個人的なチャット メッセージを送信する方法を検討してください。</span><span class="sxs-lookup"><span data-stu-id="a7998-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="a7998-194">ボットは、状態を失わずに、個人とチャネルの会話の間でユーザーを簡単に移行できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="a7998-195">他のチーム メンバーに通知する操作が完了したら、チャネルを更新することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="a7998-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="a7998-196">完全な受信スキーマの例</span><span class="sxs-lookup"><span data-stu-id="a7998-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="a7998-197">受信メッセージのテキスト フィールドにメンションが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="a7998-198">適切にチェックして、それらのファイルを取り除く必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="a7998-199">詳細については、「メンション」 [を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。</span><span class="sxs-lookup"><span data-stu-id="a7998-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="a7998-200">Teamsチャネル データ</span><span class="sxs-lookup"><span data-stu-id="a7998-200">Teams channel data</span></span>

<span data-ttu-id="a7998-201">このオブジェクトには、Teams固有の情報が含まれているので、チームとチャネルの ID の決定的 `channelData` なソースです。</span><span class="sxs-lookup"><span data-stu-id="a7998-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="a7998-202">これらの ID をキャッシュし、ローカル ストレージのキーとして使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="a7998-203">オブジェクトは、チャネルの外部で行なうので、個人の会話 `channelData` のメッセージには含まれません。</span><span class="sxs-lookup"><span data-stu-id="a7998-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="a7998-204">ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a7998-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="a7998-205">`eventType`Teamsイベントの種類。チャネル変更イベントの場合[にのみ渡されます](~/resources/bot-v3/bots-notifications.md#channel-updates)。</span><span class="sxs-lookup"><span data-stu-id="a7998-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="a7998-206">`tenant.id`Azure Active Directory ID。すべてのコンテキストで渡されます。</span><span class="sxs-lookup"><span data-stu-id="a7998-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts.</span></span>
* <span data-ttu-id="a7998-207">`team` 個人チャットではなく、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="a7998-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="a7998-208">`id` チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="a7998-208">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="a7998-209">`name` チームの名前。チームの名前変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#team-name-updates)。</span><span class="sxs-lookup"><span data-stu-id="a7998-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates).</span></span>
* <span data-ttu-id="a7998-210">`channel` ボットが言及されている場合、またはボットが追加されたチームのチャネル内のイベントに対して、チャネル コンテキストでのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="a7998-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="a7998-211">`id` チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="a7998-211">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="a7998-212">`name` チャネル名。チャネル変更イベントの場合 [にのみ渡されます](~/resources/bot-v3/bots-notifications.md#channel-updates)。</span><span class="sxs-lookup"><span data-stu-id="a7998-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="a7998-213">`channelData.teamsTeamId` 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="a7998-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="a7998-214">このプロパティは、下位互換性の場合にのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="a7998-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="a7998-215">`channelData.teamsChannelId` 非推奨です。</span><span class="sxs-lookup"><span data-stu-id="a7998-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="a7998-216">このプロパティは、下位互換性の場合にのみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="a7998-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="a7998-217">channelData オブジェクトの例 (channelCreated イベント)</span><span class="sxs-lookup"><span data-stu-id="a7998-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="a7998-218">.NET の例</span><span class="sxs-lookup"><span data-stu-id="a7998-218">.NET example</span></span>

<span data-ttu-id="a7998-219">[Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)パッケージには、特定の情報にアクセスするプロパティTeams `TeamsChannelData` が提供されます。</span><span class="sxs-lookup"><span data-stu-id="a7998-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="a7998-220">メッセージへの返信の送信</span><span class="sxs-lookup"><span data-stu-id="a7998-220">Sending replies to messages</span></span>

<span data-ttu-id="a7998-221">既存のメッセージに返信するには [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) 、.NET を呼び出すか、Node.js。 [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a7998-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) in Node.js.</span></span> <span data-ttu-id="a7998-222">ボット ビルダー SDK は、すべての詳細を処理します。</span><span class="sxs-lookup"><span data-stu-id="a7998-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="a7998-223">REST API を使用する場合は、エンドポイントを呼び出 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7998-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) endpoint.</span></span>

<span data-ttu-id="a7998-224">メッセージ コンテンツ自体には、単純なテキストや、Bot Framework が提供するカードとカード [アクションの一部を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="a7998-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="a7998-225">送信スキーマでは、受信したスキーマと常に同じ `serviceUrl` 値を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="a7998-226">値は安定している傾向がありますが、変更 `serviceUrl` される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="a7998-227">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要があります `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="a7998-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="a7998-228">メッセージの更新</span><span class="sxs-lookup"><span data-stu-id="a7998-228">Updating messages</span></span>

<span data-ttu-id="a7998-229">メッセージをデータの静的スナップショットにするのではなく、ボットはメッセージを送信した後、インラインで動的にメッセージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="a7998-230">ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオで、動的メッセージ更新を使用できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="a7998-231">新しいメッセージは、型の元のメッセージと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-231">The new message need not match the original in type.</span></span> <span data-ttu-id="a7998-232">たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージは単純なテキスト メッセージになります。</span><span class="sxs-lookup"><span data-stu-id="a7998-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="a7998-233">単一添付メッセージとカルーセル レイアウトで送信されるコンテンツのみを更新できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="a7998-234">リスト レイアウトで複数の添付ファイルを含むメッセージへの更新の投稿はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a7998-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="a7998-235">REST API</span><span class="sxs-lookup"><span data-stu-id="a7998-235">REST API</span></span>

<span data-ttu-id="a7998-236">メッセージ更新を発行するには、特定のアクティビティ ID を使用してエンドポイントに対して PUT 要求 `/v3/conversations/<conversationId>/activities/<activityId>/` を実行します。</span><span class="sxs-lookup"><span data-stu-id="a7998-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="a7998-237">このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7998-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="a7998-238">.NET の例</span><span class="sxs-lookup"><span data-stu-id="a7998-238">.NET example</span></span>

<span data-ttu-id="a7998-239">ボット ビルダー SDK の `UpdateActivityAsync` メソッドを使用して、既存のメッセージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="a7998-240">Node.js例</span><span class="sxs-lookup"><span data-stu-id="a7998-240">Node.js example</span></span>

<span data-ttu-id="a7998-241">ボット ビルダー SDK の `session.connector.update` メソッドを使用して、既存のメッセージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="a7998-242">会話の開始 (プロアクティブ メッセージング)</span><span class="sxs-lookup"><span data-stu-id="a7998-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="a7998-243">ユーザーとの個人的な会話を作成するか、チーム ボットのチャネルで新しい返信チェーンを開始できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="a7998-244">これにより、ユーザーまたはユーザーに最初にボットとの接触を開始せずにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="a7998-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="a7998-245">詳細については、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a7998-245">For more information, see the following topics:</span></span>

<span data-ttu-id="a7998-246">ボット [によって開始される会話の詳細については、「](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) ボットのプロアクティブ メッセージング」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7998-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="a7998-247">メッセージの削除</span><span class="sxs-lookup"><span data-stu-id="a7998-247">Deleting messages</span></span>

<span data-ttu-id="a7998-248">メッセージは、BotBuilder SDK の connectors メソッドを使用 [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) [して削除できます](/bot-framework/bot-builder-overview-getstarted)。</span><span class="sxs-lookup"><span data-stu-id="a7998-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
