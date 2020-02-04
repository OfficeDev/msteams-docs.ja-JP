---
title: メッセージング拡張機能とは
author: clearab
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 01a038d57368826345a55358b1d628447b21f772
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674933"
---
# <a name="what-are-messaging-extensions"></a><span data-ttu-id="543fd-103">メッセージング拡張機能とは</span><span class="sxs-lookup"><span data-stu-id="543fd-103">What are messaging extensions?</span></span>

<span data-ttu-id="543fd-104">メッセージング拡張機能により、ユーザーは Microsoft Teams クライアントのボタンとフォームを使用して web サービスを操作することができます。</span><span class="sxs-lookup"><span data-stu-id="543fd-104">Messaging extensions allow users to interact with your web service through buttons and forms in the Microsoft Teams client.</span></span> <span data-ttu-id="543fd-105">作成メッセージ領域、コマンドボックス、またはメッセージから直接、外部システムでアクションを検索したり、開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="543fd-105">They can search, or initiate actions, in an external system from the compose message area, the command box, or directly from a message.</span></span> <span data-ttu-id="543fd-106">その結果を Microsoft Teams クライアントに送り返すことができます (通常は、強力な形式のカードの形式)。</span><span class="sxs-lookup"><span data-stu-id="543fd-106">You can then send the results of that interaction back to the Microsoft Teams client, typically in the form of a richly formatted card.</span></span>

<span data-ttu-id="543fd-107">次のスクリーンショットは、メッセージング拡張機能を呼び出す場所を示しています。</span><span class="sxs-lookup"><span data-stu-id="543fd-107">The screenshot below shows the locations where messaging extensions can be invoked from.</span></span>

![メッセージング拡張機能の呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="what-kinds-of-tasks-are-they-good-for"></a><span data-ttu-id="543fd-109">どのような種類のタスクが適しているか。</span><span class="sxs-lookup"><span data-stu-id="543fd-109">What kinds of tasks are they good for?</span></span>

<span data-ttu-id="543fd-110">**シナリオ:** 何らかの操作を実行するために外部システムが必要で、アクションの結果が自分の会話に送り返されるようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="543fd-110">**Scenario:** I need some external system to do something and I want the result of the action to be sent back to my conversation.\</span></span>
<span data-ttu-id="543fd-111">**例:** リソースを予約し、チャネルに予約した曜日と時間を知らせます。</span><span class="sxs-lookup"><span data-stu-id="543fd-111">**Example:** Reserve a resource and let the channel know what day/time you reserved it for.</span></span>

<span data-ttu-id="543fd-112">**シナリオ:** 外部システムで何かを検索する必要があり、その結果を自分の会話と共有する。</span><span class="sxs-lookup"><span data-stu-id="543fd-112">**Scenario:** I need to find something in an external system, and I want to share the results with my conversation.\</span></span>
<span data-ttu-id="543fd-113">**例:** Azure DevOps で作業項目を検索し、それをアダプティブカードとしてグループと共有します。</span><span class="sxs-lookup"><span data-stu-id="543fd-113">**Example:**  Search for a work item in Azure DevOps, and share it with the group as an adaptive card.</span></span>

<span data-ttu-id="543fd-114">**シナリオ:** 外部システムに複数の手順 (または大量の情報) を含む複雑なタスクを完了し、結果を会話と共有する必要があります。</span><span class="sxs-lookup"><span data-stu-id="543fd-114">**Scenario:** I need to complete a complex task involving multiple steps (or lots of information) in an external system, and the results should be shared with a conversation.\</span></span>
<span data-ttu-id="543fd-115">**例:** Teams メッセージに基づいて追跡システムにバグを作成し、そのバグを Bob に割り当ててから、バグの詳細を含むカードを会話スレッドに送信します。</span><span class="sxs-lookup"><span data-stu-id="543fd-115">**Example:** Create a bug in your tracking system based on a Teams message, assign that bug to Bob, then send a card to the conversation thread with the bug's details.</span></span>

## <a name="how-do-messaging-extensions-work"></a><span data-ttu-id="543fd-116">メッセージング拡張機能のしくみ</span><span class="sxs-lookup"><span data-stu-id="543fd-116">How do messaging extensions work?</span></span>

<span data-ttu-id="543fd-117">メッセージング拡張機能は、ホストする web サービスとアプリのマニフェストで構成されています。これは、Microsoft Teams クライアントで web サービスを呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="543fd-117">A messaging extension consists of a web service you host and your app manifest which defines where your web service can be invoked from in the Microsoft Teams client.</span></span> <span data-ttu-id="543fd-118">Bot フレームワークのメッセージングスキーマとセキュリティで保護された通信プロトコルを利用することにより、web サービスを bot フレームワークの bot として登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="543fd-118">They take advantage of the Bot Framework's messaging schema and secure communication protocol, so you'll also need to register your web service as a bot in the Bot Framework.</span></span> <span data-ttu-id="543fd-119">Web サービスを完全に手動で作成することもできますが、このプロトコルをより簡単に動作させるために[Bot フレームワーク SDK](https://github.com/microsoft/botframework)を利用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="543fd-119">Although you can create your web service completely by hand, we recommend you take advantage of the [Bot Framework SDK](https://github.com/microsoft/botframework) to make working with the protocol simpler.</span></span>

<span data-ttu-id="543fd-120">Microsoft Teams アプリのアプリマニフェストには、最大10個の異なるコマンドを持つ1つのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="543fd-120">In the app manifest for your Microsoft Teams app you'll define a single messaging extension with up to ten different commands.</span></span> <span data-ttu-id="543fd-121">各コマンドは、種類 (操作または検索)、およびクライアント内の場所 (メッセージ領域の作成、コマンドバー、メッセージ) を定義します。</span><span class="sxs-lookup"><span data-stu-id="543fd-121">Each command defines a type (action or search), and the locations in the client it can be invoked from (compose message area, command bar, and/or message).</span></span> <span data-ttu-id="543fd-122">呼び出しが完了すると、web サービスは、関連するすべての情報を含む JSON ペイロードを含む HTTPS メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="543fd-122">Once invoked, your web service will receive an HTTPS message with a JSON payload including all the relevant information.</span></span> <span data-ttu-id="543fd-123">JSON ペイロードで応答し、Teams クライアントに、次に有効にする相互作用を知らせます。</span><span class="sxs-lookup"><span data-stu-id="543fd-123">You'll respond with a JSON payload, letting the Teams client know what interaction to enable next.</span></span>

## <a name="types-of-messaging-extension-commands"></a><span data-ttu-id="543fd-124">メッセージング拡張コマンドの種類</span><span class="sxs-lookup"><span data-stu-id="543fd-124">Types of messaging extension commands</span></span>

<span data-ttu-id="543fd-125">メッセージ拡張コマンドの種類によって、web サービスで使用できる UI 要素と相互作用フローが定義されます。</span><span class="sxs-lookup"><span data-stu-id="543fd-125">The type of messaging extension command defines the UI elements and interaction flows available to your web service.</span></span> <span data-ttu-id="543fd-126">認証や構成などの一部の操作は、両方の種類のコマンドで使用できます。</span><span class="sxs-lookup"><span data-stu-id="543fd-126">Some interactions, like authentication and configuration, are available for both types of commands.</span></span>

### <a name="action-commands"></a><span data-ttu-id="543fd-127">アクションコマンド</span><span class="sxs-lookup"><span data-stu-id="543fd-127">Action commands</span></span>

<span data-ttu-id="543fd-128">アクションコマンドを使用すると、ユーザーにモーダルポップアップを表示して、情報を収集または表示することができます。</span><span class="sxs-lookup"><span data-stu-id="543fd-128">Action commands allow you present your users with a modal popup to collect or display information.</span></span> <span data-ttu-id="543fd-129">ユーザーがフォームを送信すると、web サービスは会話に直接メッセージを挿入するか、またはメッセージを作成メッセージ領域に挿入してメッセージを送信できるようにすることによって応答できます。</span><span class="sxs-lookup"><span data-stu-id="543fd-129">When they submit the form, your web service can respond by inserting a message into the conversation directly, or by inserting a message into the compose message area and allowing the user to submit the message.</span></span> <span data-ttu-id="543fd-130">複数のフォームを結合して、より複雑なワークフローを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="543fd-130">You can even chain multiple forms together for more complex workflows.</span></span>

<span data-ttu-id="543fd-131">これらのメッセージは、[メッセージの作成] 領域、[コマンド] ボックス、またはメッセージから起動できます。</span><span class="sxs-lookup"><span data-stu-id="543fd-131">They can be triggered from the compose message area, the command box, or from a message.</span></span> <span data-ttu-id="543fd-132">メッセージから呼び出した場合、bot に送信される最初の JSON ペイロードには、から呼び出されたメッセージ全体が含まれます。</span><span class="sxs-lookup"><span data-stu-id="543fd-132">When invoked from a message, the initial JSON payload sent to your bot will include the entire message it was invoked from.</span></span>

![メッセージング拡張機能のコマンドタスクモジュール](~/assets/images/task-module.png)

### <a name="search-commands"></a><span data-ttu-id="543fd-134">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="543fd-134">Search commands</span></span>

<span data-ttu-id="543fd-135">検索コマンドを使用すると、ユーザーは外部システムで情報を検索できます (検索ボックスを手動で検索するか、または監視対象ドメインへのリンクを作成メッセージ領域に貼り付けることにより)、検索の結果をメッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="543fd-135">Search commands allow your users to search an external system for information (either manually through a search box, or by pasting a link to a monitored domain into the compose message area), then insert the results of the search into a message.</span></span> <span data-ttu-id="543fd-136">最も基本的な検索コマンドフローでは、最初の呼び出しメッセージに、ユーザーが送信した検索文字列が含まれます。</span><span class="sxs-lookup"><span data-stu-id="543fd-136">In the most basic search command flow, the initial invoke message will include the search string the user submitted.</span></span> <span data-ttu-id="543fd-137">カードとカードのプレビューの一覧を返信します。</span><span class="sxs-lookup"><span data-stu-id="543fd-137">You'll respond with a list of cards and card previews.</span></span> <span data-ttu-id="543fd-138">Teams クライアントは、エンドユーザーが選択するカードのプレビューを一覧で表示します。</span><span class="sxs-lookup"><span data-stu-id="543fd-138">The Teams client will render the card previews in a list for the end user to select from.</span></span> <span data-ttu-id="543fd-139">ユーザーがカードを選択すると、フルサイズのカードが [メッセージの作成] 領域に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="543fd-139">When the user selects a card, the full-size card will be inserted into the compose message area.</span></span>

<span data-ttu-id="543fd-140">これらは、[メッセージの作成] 領域またはコマンドボックスから起動できます。</span><span class="sxs-lookup"><span data-stu-id="543fd-140">They can be triggered from the compose message area or the command box.</span></span> <span data-ttu-id="543fd-141">アクションコマンドとは異なり、メッセージからトリガーすることはできません。</span><span class="sxs-lookup"><span data-stu-id="543fd-141">Unlike action commands, they cannot be triggered from a message.</span></span>

![メッセージング拡張機能検索コマンド](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a><span data-ttu-id="543fd-143">Link unfurling</span><span class="sxs-lookup"><span data-stu-id="543fd-143">Link unfurling</span></span>

<span data-ttu-id="543fd-144">また、[メッセージの作成] 領域に URL が貼り付けられたときに、サービスを呼び出すこともできます。</span><span class="sxs-lookup"><span data-stu-id="543fd-144">You also have to option to invoke your service when a URL is pasted in the compose message area.</span></span> <span data-ttu-id="543fd-145">この機能 ( **link unfurling**と呼ばれる) を使用すると、特定のドメインを含む url が [メッセージの作成] 領域に貼り付けられたときに呼び出しを受信するようにサブスクライブできます。</span><span class="sxs-lookup"><span data-stu-id="543fd-145">This functionality, known as **link unfurling**, allows you to subscribe to receive an invoke when URLs containing a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="543fd-146">Web サービスは、URL を詳細なカードに "アン url" して、標準の web サイトプレビューカードより多くの情報を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="543fd-146">Your web service can "unfurl" the URL into a detailed card, providing more information than the standard website preview card.</span></span> <span data-ttu-id="543fd-147">ボタンを追加して、ユーザーが Microsoft Teams クライアントを離れることなく、すぐにアクションを実行できるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="543fd-147">You can even add buttons to allow your users to immediately take action without leaving the Microsoft Teams client.</span></span>

## <a name="get-started"></a><span data-ttu-id="543fd-148">作業の開始</span><span class="sxs-lookup"><span data-stu-id="543fd-148">Get Started</span></span>

<span data-ttu-id="543fd-149">構築を開始する準備ができましたか?</span><span class="sxs-lookup"><span data-stu-id="543fd-149">Ready to get started building?</span></span> <span data-ttu-id="543fd-150">クイックスタートのいずれかをお試しください。</span><span class="sxs-lookup"><span data-stu-id="543fd-150">Try one of our quickstarts:</span></span>

* <span data-ttu-id="543fd-151">C のクイックスタート#</span><span class="sxs-lookup"><span data-stu-id="543fd-151">Quickstarts for C#</span></span>
  * [<span data-ttu-id="543fd-152">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="543fd-152">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="543fd-153">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="543fd-153">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="543fd-154">JavaScript のクイックスタート</span><span class="sxs-lookup"><span data-stu-id="543fd-154">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="543fd-155">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="543fd-155">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="543fd-156">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="543fd-156">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a><span data-ttu-id="543fd-157">詳細情報</span><span class="sxs-lookup"><span data-stu-id="543fd-157">Learn more</span></span>

<span data-ttu-id="543fd-158">メッセージング拡張機能を構築します。</span><span class="sxs-lookup"><span data-stu-id="543fd-158">Build a messaging extension:</span></span>

* [<span data-ttu-id="543fd-159">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="543fd-159">Create a messaging extension</span></span>](~/messaging-extensions/how-to/create-messaging-extension.md)
* [<span data-ttu-id="543fd-160">アクションメッセージング拡張コマンドの定義</span><span class="sxs-lookup"><span data-stu-id="543fd-160">Define action messaging extension command</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="543fd-161">検索メッセージ拡張コマンドの定義</span><span class="sxs-lookup"><span data-stu-id="543fd-161">Define search messaging extension command</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
