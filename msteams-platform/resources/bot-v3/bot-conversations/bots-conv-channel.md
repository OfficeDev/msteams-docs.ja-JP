---
title: ボットを使用したチャネルとグループチャットの会話
description: Microsoft Teams のチャネルで bot との会話を行うエンドツーエンドのシナリオについて説明します。
keywords: teams シナリオチャネル会話 bot
ms.date: 06/25/2019
ms.openlocfilehash: f44db4a88ab5e6541c52395a58fc643cb07df606
ms.sourcegitcommit: b3962a7b36f260aef1af9124d14d71ae08b01ac4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "47303725"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="ff159-104">Microsoft Teams ボットとのチャネルおよびグループ チャット会話</span><span class="sxs-lookup"><span data-stu-id="ff159-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ff159-105">Microsoft Teams を使用すると、ユーザーは自分のチャネルまたはグループのチャット会話に bot を提供できます。</span><span class="sxs-lookup"><span data-stu-id="ff159-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="ff159-106">チームまたはチャットに bot を追加することで、会話のすべてのユーザーは、会話の bot 機能を利用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ff159-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="ff159-107">チーム情報のクエリやユーザーの @mentioning など、ボット内の Teams 固有の機能にアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ff159-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="ff159-108">チャネルおよびグループチャットでのチャットは、ユーザーが bot @mention する必要があるという点で、個人チャットとは異なります。</span><span class="sxs-lookup"><span data-stu-id="ff159-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="ff159-109">Bot が複数の範囲 (personal、groupchat または channel) で使用されている場合は、ボットメッセージの送信元のスコープを検出し、それに応じて処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff159-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="ff159-110">チャネルまたはグループ向けに優位な bot を設計する</span><span class="sxs-lookup"><span data-stu-id="ff159-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="ff159-111">チームに追加されたボットは別のチームメンバーとなり、会話の一部として @mentioned できます。</span><span class="sxs-lookup"><span data-stu-id="ff159-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="ff159-112">実際には、ボットは @mentioned ときにのみメッセージを受信するので、チャネルの他の会話は bot に送信されません。</span><span class="sxs-lookup"><span data-stu-id="ff159-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="ff159-113">グループまたはチャネル内の bot は、すべてのメンバーに関連する情報を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff159-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="ff159-114">ボットは確かに、その環境に関連する情報をすべて提供できるようになりますが、すべてのユーザーが見ることができるように注意してください。</span><span class="sxs-lookup"><span data-stu-id="ff159-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="ff159-115">そのため、グループまたはチャネル内の大 bot は、すべてのユーザーに値を追加する必要があります。また、1対1の会話により適切な情報を誤って共有することはありません。</span><span class="sxs-lookup"><span data-stu-id="ff159-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="ff159-116">Bot の場合と同様に、追加の作業を必要とせず、すべてのスコープに完全に関連することができます。</span><span class="sxs-lookup"><span data-stu-id="ff159-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="ff159-117">Microsoft Teams では、bot がすべてのスコープで機能することを想定していませんが、ボットがサポートする範囲内でユーザー値を提供していることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff159-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="ff159-118">範囲の詳細については、「 [Microsoft Teams のアプリ](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff159-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="ff159-119">グループまたはチャネルで機能する bot を開発すると、個人の会話と同じ機能の多くが使用されます。</span><span class="sxs-lookup"><span data-stu-id="ff159-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="ff159-120">ペイロードの追加のイベントとデータは、Teams グループとチャネル情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="ff159-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="ff159-121">次のセクションでは、これらの相違点と、共通機能の主な違いについて説明します。</span><span class="sxs-lookup"><span data-stu-id="ff159-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="ff159-122">メッセージを作成する</span><span class="sxs-lookup"><span data-stu-id="ff159-122">Creating messages</span></span>

<span data-ttu-id="ff159-123">ボットの詳細については、「 [bot の](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)メッセージを作成する」および「特に [チャネル会話を作成](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff159-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="ff159-124">メッセージの受信</span><span class="sxs-lookup"><span data-stu-id="ff159-124">Receiving messages</span></span>

<span data-ttu-id="ff159-125">[通常のメッセージスキーマ](https://docs.botframework.com/core-concepts/reference/#activity)に加えて、グループまたはチャネル内の bot の場合、bot は次のプロパティも受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ff159-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="ff159-126">`channelData` 「 [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff159-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="ff159-127">グループチャットには、そのチャットに固有の情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ff159-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="ff159-128">`conversation.id` 応答チェーン ID。チャネル ID と、返信チェーン内の最初のメッセージの ID で構成されます。</span><span class="sxs-lookup"><span data-stu-id="ff159-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="ff159-129">`conversation.isGroup``true`チャネルまたはグループチャットのボットメッセージ用</span><span class="sxs-lookup"><span data-stu-id="ff159-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="ff159-130">`conversation.conversationType``groupChat`あるいは`channel`</span><span class="sxs-lookup"><span data-stu-id="ff159-130">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="ff159-131">`entities` 1つ以上のメンションを含めることができます ( [メンション](#-mentions)を参照してください)</span><span class="sxs-lookup"><span data-stu-id="ff159-131">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="ff159-132">メッセージへの返信</span><span class="sxs-lookup"><span data-stu-id="ff159-132">Replying to messages</span></span>

<span data-ttu-id="ff159-133">既存のメッセージに返信するに [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) は、.net または [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.js で呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ff159-133">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="ff159-134">Bot ビルダー SDK は、すべての詳細を処理します。</span><span class="sxs-lookup"><span data-stu-id="ff159-134">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="ff159-135">REST API の使用を選択する場合は、エンドポイントを呼び出すこともでき [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) ます。</span><span class="sxs-lookup"><span data-stu-id="ff159-135">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="ff159-136">チャネルでは、メッセージへの返信として、開始側の返信チェインへの返信として表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff159-136">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="ff159-137">には、 `conversation.id` チャネルとトップレベルのメッセージ ID が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ff159-137">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="ff159-138">Bot フレームワークは詳細を考慮していますが、必要に応じ `conversation.id` て、その会話スレッドへの今後の返信のためにキャッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="ff159-138">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="ff159-139">ベストプラクティス: Teams でのウェルカムメッセージ</span><span class="sxs-lookup"><span data-stu-id="ff159-139">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="ff159-140">Bot が初めてグループまたはチームに追加されると、すべてのユーザーに bot を紹介するウェルカムメッセージを送信すると便利です。</span><span class="sxs-lookup"><span data-stu-id="ff159-140">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="ff159-141">ウェルカムメッセージには、bot の機能とユーザーの利点についての説明が記載されています。</span><span class="sxs-lookup"><span data-stu-id="ff159-141">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="ff159-142">メッセージには、ユーザーがアプリを操作するためのコマンドも含めることが理想的です。</span><span class="sxs-lookup"><span data-stu-id="ff159-142">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="ff159-143">これを行うには、bot がメッセージに応答して `conversationUpdate` 、オブジェクトに eventType があることを確認し `teamsAddMembers` `channelData` ます。</span><span class="sxs-lookup"><span data-stu-id="ff159-143">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="ff159-144">`memberAdded`ユーザーがチームに追加されたときに同じイベントが送信されるので、ID が bot のアプリ id 自体であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="ff159-144">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="ff159-145">詳細について [は、「Team member or bot の追加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff159-145">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="ff159-146">Bot が追加されたときに、チームの各メンバーに個人メッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="ff159-146">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="ff159-147">これを行うには、 [チーム名簿を取得](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) して、各ユーザーを [直接メッセージ](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)として送信することができます。</span><span class="sxs-lookup"><span data-stu-id="ff159-147">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="ff159-148">次の状況では、お客様がウェルカムメッセージを送信し *ない* ことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ff159-148">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="ff159-149">チームは大規模です (ただし、100メンバーよりも大きいなど)。</span><span class="sxs-lookup"><span data-stu-id="ff159-149">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="ff159-150">Bot が "spammy" と表示されている可能性があります。これを追加したユーザーは、ウェルカムメッセージが表示されるすべてのユーザーに bot の価値提案を明確に伝えない限り、苦情を受けることがあります。</span><span class="sxs-lookup"><span data-stu-id="ff159-150">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="ff159-151">Bot は、最初にグループまたはチャネルで言及されます (チームに最初に追加されるものではありません)。</span><span class="sxs-lookup"><span data-stu-id="ff159-151">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="ff159-152">グループまたはチャネルの名前が変更された</span><span class="sxs-lookup"><span data-stu-id="ff159-152">A group or channel is renamed</span></span>
* <span data-ttu-id="ff159-153">チームメンバーがグループまたはチャネルに追加される</span><span class="sxs-lookup"><span data-stu-id="ff159-153">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="ff159-154">@ メンション</span><span class="sxs-lookup"><span data-stu-id="ff159-154">@ Mentions</span></span>

<span data-ttu-id="ff159-155">グループまたはチャネル内のボットは、メッセージ内の bot ("@_botname_") に記述されている場合にのみ応答するため、グループチャネル内の bot が受信するすべてのメッセージには独自の名前が含まれており、メッセージ解析がそれを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff159-155">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="ff159-156">また、bot は、前述の他のユーザーを分析し、ユーザーにメッセージの一部として言及することができます。</span><span class="sxs-lookup"><span data-stu-id="ff159-156">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="ff159-157">メンションの取得</span><span class="sxs-lookup"><span data-stu-id="ff159-157">Retrieving mentions</span></span>

<span data-ttu-id="ff159-158">メンションは、 `entities` ペイロードのオブジェクトに返され、ユーザーの一意の ID と、通常はユーザーの名前の両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ff159-158">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="ff159-159">メッセージ内のすべてのメンションを取得するには、 `GetMentions` Bot ビルダー SDK の関数を呼び出します。これは、オブジェクトの配列を返し `Mentioned` ます。</span><span class="sxs-lookup"><span data-stu-id="ff159-159">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="ff159-160">.NET のコード例: @bot 言及していることを確認して削除する</span><span class="sxs-lookup"><span data-stu-id="ff159-160">.NET example code: Check for and strip @bot mention</span></span>

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> <span data-ttu-id="ff159-161">Teams 拡張機能を使用して、 `GetTextWithoutMentions` bot を含むすべてのメンションをストリップすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ff159-161">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="ff159-162">Node.js コード例: @bot 言及することを確認し、削除します。</span><span class="sxs-lookup"><span data-stu-id="ff159-162">Node.js example code: Check for and strip @bot mention</span></span>

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

<span data-ttu-id="ff159-163">Teams 拡張機能を使用して、 `getTextWithoutMentions` bot を含むすべてのメンションをストリップすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ff159-163">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="ff159-164">メンションの構築</span><span class="sxs-lookup"><span data-stu-id="ff159-164">Constructing mentions</span></span>

<span data-ttu-id="ff159-165">Bot は、チャネルに投稿されたメッセージに他のユーザーを伝えます。</span><span class="sxs-lookup"><span data-stu-id="ff159-165">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="ff159-166">これを行うには、メッセージで次の操作を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff159-166">To do this, your message must do the following:</span></span>

* <span data-ttu-id="ff159-167">`<at>@username</at>`メッセージテキストに含める</span><span class="sxs-lookup"><span data-stu-id="ff159-167">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="ff159-168">オブジェクトを `mention` entities コレクション内に含める</span><span class="sxs-lookup"><span data-stu-id="ff159-168">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="ff159-169">.NET の例</span><span class="sxs-lookup"><span data-stu-id="ff159-169">.NET example</span></span>

<span data-ttu-id="ff159-170">この例では、 [Microsoft の Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="ff159-170">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="ff159-171">Node.js の例</span><span class="sxs-lookup"><span data-stu-id="ff159-171">Node.js example</span></span>

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="ff159-172">例: ユーザーが説明した送信メッセージ</span><span class="sxs-lookup"><span data-stu-id="ff159-172">Example: Outgoing message with user mentioned</span></span>

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="ff159-173">GroupChat またはチャネルスコープへのアクセス</span><span class="sxs-lookup"><span data-stu-id="ff159-173">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="ff159-174">Bot は、グループと teams でメッセージを送受信することができます。</span><span class="sxs-lookup"><span data-stu-id="ff159-174">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="ff159-175">たとえば、プロファイル情報やチャネルの一覧を含む、メンバーの一覧を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="ff159-175">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="ff159-176">詳細については [、「Microsoft Teams の bot のコンテキストを取得](~/resources/bot-v3/bots-context.md) する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff159-176">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="ff159-177">[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="ff159-177">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
