---
title: ボットを使用したメッセージの送受信
description: Microsoft Teamsでボットを使用してメッセージを送受信する方法について説明Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: チームボットメッセージ
ms.date: 05/20/2019
ms.openlocfilehash: e1926afe42bca45eda5f39be1be8342452b3aa24
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566496"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="34f58-104">Microsoft Teamsボットと会話する</span><span class="sxs-lookup"><span data-stu-id="34f58-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="34f58-105">会話は、ボットと 1 人以上のユーザーとの間でやり取りされる一連のメッセージです。</span><span class="sxs-lookup"><span data-stu-id="34f58-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="34f58-106">Teams には、次の 3 種類の会話 (スコープとも呼ばれる) があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="34f58-107">`teams` チャネル会話とも呼ばれ、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="34f58-108">`personal` ボットと単一ユーザー間の会話。</span><span class="sxs-lookup"><span data-stu-id="34f58-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="34f58-109">`groupChat` ボットと複数のユーザーの間でチャットします。</span><span class="sxs-lookup"><span data-stu-id="34f58-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="34f58-110">ボットは、どのような会話に関係するかによって、少し異なる動作をします。</span><span class="sxs-lookup"><span data-stu-id="34f58-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="34f58-111">[チャネルチャットとグループチャットの会話のボット](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) では、ユーザーがチャネルで呼び出すためにボットを@mentionする必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="34f58-112">[単一ユーザー会話のボット](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) は@mentionを必要としません - ユーザーは入力するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="34f58-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @mention -  the user can just type.</span></span>

<span data-ttu-id="34f58-113">ボットが特定のスコープで動作するためには、そのスコープをサポートするマニフェストとしてリストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="34f58-114">スコープは、 [マニフェスト リファレンス](~/resources/schema/manifest-schema.md)で定義および説明します。</span><span class="sxs-lookup"><span data-stu-id="34f58-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="34f58-115">プロアクティブ メッセージ</span><span class="sxs-lookup"><span data-stu-id="34f58-115">Proactive messages</span></span>

<span data-ttu-id="34f58-116">ボットは、会話に参加したり、会話を開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="34f58-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="34f58-117">ほとんどの通信は、別のメッセージに応答しています。</span><span class="sxs-lookup"><span data-stu-id="34f58-117">Most communication is in response to another message.</span></span> <span data-ttu-id="34f58-118">ボットが会話を開始した場合は、 *プロアクティブ メッセージ* と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="34f58-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="34f58-119">たとえば、次のような情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="34f58-119">Examples include:</span></span>

* <span data-ttu-id="34f58-120">ウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="34f58-120">Welcome messages</span></span>
* <span data-ttu-id="34f58-121">イベント通知</span><span class="sxs-lookup"><span data-stu-id="34f58-121">Event notifications</span></span>
* <span data-ttu-id="34f58-122">メッセージのポーリング</span><span class="sxs-lookup"><span data-stu-id="34f58-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="34f58-123">会話の基本</span><span class="sxs-lookup"><span data-stu-id="34f58-123">Conversation basics</span></span>

<span data-ttu-id="34f58-124">各メッセージは `messageType: message` 型の `Activity` オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="34f58-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="34f58-125">ユーザーがメッセージを送信すると、Teams はそのメッセージをボットに投稿します。具体的には、ボットのメッセージング エンドポイントに JSON オブジェクトを送信します。</span><span class="sxs-lookup"><span data-stu-id="34f58-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="34f58-126">ボットはメッセージを調べて、その種類を判断し、それに応じて応答します。</span><span class="sxs-lookup"><span data-stu-id="34f58-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="34f58-127">ボットはイベント形式のメッセージもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="34f58-127">Bots also support event-style messages.</span></span> <span data-ttu-id="34f58-128">詳細については[、「Microsoft Teamsでのボット イベントの処理」を](~/resources/bot-v3/bots-notifications.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-128">For more information, see [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md).</span></span> <span data-ttu-id="34f58-129">現在、音声はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="34f58-129">Speech is currently not supported.</span></span>

<span data-ttu-id="34f58-130">メッセージは、ほとんどの場合、すべてのスコープで同じですが、UI でボットにアクセスする方法と、知る必要がある舞台裏の違いには違いがあります。</span><span class="sxs-lookup"><span data-stu-id="34f58-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="34f58-131">基本的な会話は、ボットがTeamsやその他のチャネルと通信できるようにするための単一の REST API である Bot Framework コネクタを通じて処理されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="34f58-132">Bot Builder SDK は、この API へのアクセスが簡単で、会話フローと状態を管理するための追加機能、および自然言語処理 (NLP) などのコグニティブ サービスを組み込む簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="34f58-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="34f58-133">メッセージの内容</span><span class="sxs-lookup"><span data-stu-id="34f58-133">Message content</span></span>

<span data-ttu-id="34f58-134">ボットはリッチ テキスト、画像、およびカードを送信できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="34f58-135">ユーザーは、ボットにリッチ テキストや画像を送信できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="34f58-136">ボットのMicrosoft Teams設定ページで、ボットが処理できるコンテンツの種類を指定できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="34f58-137">Format</span><span class="sxs-lookup"><span data-stu-id="34f58-137">Format</span></span> | <span data-ttu-id="34f58-138">ユーザーからボットへ</span><span class="sxs-lookup"><span data-stu-id="34f58-138">From user to bot</span></span>  | <span data-ttu-id="34f58-139">ボットからユーザーへ</span><span class="sxs-lookup"><span data-stu-id="34f58-139">From bot to user</span></span> |  <span data-ttu-id="34f58-140">備考</span><span class="sxs-lookup"><span data-stu-id="34f58-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="34f58-141">リッチ テキスト</span><span class="sxs-lookup"><span data-stu-id="34f58-141">Rich text</span></span> | <span data-ttu-id="34f58-142">✔</span><span class="sxs-lookup"><span data-stu-id="34f58-142">✔</span></span> | <span data-ttu-id="34f58-143">✔</span><span class="sxs-lookup"><span data-stu-id="34f58-143">✔</span></span> |  |
| <span data-ttu-id="34f58-144">ピクチャ</span><span class="sxs-lookup"><span data-stu-id="34f58-144">Pictures</span></span> | <span data-ttu-id="34f58-145">✔</span><span class="sxs-lookup"><span data-stu-id="34f58-145">✔</span></span> | <span data-ttu-id="34f58-146">✔</span><span class="sxs-lookup"><span data-stu-id="34f58-146">✔</span></span> | <span data-ttu-id="34f58-147">PNG、JPEG、または GIF 形式の最大 1024×1024 および 1 MB。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="34f58-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported.</span></span> |
| <span data-ttu-id="34f58-148">カード</span><span class="sxs-lookup"><span data-stu-id="34f58-148">Cards</span></span> | <span data-ttu-id="34f58-149">✖</span><span class="sxs-lookup"><span data-stu-id="34f58-149">✖</span></span> | <span data-ttu-id="34f58-150">✔</span><span class="sxs-lookup"><span data-stu-id="34f58-150">✔</span></span> | <span data-ttu-id="34f58-151">サポートされている[カードについては、Teamsカードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="34f58-152">絵文字</span><span class="sxs-lookup"><span data-stu-id="34f58-152">Emojis</span></span> | <span data-ttu-id="34f58-153">✖</span><span class="sxs-lookup"><span data-stu-id="34f58-153">✖</span></span> | <span data-ttu-id="34f58-154">✔</span><span class="sxs-lookup"><span data-stu-id="34f58-154">✔</span></span> | <span data-ttu-id="34f58-155">Teamsは現在、顔をニヤニヤするためのU + 1F600などのUTF-16経由で絵文字をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="34f58-155">Teams currently supports emojis via UTF-16 such as, U+1F600 for grinning face.</span></span> |
|

<span data-ttu-id="34f58-156">チーム内のボットが基づいているボット フレームワークでサポートされるボットの相互作用の種類の詳細については、ボット[ビルダー SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true)およびボット ビルダー SDK for Node.jsのドキュメントの[会話フロー](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true)と関連概念に関する Bot Framework のドキュメント[を](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)参照してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-156">For more information on the types of bot interaction supported by the Bot Framework, which bots in teams are based on, see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="34f58-157">メッセージの書式設定</span><span class="sxs-lookup"><span data-stu-id="34f58-157">Message formatting</span></span>

<span data-ttu-id="34f58-158">の省略可能 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) なプロパティ `message` を設定して、メッセージのテキスト コンテンツの表示方法を制御できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="34f58-159">ボット メッセージでサポートされる書式設定の詳細については、「 [メッセージの書式設定](~/resources/bot-v3/bots-message-format.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="34f58-160">オプションの [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) プロパティを設定して、メッセージのテキスト コンテンツの表示方法を制御できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="34f58-161">チームでのテキストの書式設定Teamsサポートする方法の詳細については[、「bot メッセージでのテキストの書式設定](~/resources/bot-v3/bots-text-formats.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="34f58-162">メッセージのカードの書式設定の詳細については、「 [カードの書式設定](~/task-modules-and-cards/cards/cards-format.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-162">For more information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="34f58-163">画像メッセージ</span><span class="sxs-lookup"><span data-stu-id="34f58-163">Picture messages</span></span>

<span data-ttu-id="34f58-164">画像は、メッセージに添付ファイルを追加することによって送信されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="34f58-165">添付ファイルの詳細については [、Bot Framework のドキュメントを参照してください](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="34f58-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="34f58-166">画像は、PNG、JPEG、または GIF 形式で、1024×1024 および 1 MB 以上にすることができます。アニメーション GIF はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="34f58-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="34f58-167">各画像の高さと幅は、XML を使用して指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="34f58-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="34f58-168">マークダウンを使用する場合、イメージサイズはデフォルトで 256×256 になります。</span><span class="sxs-lookup"><span data-stu-id="34f58-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="34f58-169">例:</span><span class="sxs-lookup"><span data-stu-id="34f58-169">For example:</span></span>

* <span data-ttu-id="34f58-170">`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` を使う</span><span class="sxs-lookup"><span data-stu-id="34f58-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="34f58-171">使用しない `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="34f58-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="34f58-172">メッセージの受信</span><span class="sxs-lookup"><span data-stu-id="34f58-172">Receiving messages</span></span>

<span data-ttu-id="34f58-173">宣言されているスコープに応じて、ボットは次のコンテキストでメッセージを受信できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="34f58-174">**パーソナルチャット** ユーザーは、チャット履歴で追加されたボットを選択するか、新しいチャットの [To: ] ボックスにその名前またはアプリ ID を入力するだけで、ボットとのプライベートな会話をやり取りできます。</span><span class="sxs-lookup"><span data-stu-id="34f58-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="34f58-175">**チャンネル** ボットがチームに追加されている場合、ボットはチャンネルで言及できます _(「@botname」)。_</span><span class="sxs-lookup"><span data-stu-id="34f58-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="34f58-176">チャネル内のボットに対する追加の返信には、ボットに言及する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="34f58-177">言及されていない場合は返信されません。</span><span class="sxs-lookup"><span data-stu-id="34f58-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="34f58-178">受信メッセージの場合、ボットは [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) type 型のオブジェクトを受け取ります `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="34f58-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) object of type `messageType: message`.</span></span> <span data-ttu-id="34f58-179">オブジェクトには `Activity` 、ボットに送信される [チャネルの更新](~/resources/bot-v3/bots-notifications.md#channel-updates) など、他の種類の情報を含めることができますが、この `message` 型はボットとユーザー間の通信を表します。</span><span class="sxs-lookup"><span data-stu-id="34f58-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="34f58-180">ボットは、ユーザー メッセージ、ユーザー、メッセージの `Text` ソース、およびTeams情報に関するその他の情報を含むペイロードを受信します。</span><span class="sxs-lookup"><span data-stu-id="34f58-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="34f58-181">注意:</span><span class="sxs-lookup"><span data-stu-id="34f58-181">Of note:</span></span>

* <span data-ttu-id="34f58-182">`timestamp` 世界協定時刻 (UTC) でのメッセージの日付と時刻。</span><span class="sxs-lookup"><span data-stu-id="34f58-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC).</span></span>
* <span data-ttu-id="34f58-183">`localTimestamp` 送信者のタイム ゾーン内のメッセージの日時。</span><span class="sxs-lookup"><span data-stu-id="34f58-183">`localTimestamp` The date and time of the message in the time zone of the sender.</span></span>
* <span data-ttu-id="34f58-184">`channelId` 常に"msteams"。</span><span class="sxs-lookup"><span data-stu-id="34f58-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="34f58-185">これは、チーム チャネルではなく、ボット フレームワーク チャネルを指します。</span><span class="sxs-lookup"><span data-stu-id="34f58-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="34f58-186">`from.id` ボットのそのユーザーの一意の暗号化 ID。アプリがユーザー データを格納する必要がある場合は、キーとして適しています。</span><span class="sxs-lookup"><span data-stu-id="34f58-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="34f58-187">この ID はボットに固有であり、そのユーザーを識別するために意味のある方法でボットインスタンスの外部で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="34f58-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>
* <span data-ttu-id="34f58-188">`channelData.tenant.id` ユーザーのテナント ID。</span><span class="sxs-lookup"><span data-stu-id="34f58-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="34f58-189">`from.id` はボットに固有であり、そのユーザーを識別するために意味のある方法でボットインスタンスの外部で直接使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="34f58-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="34f58-190">ボットとチャンネルとプライベートの相互作用を組み合わせる</span><span class="sxs-lookup"><span data-stu-id="34f58-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="34f58-191">チャネルで対話する場合、ボットはユーザーとの特定の会話をオフラインにすることに賢明である必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="34f58-192">たとえば、ユーザーがチーム メンバーのセットを使用してスケジュールを設定するなど、複雑なタスクを調整しようとしているとします。</span><span class="sxs-lookup"><span data-stu-id="34f58-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="34f58-193">チャネルに対して対話のシーケンス全体を表示するのではなく、ユーザーに個人用のチャット メッセージを送信することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="34f58-194">ボットは、状態を失うことなく、ユーザーの会話を簡単に個人会話とチャンネル会話に移行できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="34f58-195">他のチーム メンバーに通知するために、対話が完了したときにチャネルを更新することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="34f58-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="34f58-196">完全な受信スキーマの例</span><span class="sxs-lookup"><span data-stu-id="34f58-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="34f58-197">受信メッセージのテキスト フィールドには、メンションが含まれることがあります。</span><span class="sxs-lookup"><span data-stu-id="34f58-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="34f58-198">それらを正しくチェックして取り除くようにしてください。</span><span class="sxs-lookup"><span data-stu-id="34f58-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="34f58-199">詳細については、「 [メンション](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="34f58-200">チャネル データTeams</span><span class="sxs-lookup"><span data-stu-id="34f58-200">Teams channel data</span></span>

<span data-ttu-id="34f58-201">`channelData`このオブジェクトにはTeams固有の情報が含まれ、チーム ID とチャネル ID の決定的なソースです。</span><span class="sxs-lookup"><span data-stu-id="34f58-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="34f58-202">これらの ID をキャッシュし、ローカルストレージのキーとして使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="34f58-203">`channelData`オブジェクトは、チャネル外で行われるため、個人的な会話のメッセージには含まれません。</span><span class="sxs-lookup"><span data-stu-id="34f58-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="34f58-204">ボットに送信されるアクティビティの一般的な channelData オブジェクトには、次の情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="34f58-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="34f58-205">`eventType`Teamsイベントの種類。[チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="34f58-206">`tenant.id`Azure Active Directoryテナント ID。すべてのコンテキストで渡されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts.</span></span>
* <span data-ttu-id="34f58-207">`team` チャンネルコンテキストでのみ渡され、パーソナルチャットでは渡されません。</span><span class="sxs-lookup"><span data-stu-id="34f58-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="34f58-208">`id` チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="34f58-208">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="34f58-209">`name` チームの名前。 [チーム名変更イベント](~/resources/bot-v3/bots-notifications.md#team-name-updates)の場合にのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates).</span></span>
* <span data-ttu-id="34f58-210">`channel` ボットが言及されている場合、またはボットが追加されたチームのチャネルのイベントに対してのみ、チャネル コンテキストで渡されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="34f58-211">`id` チャネルの GUID。</span><span class="sxs-lookup"><span data-stu-id="34f58-211">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="34f58-212">`name` チャネル名。 [チャネル変更イベント](~/resources/bot-v3/bots-notifications.md#channel-updates)の場合にのみ渡されます。</span><span class="sxs-lookup"><span data-stu-id="34f58-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="34f58-213">`channelData.teamsTeamId` 廃止。</span><span class="sxs-lookup"><span data-stu-id="34f58-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="34f58-214">このプロパティは、下位互換性を保つためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="34f58-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="34f58-215">`channelData.teamsChannelId` 廃止。</span><span class="sxs-lookup"><span data-stu-id="34f58-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="34f58-216">このプロパティは、下位互換性を保つためにのみ含まれています。</span><span class="sxs-lookup"><span data-stu-id="34f58-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="34f58-217">チャネルデータ オブジェクトの例 (チャネル作成イベント)</span><span class="sxs-lookup"><span data-stu-id="34f58-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="34f58-218">.NET の例</span><span class="sxs-lookup"><span data-stu-id="34f58-218">.NET example</span></span>

<span data-ttu-id="34f58-219">[Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)パッケージには `TeamsChannelData` 、Teams固有の情報にアクセスするためのプロパティを公開する特殊なオブジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="34f58-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="34f58-220">メッセージへの返信</span><span class="sxs-lookup"><span data-stu-id="34f58-220">Sending replies to messages</span></span>

<span data-ttu-id="34f58-221">既存のメッセージに返信するには [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) 、.NET または [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) Node.jsで呼び出します。</span><span class="sxs-lookup"><span data-stu-id="34f58-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) in Node.js.</span></span> <span data-ttu-id="34f58-222">ボット ビルダー SDK では、すべての詳細を処理します。</span><span class="sxs-lookup"><span data-stu-id="34f58-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="34f58-223">REST API を使用する場合は、エンドポイントを呼び出すこともできます [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) 。</span><span class="sxs-lookup"><span data-stu-id="34f58-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) endpoint.</span></span>

<span data-ttu-id="34f58-224">メッセージの内容自体には、単純なテキストを含めることも、Bot Framework が提供する [カードやカード アクション](~/task-modules-and-cards/cards/cards-actions.md)を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="34f58-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="34f58-225">送信スキーマでは、 `serviceUrl` 常に受信したものと同じものを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="34f58-226">の値は `serviceUrl` 安定する傾向がありますが、変化する可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="34f58-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="34f58-227">新しいメッセージが到着すると、ボットは保存された値を `serviceUrl` 確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="34f58-228">メッセージの更新</span><span class="sxs-lookup"><span data-stu-id="34f58-228">Updating messages</span></span>

<span data-ttu-id="34f58-229">メッセージをデータの静的なスナップショットにするのではなく、送信後にメッセージをインラインで動的に更新できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="34f58-230">動的メッセージ更新は、ポーリングの更新、ボタンを押した後の使用可能なアクションの変更、その他の非同期状態の変更などのシナリオに使用できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="34f58-231">新しいメッセージは、元のメッセージの種類と一致する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="34f58-231">The new message need not match the original in type.</span></span> <span data-ttu-id="34f58-232">たとえば、元のメッセージに添付ファイルが含まれている場合、新しいメッセージは単純なテキスト メッセージになります。</span><span class="sxs-lookup"><span data-stu-id="34f58-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="34f58-233">単一添付ファイル メッセージおよびカルーセル レイアウトで送信されたコンテンツのみを更新できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="34f58-234">リスト レイアウトで複数の添付ファイルを含むメッセージへの更新の投稿はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="34f58-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="34f58-235">REST API</span><span class="sxs-lookup"><span data-stu-id="34f58-235">REST API</span></span>

<span data-ttu-id="34f58-236">メッセージ更新を発行するには、 `/v3/conversations/<conversationId>/activities/<activityId>/` 指定されたアクティビティ ID を使用してエンドポイントに対して PUT 要求を実行するだけです。</span><span class="sxs-lookup"><span data-stu-id="34f58-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="34f58-237">このシナリオを完了するには、元の POST 呼び出しによって返されるアクティビティ ID をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="34f58-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="34f58-238">.NET の例</span><span class="sxs-lookup"><span data-stu-id="34f58-238">.NET example</span></span>

<span data-ttu-id="34f58-239">ボット ビルダー `UpdateActivityAsync` SDK のメソッドを使用して、既存のメッセージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="34f58-240">Node.js例</span><span class="sxs-lookup"><span data-stu-id="34f58-240">Node.js example</span></span>

<span data-ttu-id="34f58-241">ボット ビルダー `session.connector.update` SDK のメソッドを使用して、既存のメッセージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="34f58-242">会話の開始 (プロアクティブなメッセージング)</span><span class="sxs-lookup"><span data-stu-id="34f58-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="34f58-243">ユーザーとの個人的な会話を作成したり、チームボットのチャネルで新しい返信チェーンを開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="34f58-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="34f58-244">これにより、ユーザーが最初にボットとの接触を開始することなく、ユーザーにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="34f58-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="34f58-245">詳細については、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="34f58-245">For more information, see the following topics:</span></span>

<span data-ttu-id="34f58-246">ボットが開始した会話の一般的な情報については [、「ボットのプロアクティブなメッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="34f58-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="34f58-247">メッセージの削除</span><span class="sxs-lookup"><span data-stu-id="34f58-247">Deleting messages</span></span>

<span data-ttu-id="34f58-248">BotBuilder SDK のコネクタ メソッドを使用してメッセージを削除できます [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) 。 [](/bot-framework/bot-builder-overview-getstarted)</span><span class="sxs-lookup"><span data-stu-id="34f58-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
