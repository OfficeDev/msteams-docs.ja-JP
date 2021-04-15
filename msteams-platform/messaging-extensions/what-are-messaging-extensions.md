---
title: メッセージング拡張機能
author: clearab
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2d82202c72584927fc705813151d91510a7f12c9
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696752"
---
# <a name="messaging-extensions"></a><span data-ttu-id="c09ab-103">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c09ab-103">Messaging extensions</span></span>

<span data-ttu-id="c09ab-104">メッセージング拡張機能を使用すると、ユーザーは Microsoft Teams クライアントのボタンとフォームを介して Web サービスを操作できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-104">Messaging extensions allow the users to interact with your web service through buttons and forms in the Microsoft Teams client.</span></span> <span data-ttu-id="c09ab-105">ユーザーは、作成メッセージ領域、コマンド ボックス、またはメッセージから直接、外部システムでアクションを検索または開始できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-105">They can search or initiate actions in an external system from the compose message area, the command box, or directly from a message.</span></span> <span data-ttu-id="c09ab-106">その操作の結果を、リッチ形式のカードの形式で Microsoft Teams クライアントに返送できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-106">You can send back the results of that interaction to the Microsoft Teams client in the form of a richly formatted card.</span></span> <span data-ttu-id="c09ab-107">このドキュメントでは、メッセージング拡張機能の概要、さまざまなシナリオで実行されるタスク、メッセージング拡張機能の作業、アクションと検索コマンド、リンク解除について説明します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-107">This document gives an overview of the messaging extension, tasks performed under different scenarios, working of messaging extension, action and search commands, and link unfurling.</span></span>

<span data-ttu-id="c09ab-108">次の図は、メッセージング拡張機能が呼び出される場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-108">The following image displays the locations from where messaging extensions are invoked:</span></span>

![メッセージング拡張機能の呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="scenarios-where-messaging-extensions-are-used"></a><span data-ttu-id="c09ab-110">メッセージング拡張機能が使用されるシナリオ</span><span class="sxs-lookup"><span data-stu-id="c09ab-110">Scenarios where messaging extensions are used</span></span>

| <span data-ttu-id="c09ab-111">シナリオ</span><span class="sxs-lookup"><span data-stu-id="c09ab-111">Scenario</span></span> | <span data-ttu-id="c09ab-112">例</span><span class="sxs-lookup"><span data-stu-id="c09ab-112">Example</span></span> |
|:-----------------|:-----------------|
|<span data-ttu-id="c09ab-113">一部の外部システムでアクションを実行し、アクションの結果を会話に戻す必要があります。</span><span class="sxs-lookup"><span data-stu-id="c09ab-113">You want some external system to do an action  and the result of the action to be sent back to your conversation.</span></span>|<span data-ttu-id="c09ab-114">リソースを予約し、チャネルが予約されたタイム スロットを知るのを許可します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-114">Reserve a resource and allow the channel to know the reserved time slot.</span></span>|
|<span data-ttu-id="c09ab-115">外部システムで何かを見つけて、その結果を会話と共有します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-115">You want to find something in an external system, and share the results with the conversation.</span></span>|<span data-ttu-id="c09ab-116">Azure DevOps で作業項目を検索し、アダプティブ カードとしてグループと共有します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-116">Search for a work item in Azure DevOps, and share it with the group as an Adaptive Card.</span></span>|
|<span data-ttu-id="c09ab-117">外部システムで複数の手順または多数の情報を含む複雑なタスクを完了し、その結果を会話と共有します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-117">You want to complete a complex task involving multiple steps or lots of information in an external system, and share the results with a conversation.</span></span>|<span data-ttu-id="c09ab-118">Teams メッセージに基づいて追跡システムにバグを作成し、そのバグを Bob に割り当て、そのバグの詳細を示すカードをスレッドに送信します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-118">Create a bug in your tracking system based on a Teams message, assign that bug to Bob, and send a card to the conversation thread with the bug's details.</span></span>|

## <a name="understand-how-messaging-extensions-work"></a><span data-ttu-id="c09ab-119">メッセージング拡張機能の動作を理解する</span><span class="sxs-lookup"><span data-stu-id="c09ab-119">Understand how messaging extensions work</span></span>

<span data-ttu-id="c09ab-120">メッセージング拡張機能は、ホストする Web サービスと、Microsoft Teams クライアントでの Web サービスの呼び出し先を定義するアプリ マニフェストで構成されます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-120">A messaging extension consists of a web service that you host and an app manifest, which defines where your web service is invoked from in the Microsoft Teams client.</span></span> <span data-ttu-id="c09ab-121">Web サービスは、ボット フレームワークのメッセージング スキーマとセキュリティで保護された通信プロトコルを利用します。そのため、Web サービスをボット フレームワークにボットとして登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c09ab-121">The web service takes advantage of the Bot Framework's messaging schema and secure communication protocol, so you must register your web service as a bot in the Bot Framework.</span></span> 

> [!NOTE]
> <span data-ttu-id="c09ab-122">Web サービスを手動で作成することもできますが、 [ボット フレームワーク SDK を使用](https://github.com/microsoft/botframework) してプロトコルを操作します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-122">Though you can create the web service manually, use [Bot Framework SDK](https://github.com/microsoft/botframework) to work with the protocol.</span></span>

<span data-ttu-id="c09ab-123">Microsoft Teams アプリのアプリ マニフェストでは、最大 10 個の異なるコマンドで 1 つのメッセージング拡張機能が定義されます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-123">In the app manifest for Microsoft Teams app, a single messaging extension is defined with up to ten different commands.</span></span> <span data-ttu-id="c09ab-124">各コマンドは、アクションや検索などの種類と、呼び出されたクライアント内の場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-124">Each command defines a type, such as action or search and the locations in the client from where it is invoked.</span></span> <span data-ttu-id="c09ab-125">呼び出し場所は、メッセージ領域、コマンド バー、およびメッセージを作成します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-125">The invoke locations are compose message area, command bar, and message.</span></span> <span data-ttu-id="c09ab-126">呼び出し時に、Web サービスは、関連するすべての情報を含む JSON ペイロードを含む HTTPS メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-126">On invoke, the web service receives an HTTPS message with a JSON payload including all the relevant information.</span></span> <span data-ttu-id="c09ab-127">JSON ペイロードで応答し、Teams クライアントが次の対話を有効にすることを知る。</span><span class="sxs-lookup"><span data-stu-id="c09ab-127">Respond with a JSON payload, allowing the Teams client to know the next interaction to enable.</span></span> 

## <a name="types-of-messaging-extension-commands"></a><span data-ttu-id="c09ab-128">メッセージング拡張機能のコマンドの種類</span><span class="sxs-lookup"><span data-stu-id="c09ab-128">Types of messaging extension commands</span></span>

<span data-ttu-id="c09ab-129">メッセージング拡張機能コマンドには、アクション コマンドと検索コマンドの 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="c09ab-129">There are two types of messaging extension commands, action command and search command.</span></span> <span data-ttu-id="c09ab-130">メッセージング拡張機能コマンドの種類は、Web サービスで使用できる UI 要素と対話フローを定義します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-130">The messaging extension command type defines the UI elements and interaction flows available to your web service.</span></span> <span data-ttu-id="c09ab-131">認証や構成などの一部の操作は、両方の種類のコマンドで使用できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-131">Some interactions, such as authentication and configuration are available for both types of commands.</span></span>

### <a name="action-commands"></a><span data-ttu-id="c09ab-132">操作コマンド</span><span class="sxs-lookup"><span data-stu-id="c09ab-132">Action commands</span></span>

<span data-ttu-id="c09ab-133">アクション コマンドは、ユーザーにモーダル ポップアップを表示して情報を収集または表示するために使用します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-133">Action commands are used to present the users with a modal popup to collect or display information.</span></span> <span data-ttu-id="c09ab-134">ユーザーがフォームを送信すると、Web サービスはメッセージを会話に直接挿入するか、メッセージを作成メッセージ領域に挿入して応答します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-134">When the user submits the form, your web service responds by inserting a message into the conversation directly or by inserting a message into the compose message area.</span></span> <span data-ttu-id="c09ab-135">その後、ユーザーはメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-135">After that the user can submit the message.</span></span> <span data-ttu-id="c09ab-136">複数のフォームを連鎖して、より複雑なワークフローを作成できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-136">You can chain multiple forms together for more complex workflows.</span></span>

<span data-ttu-id="c09ab-137">アクション コマンドは、作成メッセージ領域、コマンド ボックス、またはメッセージからトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-137">The action commands are triggered from the compose message area, the command box, or from a message.</span></span> <span data-ttu-id="c09ab-138">コマンドがメッセージから呼び出されると、ボットに送信される最初の JSON ペイロードには、呼び出されたメッセージ全体が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-138">When the command is invoked from a message, the initial JSON payload sent to your bot includes the entire message it was invoked from.</span></span> <span data-ttu-id="c09ab-139">次の図は、メッセージング拡張機能アクション コマンド タスク モジュールを表示します。 ![ メッセージング拡張機能アクション コマンド タスク モジュール](~/assets/images/task-module.png)</span><span class="sxs-lookup"><span data-stu-id="c09ab-139">The following image displays the messaging extension action command task module: ![messaging extension action command task module](~/assets/images/task-module.png)</span></span>

### <a name="search-commands"></a><span data-ttu-id="c09ab-140">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="c09ab-140">Search commands</span></span>

<span data-ttu-id="c09ab-141">検索コマンドを使用すると、ユーザーは、検索ボックスを介して手動で、または監視対象ドメインへのリンクを作成メッセージ領域に貼り付け、検索の結果をメッセージに挿入することで、外部システムを検索できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-141">Search commands allow the users to search an external system for information either manually through a search box, or by pasting a link to a monitored domain into the compose message area, and insert the results of the search into a message.</span></span> <span data-ttu-id="c09ab-142">最も基本的な検索コマンド フローでは、最初の呼び出しメッセージには、ユーザーが送信した検索文字列が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-142">In the most basic search command flow, the initial invoke message includes the search string that the user submitted.</span></span> <span data-ttu-id="c09ab-143">カードとカードのプレビューの一覧で応答します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-143">You respond with a list of cards and card previews.</span></span> <span data-ttu-id="c09ab-144">Teams クライアントは、ユーザーのカード プレビューの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-144">The Teams client renders a list of card previews for the user.</span></span> <span data-ttu-id="c09ab-145">ユーザーがリストからカードを選択すると、フルサイズのカードが作成メッセージ領域に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-145">When the user selects a card from the list, the full-size card is inserted into the compose message area.</span></span>

<span data-ttu-id="c09ab-146">カードは、メッセージの作成領域またはコマンド ボックスからトリガーされ、メッセージからトリガーされません。</span><span class="sxs-lookup"><span data-stu-id="c09ab-146">The cards are triggered from the compose message area or the command box and not triggered from a message.</span></span> <span data-ttu-id="c09ab-147">メッセージからトリガーできない。</span><span class="sxs-lookup"><span data-stu-id="c09ab-147">They can not be triggered from a message.</span></span>
<span data-ttu-id="c09ab-148">次の図は、メッセージング拡張機能の検索コマンド タスク モジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-148">The following image displays the messaging extension search command task module:</span></span>

![メッセージング拡張機能の検索コマンド](~/assets/images/search-extension.png)

> [!NOTE]
> <span data-ttu-id="c09ab-150">カードの詳細については、「カードは [何か」を参照してください](../task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="c09ab-150">For more information on cards, see [what are cards](../task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="link-unfurling"></a><span data-ttu-id="c09ab-151">リンク展開</span><span class="sxs-lookup"><span data-stu-id="c09ab-151">Link unfurling</span></span>

<span data-ttu-id="c09ab-152">Web サービスは、作成メッセージ領域に URL を貼り付けするときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-152">A web service is invoked when a URL is pasted in the compose message area.</span></span> <span data-ttu-id="c09ab-153">この機能は、リンク解除と呼ばれる機能です。</span><span class="sxs-lookup"><span data-stu-id="c09ab-153">This functionality is known as link unfurling.</span></span> <span data-ttu-id="c09ab-154">特定のドメインを含む URL を作成メッセージ領域に貼り付けるときに、呼び出しを受信するためにサブスクライブできます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-154">You can subscribe to receive an invoke when URLs containing a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="c09ab-155">お客様の Web サービスは、URL を詳細情報が記載されたカードに "展開" することができ、そのカードでは標準的な Web サイトのプレビュー カードよりも多くの情報を提供できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-155">Your web service can "unfurl" the URL into a detailed card, providing more information than the standard website preview card.</span></span> <span data-ttu-id="c09ab-156">ボタンを追加すると、Microsoft Teams クライアントを離れることなく、ユーザーが直ちにアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="c09ab-156">You can add buttons to allow the users to immediately take action without leaving the Microsoft Teams client.</span></span>
<span data-ttu-id="c09ab-157">次の画像は、メッセージング拡張機能にリンクを貼り付けするときにリンクの分岐解除機能を表示します。</span><span class="sxs-lookup"><span data-stu-id="c09ab-157">The following images display link unfurling feature when a link is pasted in messaging extension:</span></span>
 
![unfurl リンク](../assets/images/messaging-extension/unfurl-link.png)

![リンクのリンク解除](../assets/images/messaging-extension/link-unfurl.gif)


## <a name="see-also"></a><span data-ttu-id="c09ab-160">関連項目</span><span class="sxs-lookup"><span data-stu-id="c09ab-160">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c09ab-161">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="c09ab-161">Create a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)

## <a name="next-step"></a><span data-ttu-id="c09ab-162">次の手順</span><span class="sxs-lookup"><span data-stu-id="c09ab-162">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c09ab-163">アクション メッセージング拡張機能のコマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="c09ab-163">Define action messaging extension command</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c09ab-164">検索メッセージング拡張機能のコマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="c09ab-164">Define search messaging extension command</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
