---
title: ボットとのチャネルチャットとグループ チャットの会話
description: チャネル内でボットと会話を行うエンドツーエンドのシナリオについて説明Microsoft Teams
keywords: チームのシナリオ チャネルの会話ボット
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: 2eac067a75fc75c9991e8b30ec5d693d89ed8228
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019798"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="c757e-104">Microsoft Teams ボットとのチャネルおよびグループ チャット会話</span><span class="sxs-lookup"><span data-stu-id="c757e-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="c757e-105">Microsoft Teamsは、ユーザーが自分のチャネルまたはグループ チャットの会話にボットを取り込むのを許可します。</span><span class="sxs-lookup"><span data-stu-id="c757e-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="c757e-106">チームまたはチャットにボットを追加すると、会話のすべてのユーザーが会話でボット機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="c757e-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="c757e-107">また、チーム情報のTeamsユーザーのクエリなど、ボット内の特定の機能@mentioningできます。</span><span class="sxs-lookup"><span data-stu-id="c757e-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="c757e-108">チャネルやグループ チャットでのチャットは、ユーザーがボットにアクセスする必要があるという点@mention異なります。</span><span class="sxs-lookup"><span data-stu-id="c757e-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="c757e-109">ボットが複数のスコープ (個人用、グループチャット、またはチャネル) で使用されている場合は、ボット メッセージが送信されたスコープを検出し、その範囲に応じて処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="c757e-110">チャネルまたはグループに最適なボットを設計する</span><span class="sxs-lookup"><span data-stu-id="c757e-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="c757e-111">チームに追加されたボットは、別のチーム メンバーになり、会話@mentionedに使用できます。</span><span class="sxs-lookup"><span data-stu-id="c757e-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="c757e-112">実際、ボットはメッセージを受信するときにのみ受信@mentioned、チャネル上の他の会話はボットに送信されません。</span><span class="sxs-lookup"><span data-stu-id="c757e-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="c757e-113">グループまたはチャネルのボットは、すべてのメンバーに関連する適切な情報を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="c757e-114">ボットはエクスペリエンスに関連する情報を確実に提供することができますが、ボットとの会話は誰にでも表示されます。</span><span class="sxs-lookup"><span data-stu-id="c757e-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="c757e-115">したがって、グループまたはチャネルの優良なボットは、すべてのユーザーに価値を追加し、1 対 1 の会話に適した情報を誤って共有する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="c757e-116">ボットは、同様に、追加の作業を必要とせずに、すべてのスコープで完全に関連している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="c757e-117">このMicrosoft Teams、すべてのスコープでボットが機能するとは思いもよらありませんが、ボットがサポートを選択したスコープでユーザー値を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="c757e-118">スコープの詳細については、「App [in Microsoft Teams」を参照してください](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c757e-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="c757e-119">グループまたはチャネルで動作するボットの開発では、個人の会話と同じ機能の多くを使用します。</span><span class="sxs-lookup"><span data-stu-id="c757e-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="c757e-120">ペイロード内の追加のイベントとデータは、Teamsチャネル情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="c757e-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="c757e-121">これらの違い、および一般的な機能の主な違いについては、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="c757e-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="c757e-122">メッセージの作成</span><span class="sxs-lookup"><span data-stu-id="c757e-122">Creating messages</span></span>

<span data-ttu-id="c757e-123">チャネルでメッセージを作成するボットの詳細については、「 [ボットのプロ](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)アクティブ メッセージング」および「特にチャネル会話の作成 [」を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。</span><span class="sxs-lookup"><span data-stu-id="c757e-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="c757e-124">メッセージの受信</span><span class="sxs-lookup"><span data-stu-id="c757e-124">Receiving messages</span></span>

<span data-ttu-id="c757e-125">グループまたはチャネル内のボットの場合、通常のメッセージ[](https://docs.botframework.com/core-concepts/reference/#activity)スキーマに加えて、ボットは次のプロパティも受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c757e-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="c757e-126">`channelData`「チャネル[Teams」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。</span><span class="sxs-lookup"><span data-stu-id="c757e-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="c757e-127">グループ チャットには、そのチャットに固有の情報が含まれる。</span><span class="sxs-lookup"><span data-stu-id="c757e-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="c757e-128">`conversation.id` チャネル ID と返信チェーン内の最初のメッセージの ID で構成される応答チェーン ID</span><span class="sxs-lookup"><span data-stu-id="c757e-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="c757e-129">`conversation.isGroup` チャネル `true` またはグループ チャットのボット メッセージ用です</span><span class="sxs-lookup"><span data-stu-id="c757e-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="c757e-130">`conversation.conversationType` どちらか `groupChat` または `channel`</span><span class="sxs-lookup"><span data-stu-id="c757e-130">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="c757e-131">`entities`1 つ以上のメンションを含めできます (「[メンション」を参照)。](#-mentions)</span><span class="sxs-lookup"><span data-stu-id="c757e-131">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="c757e-132">メッセージへの返信</span><span class="sxs-lookup"><span data-stu-id="c757e-132">Replying to messages</span></span>

<span data-ttu-id="c757e-133">既存のメッセージに返信するには [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) 、.NET を呼び出すか、Node.js。 [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler)</span><span class="sxs-lookup"><span data-stu-id="c757e-133">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="c757e-134">ボット ビルダー SDK は、すべての詳細を処理します。</span><span class="sxs-lookup"><span data-stu-id="c757e-134">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="c757e-135">REST API を使用する場合は、エンドポイントを呼び出 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) することもできます。</span><span class="sxs-lookup"><span data-stu-id="c757e-135">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="c757e-136">チャネルでは、メッセージに返信すると、開始する返信チェーンへの返信として表示されます。</span><span class="sxs-lookup"><span data-stu-id="c757e-136">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="c757e-137">チャネル `conversation.id` とトップ レベルのメッセージ ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="c757e-137">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="c757e-138">ボット フレームワークは詳細を処理しますが、必要に応じて、その会話スレッドに対する今後の返信のためにキャッシュ `conversation.id` できます。</span><span class="sxs-lookup"><span data-stu-id="c757e-138">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="c757e-139">ベスト プラクティス: ウェルカム メッセージ (Teams</span><span class="sxs-lookup"><span data-stu-id="c757e-139">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="c757e-140">ボットが最初にグループまたはチームに追加される場合は、通常、ボットを紹介するウェルカム メッセージをすべてのユーザーに送信すると便利です。</span><span class="sxs-lookup"><span data-stu-id="c757e-140">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="c757e-141">ウェルカム メッセージには、ボットの機能とユーザーの利点の説明が記載されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-141">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="c757e-142">理想的には、メッセージには、ユーザーがアプリを操作するためのコマンドも含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-142">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="c757e-143">これを行うには、ボットがメッセージに応答し、オブジェクトに `conversationUpdate` `teamsAddMembers` eventType が含まれることを確認 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="c757e-143">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="c757e-144">ユーザーがチームに追加された場合に同じイベントが送信されるので、ID がボットのアプリ ID 自体 `memberAdded` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-144">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="c757e-145">詳細については [、「チーム メンバーまたはボットの追加」](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c757e-145">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="c757e-146">ボットを追加するときに、チームの各メンバーに個人用メッセージを送信する場合があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-146">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="c757e-147">これを行うには、チーム名 [簿を](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) フェッチし、各ユーザーに直接メッセージを [送信します](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="c757e-147">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="c757e-148">次の状況では *、ボットが* ウェルカム メッセージを送信しなかすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c757e-148">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="c757e-149">チームは大きい (明らかに主観的ですが、たとえば 100 人を超えるメンバー)。</span><span class="sxs-lookup"><span data-stu-id="c757e-149">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="c757e-150">ボットは "spammy" と見なされ、追加したユーザーは、ウェルカム メッセージを見たすべてのユーザーにボットの価値提案を明確に伝えない限り、苦情を受け取る可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-150">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="c757e-151">ボットは、最初にグループまたはチャネルで言及されます (最初にチームに追加される場合と比較して)</span><span class="sxs-lookup"><span data-stu-id="c757e-151">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="c757e-152">グループまたはチャネルの名前が変更される</span><span class="sxs-lookup"><span data-stu-id="c757e-152">A group or channel is renamed</span></span>
* <span data-ttu-id="c757e-153">チーム メンバーがグループまたはチャネルに追加される</span><span class="sxs-lookup"><span data-stu-id="c757e-153">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="c757e-154">@ メンション</span><span class="sxs-lookup"><span data-stu-id="c757e-154">@ Mentions</span></span>

<span data-ttu-id="c757e-155">グループまたはチャネル内のボットは、メッセージに ("@_botname_") と記載されている場合にのみ応答しますので、グループ チャネル内のボットによって受信されるメッセージには、その名前が含まれているため、メッセージ解析で処理を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-155">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="c757e-156">さらに、ボットは、メッセージの一部として言及された他のユーザーを解析し、ユーザーに言及することもできます。</span><span class="sxs-lookup"><span data-stu-id="c757e-156">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="c757e-157">メンションの取得</span><span class="sxs-lookup"><span data-stu-id="c757e-157">Retrieving mentions</span></span>

<span data-ttu-id="c757e-158">メンションはペイロード内のオブジェクトで返され、ユーザーの一意の ID と、ほとんどの場合、言及されたユーザーの `entities` 名前の両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c757e-158">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="c757e-159">メッセージ内のすべてのメンションを取得するには、オブジェクトの配列を返す .NET 用ボット ビルダー SDK で関数 `GetMentions` を呼び出 `Mentioned` します。</span><span class="sxs-lookup"><span data-stu-id="c757e-159">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="c757e-160">.NET サンプル コード: メンションの確認と@botする</span><span class="sxs-lookup"><span data-stu-id="c757e-160">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="c757e-161">ボットを含むすべてのTeamsを取り除く拡張機能を使用 `GetTextWithoutMentions` することもできます。</span><span class="sxs-lookup"><span data-stu-id="c757e-161">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="c757e-162">Node.jsコードの例: メンションの確認と@botする</span><span class="sxs-lookup"><span data-stu-id="c757e-162">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="c757e-163">ボットを含むすべてのTeamsを取り除く拡張機能を使用 `getTextWithoutMentions` することもできます。</span><span class="sxs-lookup"><span data-stu-id="c757e-163">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="c757e-164">メンションの作成</span><span class="sxs-lookup"><span data-stu-id="c757e-164">Constructing mentions</span></span>

<span data-ttu-id="c757e-165">ボットは、チャネルに投稿されたメッセージで他のユーザーに言及できます。</span><span class="sxs-lookup"><span data-stu-id="c757e-165">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="c757e-166">これを行うには、メッセージで次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="c757e-166">To do this, your message must do the following:</span></span>

* <span data-ttu-id="c757e-167">メッセージ `<at>@username</at>` テキストに含める</span><span class="sxs-lookup"><span data-stu-id="c757e-167">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="c757e-168">エンティティ コレクション `mention` 内にオブジェクトを含める</span><span class="sxs-lookup"><span data-stu-id="c757e-168">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="c757e-169">.NET の例</span><span class="sxs-lookup"><span data-stu-id="c757e-169">.NET example</span></span>

<span data-ttu-id="c757e-170">この例では[、Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)します。</span><span class="sxs-lookup"><span data-stu-id="c757e-170">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="c757e-171">Node.js例</span><span class="sxs-lookup"><span data-stu-id="c757e-171">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="c757e-172">例: ユーザーが言及した送信メッセージ</span><span class="sxs-lookup"><span data-stu-id="c757e-172">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="c757e-173">groupChat またはチャネル スコープへのアクセス</span><span class="sxs-lookup"><span data-stu-id="c757e-173">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="c757e-174">ボットは、グループやチームでメッセージを送受信する以上の操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="c757e-174">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="c757e-175">たとえば、メンバーのリスト (プロファイル情報を含む) とチャネルのリストをフェッチすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c757e-175">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="c757e-176">詳細[については、「Get context for your Microsoft Teamsボット」](~/resources/bot-v3/bots-context.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c757e-176">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="c757e-177">*「Bot* [Framework のサンプル」も参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="c757e-177">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
