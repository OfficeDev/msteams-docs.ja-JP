---
title: ボットとのチャンネルチャットとグループチャットの会話
description: チャネル内のボットと会話するエンド ツー エンドのシナリオを説明Microsoft Teams
keywords: チーム シナリオ チャネル会話ボット
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566797"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="a7ddb-104">Microsoft Teams ボットとのチャネルおよびグループ チャット会話</span><span class="sxs-lookup"><span data-stu-id="a7ddb-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="a7ddb-105">Microsoft Teamsを使用すると、ユーザーは自分のチャンネルやグループチャットの会話にボットを持ち込むことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="a7ddb-106">チームまたはチャットにボットを追加することで、会話のすべてのユーザーが、会話のボット機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="a7ddb-107">チーム情報の照会やユーザーの@mentioningなど、ボット内のTeams固有の機能にアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="a7ddb-108">チャンネルチャットやグループチャットは、ユーザーがボットを@mentionする必要があるという点で、個人チャットとは異なります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="a7ddb-109">ボットが個人、グループチャット、チャネルなどの複数のスコープで使用されている場合は、ボット メッセージがどのスコープから来たかを検出し、それに応じて処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-109">If a bot is used in multiple scopes such as personal, groupchat, or channel, you need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="a7ddb-110">チャネルまたはグループ用の優れたボットの設計</span><span class="sxs-lookup"><span data-stu-id="a7ddb-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="a7ddb-111">チームに追加されたボットは別のチーム メンバーになり、会話の一部として@mentionedできます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="a7ddb-112">実際、ボットは@mentionedされたときにのみメッセージを受信するため、チャネル上の他の会話はボットに送信されません。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="a7ddb-113">グループまたはチャネル内のボットは、すべてのメンバーに関連し、適切な情報を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="a7ddb-114">ボットは、エクスペリエンスに関連する情報を提供できますが、そのボットとの会話は誰でも見ることができます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="a7ddb-115">したがって、グループやチャネルの優れたボットは、すべてのユーザーに価値を追加し、1 対 1 の会話に適した情報を誤って共有する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="a7ddb-116">ボットは、このままでも、追加の作業を必要とせずに、すべてのスコープで完全に関連している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="a7ddb-117">Microsoft Teamsでは、すべてのスコープでボットが機能するとは考えられませんが、サポートするスコープでボットがユーザー値を提供することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="a7ddb-118">スコープの詳細については[、「Microsoft Teamsのアプリ](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="a7ddb-119">グループやチャンネルで機能するボットを開発するには、個人的な会話と同じ機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="a7ddb-120">ペイロード内の追加のイベントとデータは、グループ情報とチャネル情報Teams提供します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="a7ddb-121">これらの相違点と共通機能の主な相違点については、以下のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="a7ddb-122">メッセージの作成</span><span class="sxs-lookup"><span data-stu-id="a7ddb-122">Creating messages</span></span>

<span data-ttu-id="a7ddb-123">チャネルでメッセージを作成するボットの詳細については、「 [ボットのプロアクティブなメッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」、特に [チャネル会話の作成 を](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="a7ddb-124">メッセージの受信</span><span class="sxs-lookup"><span data-stu-id="a7ddb-124">Receiving messages</span></span>

<span data-ttu-id="a7ddb-125">グループまたはチャネルのボットの場合、 [通常のメッセージ スキーマ](https://docs.botframework.com/core-concepts/reference/#activity)に加えて、ボットは次のプロパティも受け取ります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="a7ddb-126">`channelData`[チャネル データTeams](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="a7ddb-127">グループ チャットには、そのチャットに固有の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="a7ddb-128">`conversation.id` チャネル ID と応答チェーン内の最初のメッセージの ID から成る応答チェーン ID。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain.</span></span>
* <span data-ttu-id="a7ddb-129">`conversation.isGroup``true`チャネルまたはグループ チャットのボット メッセージ用です。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats.</span></span>
* <span data-ttu-id="a7ddb-130">`conversation.conversationType``groupChat`または のいずれか `channel` 。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-130">`conversation.conversationType` Either `groupChat` or `channel`.</span></span>
* <span data-ttu-id="a7ddb-131">`entities` 1 つまたは複数のメンションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-131">`entities` Can contain one or more mentions.</span></span> <span data-ttu-id="a7ddb-132">詳細については、「 [メンション](#-mentions)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-132">For more information, see [Mentions](#-mentions).</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="a7ddb-133">メッセージへの返信</span><span class="sxs-lookup"><span data-stu-id="a7ddb-133">Replying to messages</span></span>

<span data-ttu-id="a7ddb-134">既存のメッセージに返信するには [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) 、.NET または [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.jsで呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="a7ddb-135">ボット ビルダー SDK では、すべての詳細を処理します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="a7ddb-136">REST API を使用する場合は、エンドポイントを呼び出すこともできます [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="a7ddb-137">チャネルでは、メッセージに返信すると、その応答チェーンへの応答として表示されます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="a7ddb-138">`conversation.id`には、チャネルと最上位レベルのメッセージ ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="a7ddb-139">Bot Framework は詳細を処理しますが、必要に応じてその `conversation.id` 会話スレッドに対する今後の返信にキャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="a7ddb-140">ベスト プラクティス: Teamsのウェルカム メッセージ</span><span class="sxs-lookup"><span data-stu-id="a7ddb-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="a7ddb-141">ボットを最初にグループまたはチームに追加した場合、一般的に、ボットを紹介するウェルカム メッセージをすべてのユーザーに送信すると便利です。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="a7ddb-142">ウェルカム メッセージには、ボットの機能とユーザーの利点の説明が記載されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="a7ddb-143">メッセージには、ユーザーがアプリを操作するためのコマンドも含めるのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="a7ddb-144">これを行うには、オブジェクト内の eventType を使用して `conversationUpdate` 、ボットがメッセージに応答することを確認 `teamsAddMembers` `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="a7ddb-145">`memberAdded`ユーザーがチームに追加されたときに同じイベントが送信されるため、ID がボットのアプリ ID であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="a7ddb-146">詳細については [、チーム メンバーまたはボットの追加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="a7ddb-147">ボットが追加されたときに、チームの各メンバーに個人用メッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="a7ddb-148">これを行うには、 [チームの名簿を取得](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) し、各ユーザーに [ダイレクトメッセージ](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)を送信します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="a7ddb-149">次の状況では、ボットからウェルカム メッセージを送信 *しないことを* お勧めします。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="a7ddb-150">チームは大きい(明らかに、100人以上のメンバー)。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-150">The team is big (obviously subjective, for example, more than 100 members).</span></span> <span data-ttu-id="a7ddb-151">ボットは「スパム」と見なされ、ボットを追加した人は、ウェルカムメッセージを見たすべての人にボットの価値提案を明確に伝えない限り、苦情を受け取る可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="a7ddb-152">ボットは、最初にグループまたはチャネルで言及され、最初にチームに追加されます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-152">Your bot is first mentioned in a group or channel, versus being first added to a team.</span></span>
* <span data-ttu-id="a7ddb-153">グループまたはチャネルの名前が変更されます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-153">A group or channel is renamed.</span></span>
* <span data-ttu-id="a7ddb-154">チーム メンバーがグループまたはチャネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-154">A team member is added to a group or channel.</span></span>

## <a name="-mentions"></a><span data-ttu-id="a7ddb-155">@言及</span><span class="sxs-lookup"><span data-stu-id="a7ddb-155">@ Mentions</span></span>

<span data-ttu-id="a7ddb-156">グループまたはチャネル内のボットはメッセージに記述されている場合にのみ応答するため _("@botname")、_ グループチャネル内のボットが受信するすべてのメッセージには独自の名前が含まれているため、メッセージの解析はそれを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="a7ddb-157">さらに、ボットは、メッセージの一部として、ユーザーに言及されている他のユーザーを解析し、言及することができます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="a7ddb-158">メンションの取得</span><span class="sxs-lookup"><span data-stu-id="a7ddb-158">Retrieving mentions</span></span>

<span data-ttu-id="a7ddb-159">メンションは `entities` ペイロードのオブジェクトに返され、ユーザーの一意の ID と、ほとんどの場合、言及されたユーザーの名前の両方が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="a7ddb-160">オブジェクトの配列を返す `GetMentions` Bot Builder SDK for .NET の関数を呼び出すことで、メッセージ内のすべてのメンションを取得できます `Mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="a7ddb-161">.NET のコード例: @bot参照を確認し、削除します。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-161">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="a7ddb-162">また、 `GetTextWithoutMentions` ボットを含むすべてのメンションを取り除くTeams拡張機能を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="a7ddb-163">Node.js例のコード: @bot参照を確認して削除する</span><span class="sxs-lookup"><span data-stu-id="a7ddb-163">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="a7ddb-164">また、 `getTextWithoutMentions` ボットを含むすべてのメンションを取り除くTeams拡張機能を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="a7ddb-165">メンションの構築</span><span class="sxs-lookup"><span data-stu-id="a7ddb-165">Constructing mentions</span></span>

<span data-ttu-id="a7ddb-166">ボットは、チャンネルに投稿されたメッセージで他のユーザーに言及できます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="a7ddb-167">これを行うには、メッセージで次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="a7ddb-168">`<at>@username</at>`メッセージ テキストに含めます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-168">Include `<at>@username</at>` in the message text.</span></span>
* <span data-ttu-id="a7ddb-169">エンティティ `mention` コレクション内にオブジェクトを含めます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-169">Include the `mention` object inside the entities collection.</span></span>

#### <a name="net-example"></a><span data-ttu-id="a7ddb-170">.NET の例</span><span class="sxs-lookup"><span data-stu-id="a7ddb-170">.NET example</span></span>

<span data-ttu-id="a7ddb-171">この例では[、NuGet パッケージを使用Teams。](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="a7ddb-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="a7ddb-172">Node.js例</span><span class="sxs-lookup"><span data-stu-id="a7ddb-172">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="a7ddb-173">例: ユーザーが言及した送信メッセージ</span><span class="sxs-lookup"><span data-stu-id="a7ddb-173">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="a7ddb-174">グループチャットまたはチャネルスコープへのアクセス</span><span class="sxs-lookup"><span data-stu-id="a7ddb-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="a7ddb-175">ボットは、グループやチームでメッセージを送受信する以外の操作も実行できます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="a7ddb-176">たとえば、プロファイル情報やチャネルのリストを含むメンバーのリストを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="a7ddb-177">詳細については、「 [Microsoft Teams ボットのコンテキストを取得する](~/resources/bot-v3/bots-context.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7ddb-177">For more information, see [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a7ddb-178">関連項目</span><span class="sxs-lookup"><span data-stu-id="a7ddb-178">See also</span></span>

[<span data-ttu-id="a7ddb-179">ボット フレームワークのサンプル</span><span class="sxs-lookup"><span data-stu-id="a7ddb-179">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
