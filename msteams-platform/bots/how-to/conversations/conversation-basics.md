---
title: 会話の基本
description: 会話の概要
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: c06f8765ae17f28f3abb1dff67d77aad4e76958c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020036"
---
# <a name="conversation-basics"></a><span data-ttu-id="59b48-103">会話の基本</span><span class="sxs-lookup"><span data-stu-id="59b48-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="59b48-104">会話とは、Microsoft Teams ボットと 1 人または複数のユーザーの間で送信される一連のメッセージです。</span><span class="sxs-lookup"><span data-stu-id="59b48-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="59b48-105">次の表に、Teams のスコープとも呼ばれる 3 種類の会話を示します。</span><span class="sxs-lookup"><span data-stu-id="59b48-105">The following table provides the three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="59b48-106">会話の種類</span><span class="sxs-lookup"><span data-stu-id="59b48-106">Conversation type</span></span> | <span data-ttu-id="59b48-107">説明</span><span class="sxs-lookup"><span data-stu-id="59b48-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="59b48-108">この会話の種類は、チャネルのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="59b48-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="59b48-109">この会話の種類には、ボットと 1 人のユーザーとの会話が含まれます。</span><span class="sxs-lookup"><span data-stu-id="59b48-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="59b48-110">この会話の種類には、ボットと 2 人以上のユーザーの間のチャットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="59b48-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="59b48-111">また、会議チャットでボットを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="59b48-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="59b48-112">ボットの動作は、関連する会話に応じて異なります。</span><span class="sxs-lookup"><span data-stu-id="59b48-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="59b48-113">チャネルチャットとグループ チャット会話のボットでは、チャネルでボットを呼び出す場合は、ユーザーがボットに @メンションする必要があります。</span><span class="sxs-lookup"><span data-stu-id="59b48-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="59b48-114">1 対 1 の会話のボットでは@メンションは必要ない。</span><span class="sxs-lookup"><span data-stu-id="59b48-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="59b48-115">ユーザーが送信したメッセージはすべてボットにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="59b48-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="59b48-116">ボットが特定の会話またはスコープで動作するには、アプリ マニフェストのそのスコープにサポートを [追加します](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="59b48-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

<span data-ttu-id="59b48-117">ボット会話の各メッセージは、 `Activity` 型のオブジェクトです `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="59b48-117">Each message in a bot conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="59b48-118">ユーザーがメッセージを送信すると、Teams はメッセージをボットに投稿し、ボットはメッセージを処理します。</span><span class="sxs-lookup"><span data-stu-id="59b48-118">When a user sends a message, Teams posts the message to your bot and the bot handles the message.</span></span> <span data-ttu-id="59b48-119">さらに、ボットが応答するコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。</span><span class="sxs-lookup"><span data-stu-id="59b48-119">In addition, to define core commands that your bot responds to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="59b48-120">グループまたはチャネル内のボットは、グループまたはチャネルに関する情報が記載されている場合にのみ@botname。</span><span class="sxs-lookup"><span data-stu-id="59b48-120">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="59b48-121">Teams は、ボットがアクティブなスコープで発生する会話イベントの通知をボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="59b48-121">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="59b48-122">これらのイベントをコードでキャプチャし、アクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="59b48-122">You can capture these events in your code and take action on them.</span></span> 

<span data-ttu-id="59b48-123">ボットは、ユーザーにプロアクティブ メッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="59b48-123">A bot can also send proactive messages to users.</span></span> <span data-ttu-id="59b48-124">プロアクティブ メッセージとは、ユーザーからの要求に応答しないボットから送信されるメッセージです。</span><span class="sxs-lookup"><span data-stu-id="59b48-124">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="59b48-125">ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含むリッチ カードをボット メッセージに書式設定できます。</span><span class="sxs-lookup"><span data-stu-id="59b48-125">You can format your bot messages to include rich cards that include interactive elements, such as buttons, text, images, audio, video, and so on.</span></span> <span data-ttu-id="59b48-126">ボットは、メッセージをデータの静的スナップショットとしてではなく、送信後に動的に更新できます。</span><span class="sxs-lookup"><span data-stu-id="59b48-126">Bot can dynamically update messages after sending them, instead of having your messages as static snapshots of data.</span></span> <span data-ttu-id="59b48-127">ボット フレームワークのメソッドを使用してメッセージを削除 `DeleteActivity` することもできます。</span><span class="sxs-lookup"><span data-stu-id="59b48-127">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="next-step"></a><span data-ttu-id="59b48-128">次の手順</span><span class="sxs-lookup"><span data-stu-id="59b48-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59b48-129">ボットの会話内のメッセージ</span><span class="sxs-lookup"><span data-stu-id="59b48-129">Messages in bot conversations</span></span>](~/bots/how-to/conversations/conversation-messages.md)
