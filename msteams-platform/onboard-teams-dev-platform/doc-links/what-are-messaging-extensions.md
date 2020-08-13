---
title: メッセージング拡張機能について
author: clearab
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3e80c965fb8cb2c4da2af6f6bf0709e7c8bd1d88
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652061"
---
# <a name="what-are-messaging-extensions"></a><span data-ttu-id="c58b2-103">メッセージング拡張機能について</span><span class="sxs-lookup"><span data-stu-id="c58b2-103">What are messaging extensions?</span></span>

<span data-ttu-id="c58b2-104">メッセージング拡張機能では、ユーザーは、Microsoft Teams クライアントのボタンとフォームを使用して Web サービスを操作することができます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-104">Messaging extensions allow users to interact with your web service through buttons and forms in the Microsoft Teams client.</span></span> <span data-ttu-id="c58b2-105">作成メッセージ領域、コマンドボックス、またはメッセージから直接、外部システムのアクションを検索または開始することができます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-105">They can search or initiate actions in an external system from the compose message area, the command box, or directly from a message.</span></span> <span data-ttu-id="c58b2-106">その操作の結果を、通常は書式設定されたカードとして Microsoft Teams クライアントに送信できます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-106">You can then send the results of that interaction back to the Microsoft Teams client, typically in the form of a richly formatted card.</span></span>

<span data-ttu-id="c58b2-107">次のスクリーンショットは、メッセージング拡張機能を呼び出す場所を示しています。</span><span class="sxs-lookup"><span data-stu-id="c58b2-107">The screenshot below shows the locations where messaging extensions can be invoked from.</span></span>

![メッセージング拡張機能の呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="user-scenarios"></a><span data-ttu-id="c58b2-109">ユーザーのシナリオ</span><span class="sxs-lookup"><span data-stu-id="c58b2-109">User scenarios</span></span>

<span data-ttu-id="c58b2-110">**シナリオ:** 何らかの操作を実行するために外部システムが必要で、アクションの結果が自分の会話に送り返されるようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="c58b2-110">**Scenario:** I need some external system to do something and I want the result of the action to be sent back to my conversation.\</span></span>
<span data-ttu-id="c58b2-111">**例:** リソースを予約し、チャネルに予約した曜日と時間を知らせます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-111">**Example:** Reserve a resource and let the channel know what day/time you reserved it for.</span></span>

<span data-ttu-id="c58b2-112">**シナリオ:** 外部システムで何かを検索する必要があり、その結果を自分の会話と共有する。</span><span class="sxs-lookup"><span data-stu-id="c58b2-112">**Scenario:** I need to find something in an external system, and I want to share the results with my conversation.\</span></span>
<span data-ttu-id="c58b2-113">**例:** Azure DevOps で作業項目を検索し、それをアダプティブカードとしてグループと共有します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-113">**Example:**  Search for a work item in Azure DevOps, and share it with the group as an adaptive card.</span></span>

<span data-ttu-id="c58b2-114">**シナリオ:** 外部システムに複数の手順 (または大量の情報) を含む複雑なタスクを完了し、結果を会話と共有する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c58b2-114">**Scenario:** I need to complete a complex task involving multiple steps (or lots of information) in an external system, and the results should be shared with a conversation.\</span></span>
<span data-ttu-id="c58b2-115">**例:** Teams メッセージに基づいて追跡システムにバグを作成し、そのバグを Bob に割り当ててから、バグの詳細を含むカードを会話スレッドに送信します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-115">**Example:** Create a bug in your tracking system based on a Teams message, assign that bug to Bob, then send a card to the conversation thread with the bug's details.</span></span>

## <a name="how-do-messaging-extensions-work"></a><span data-ttu-id="c58b2-116">メッセージング拡張機能のしくみ</span><span class="sxs-lookup"><span data-stu-id="c58b2-116">How do messaging extensions work?</span></span>

<span data-ttu-id="c58b2-117">メッセージング拡張機能は、ホストする web サービスとアプリのマニフェストで構成されています。これは、Microsoft Teams クライアントで web サービスを呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-117">A messaging extension consists of a web service you host and your app manifest which defines where your web service can be invoked from in the Microsoft Teams client.</span></span> <span data-ttu-id="c58b2-118">これらは Bot Framework のメッセージング スキーマとセキュリティで保護された通信プロトコルを利用するので、Web サービスを Bot Framework でボットとして登録する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="c58b2-118">They take advantage of the Bot Framework's messaging schema and secure communication protocol, so you'll also need to register your web service as a bot in the Bot Framework.</span></span> <span data-ttu-id="c58b2-119">Web サービスを完全に手動で作成することもできますが、このプロトコルをより簡単に動作させるために[Bot フレームワーク SDK](https://github.com/microsoft/botframework)を利用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c58b2-119">Although you can create your web service completely by hand, we recommend you take advantage of the [Bot Framework SDK](https://github.com/microsoft/botframework) to make working with the protocol simpler.</span></span>

<span data-ttu-id="c58b2-120">Microsoft Teams アプリのアプリマニフェストには、最大10個の異なるコマンドを持つ1つのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-120">In the app manifest for your Microsoft Teams app you'll define a single messaging extension with up to ten different commands.</span></span> <span data-ttu-id="c58b2-121">各コマンドは、種類 (操作または検索)、およびクライアント内の場所 (メッセージ領域の作成、コマンドバー、メッセージ) を定義します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-121">Each command defines a type (action or search), and the locations in the client it can be invoked from (compose message area, command bar, and/or message).</span></span> <span data-ttu-id="c58b2-122">呼び出しが完了すると、web サービスは、関連するすべての情報を含む JSON ペイロードを含む HTTPS メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-122">Once invoked, your web service will receive an HTTPS message with a JSON payload including all the relevant information.</span></span> <span data-ttu-id="c58b2-123">JSON ペイロードで応答し、Teams クライアントに、次に有効にする相互作用を知らせます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-123">You'll respond with a JSON payload, letting the Teams client know what interaction to enable next.</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="c58b2-124">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="c58b2-124">Types of messaging extensions</span></span>

<span data-ttu-id="c58b2-125">メッセージ拡張コマンドの種類によって、web サービスで使用できる UI 要素と相互作用フローが定義されます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-125">The type of messaging extension command defines the UI elements and interaction flows available to your web service.</span></span> <span data-ttu-id="c58b2-126">認証や構成などの一部の操作は、両方の種類のコマンドで使用できます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-126">Some interactions, like authentication and configuration, are available for both types of commands.</span></span>

### <a name="action-commands"></a><span data-ttu-id="c58b2-127">操作コマンド</span><span class="sxs-lookup"><span data-stu-id="c58b2-127">Action commands</span></span>

<span data-ttu-id="c58b2-128">アクションコマンドを使用すると、ユーザーにモーダルポップアップを表示して、情報を収集または表示することができます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-128">Action commands allow you to present your users with a modal popup to collect or display information.</span></span> <span data-ttu-id="c58b2-129">ユーザーがフォームを送信すると、web サービスは会話に直接メッセージを挿入するか、またはメッセージを作成メッセージ領域に挿入してメッセージを送信できるようにすることによって応答できます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-129">When they submit the form, your web service can respond by inserting a message into the conversation directly, or by inserting a message into the compose message area and allowing the user to submit the message.</span></span> <span data-ttu-id="c58b2-130">複数のフォームを結合して、より複雑なワークフローを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-130">You can even chain multiple forms together for more complex workflows.</span></span>

<span data-ttu-id="c58b2-131">これらのメッセージは、[メッセージの作成] 領域、[コマンド] ボックス、またはメッセージから起動できます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-131">They can be triggered from the compose message area, the command box, or from a message.</span></span> <span data-ttu-id="c58b2-132">メッセージから呼び出した場合、bot に送信される最初の JSON ペイロードには、から呼び出されたメッセージ全体が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-132">When invoked from a message, the initial JSON payload sent to your bot will include the entire message it was invoked from.</span></span>

![メッセージング拡張機能のコマンドタスクモジュール](~/assets/images/task-module.png)

### <a name="search-commands"></a><span data-ttu-id="c58b2-134">検索コマンド</span><span class="sxs-lookup"><span data-stu-id="c58b2-134">Search commands</span></span>

<span data-ttu-id="c58b2-135">検索コマンドを使用すると、ユーザーは (検索ボックスを使用して手動で、または監視対象ドメインへのリンクを [メッセージの作成] 領域に貼り付けて) 外部システムの情報を検索し、検索結果をメッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-135">Search commands allow your users to search an external system for information (either manually through a search box, or by pasting a link to a monitored domain into the compose message area), then insert the results of the search into a message.</span></span> <span data-ttu-id="c58b2-136">最も基本的な検索コマンドのフローでは、ユーザーが送信した検索文字列が最初の呼び出しメッセージに含まれています。</span><span class="sxs-lookup"><span data-stu-id="c58b2-136">In the most basic search command flow, the initial invoke message will include the search string the user submitted.</span></span> <span data-ttu-id="c58b2-137">これに対して、カードの一覧とカードのプレビューで応答します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-137">You'll respond with a list of cards and card previews.</span></span> <span data-ttu-id="c58b2-138">Teams クライアントは、エンドユーザーが選択するカードのプレビューを一覧で表示します。</span><span class="sxs-lookup"><span data-stu-id="c58b2-138">The Teams client will render the card previews in a list for the end user to select from.</span></span> <span data-ttu-id="c58b2-139">ユーザーがカードを選択すると、フルサイズのカードが [メッセージの作成] 領域に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-139">When the user selects a card, the full-size card will be inserted into the compose message area.</span></span>

<span data-ttu-id="c58b2-140">これらは、[メッセージの作成] 領域またはコマンドボックスから起動できます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-140">They can be triggered from the compose message area or the command box.</span></span> <span data-ttu-id="c58b2-141">アクションコマンドとは異なり、メッセージからトリガーすることはできません。</span><span class="sxs-lookup"><span data-stu-id="c58b2-141">Unlike action commands, they cannot be triggered from a message.</span></span>

![メッセージング拡張機能検索コマンド](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a><span data-ttu-id="c58b2-143">リンク展開</span><span class="sxs-lookup"><span data-stu-id="c58b2-143">Link unfurling</span></span>

<span data-ttu-id="c58b2-144">また、[メッセージの作成] 領域に URL が貼り付けられたときにもサービスを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-144">You also can invoke your service when a URL is pasted in the compose message area.</span></span> <span data-ttu-id="c58b2-145">この機能 ( **link unfurling**と呼ばれる) を使用すると、特定のドメインを含む url が [メッセージの作成] 領域に貼り付けられたときに呼び出しを受信するようにサブスクライブできます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-145">This functionality, known as **link unfurling**, allows you to subscribe to receive an invoke when URLs containing a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="c58b2-146">Web サービスは、URL を詳細なカードに "アン url" して、標準の web サイトプレビューカードより多くの情報を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-146">Your web service can "unfurl" the URL into a detailed card, providing more information than the standard website preview card.</span></span> <span data-ttu-id="c58b2-147">また、ユーザーが Teams を離れずにアクションを実行できるように、ボタンを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="c58b2-147">You can even add buttons so users can take action without leaving Teams.</span></span>

## <a name="get-started"></a><span data-ttu-id="c58b2-148">作業の開始</span><span class="sxs-lookup"><span data-stu-id="c58b2-148">Get started</span></span>

<span data-ttu-id="c58b2-149">構築を開始する準備ができましたか?</span><span class="sxs-lookup"><span data-stu-id="c58b2-149">Ready to get started building?</span></span> <span data-ttu-id="c58b2-150">クイックスタートのいずれかをお試しください。</span><span class="sxs-lookup"><span data-stu-id="c58b2-150">Try one of our quickstarts:</span></span>

### <a name="c"></a><span data-ttu-id="c58b2-151">C#</span><span class="sxs-lookup"><span data-stu-id="c58b2-151">C#</span></span>
* [<span data-ttu-id="c58b2-152">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c58b2-152">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
* [<span data-ttu-id="c58b2-153">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c58b2-153">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)

### <a name="javascript"></a><span data-ttu-id="c58b2-154">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c58b2-154">JavaScript</span></span>
* [<span data-ttu-id="c58b2-155">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c58b2-155">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
* [<span data-ttu-id="c58b2-156">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c58b2-156">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a><span data-ttu-id="c58b2-157">詳細情報</span><span class="sxs-lookup"><span data-stu-id="c58b2-157">Learn more</span></span>

* [<span data-ttu-id="c58b2-158">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="c58b2-158">Create a messaging extension</span></span>](~/messaging-extensions/how-to/create-messaging-extension.md)
* [<span data-ttu-id="c58b2-159">アクションメッセージング拡張コマンドの定義</span><span class="sxs-lookup"><span data-stu-id="c58b2-159">Define action messaging extension command</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="c58b2-160">検索メッセージ拡張コマンドの定義</span><span class="sxs-lookup"><span data-stu-id="c58b2-160">Define search messaging extension command</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="c58b2-161">アプリを計画する</span><span class="sxs-lookup"><span data-stu-id="c58b2-161">Planning your app</span></span>](../../concepts/extensibility-points.md)
* [<span data-ttu-id="c58b2-162">アプリのビルド</span><span class="sxs-lookup"><span data-stu-id="c58b2-162">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="c58b2-163">アプリの発行</span><span class="sxs-lookup"><span data-stu-id="c58b2-163">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
