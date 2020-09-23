---
title: Teams アプリのエントリポイント
author: heath-hamilton
description: ユーザーが Teams でアプリを使用する方法と場所について説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 1c68467177fc440993f059133f049f18785374b7
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209782"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="ac0c9-103">Teams アプリのエントリポイント</span><span class="sxs-lookup"><span data-stu-id="ac0c9-103">Entry points for Teams apps</span></span>

<span data-ttu-id="ac0c9-104">Teams プラットフォームには、ユーザーがアプリを見つけて使用できるようにするための一連のエントリポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-104">The Teams platform provides a flexible set of entry points where people can discover and use your app.</span></span> <span data-ttu-id="ac0c9-105">アプリはシンプルなものとして、既存の web サイトを個人タブに埋め込むことも、複数のエントリポイントでユーザーが操作するマルチファセットアプリにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-105">Your app can be as simple as embedding an existing website in a personal tab or a multi-faceted app that users interact with across several entry points.</span></span>

<span data-ttu-id="ac0c9-106">最も正常なアプリケーションは Teams にネイティブであると考えられるため、アプリのエントリポイントを慎重に計画することが重要です。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-106">The most successful apps feel native to Teams, so it's important to carefully plan your app's entry points.</span></span>

## <a name="teams-channels-and-group-chats"></a><span data-ttu-id="ac0c9-107">Teams、チャネル、グループチャット</span><span class="sxs-lookup"><span data-stu-id="ac0c9-107">Teams, channels, and group chats</span></span>

<span data-ttu-id="ac0c9-108">Teams、チャネル、グループチャットはコラボレーションスペースです。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-108">Teams, channels, and group chats are collaboration spaces.</span></span> <span data-ttu-id="ac0c9-109">これらのエントリポイントを使用するアプリは、すべてのメンバーが使用できます。通常、追加のワークフローまたは新しいソーシャル操作のロックに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-109">Apps that use these entry points are available to all members and typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="ac0c9-110">Teams のアプリ機能がコラボレーションコンテキストでよく使用される方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-110">Here's how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="ac0c9-111">[**タブ**](~/tabs/what-are-tabs.md) は、チーム、チャネル、またはグループチャット用に構成された全画面表示の web 環境を提供します。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-111">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="ac0c9-112">すべてのメンバーが同じ web ベースのコンテンツを操作するため、ステートレスなシングルページアプリの操作が一般的です。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-112">All members interact with the same web-based content, so a stateless single page app experience is typical.</span></span>

* <span data-ttu-id="ac0c9-113">[**メッセージング拡張機能**](~/messaging-extensions/what-are-messaging-extensions.md) は、外部コンテンツを会話に挿入したり、Teams を離れずにメッセージに対してアクションを実行したりするためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-113">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="ac0c9-114">Link unfurling は、共通の URL からコンテンツを共有するときに、豊富なコンテンツを提供します。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-114">Link unfurling provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="ac0c9-115">[**Bot**](~/bots/what-are-bots.md) はチャットを通じて会話のメンバーと対話し、イベントに応答します (新しいメンバーの追加やチャネルの名前変更など)。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-115">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events (like adding a new member or renaming a channel).</span></span> <span data-ttu-id="ac0c9-116">これらのコンテキストで bot との会話は、チーム、チャネル、またはグループのすべてのメンバーに表示されるので、すべてのユーザーに関連する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-116">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations should be relevant to everyone.</span></span>

* <span data-ttu-id="ac0c9-117">[**Webhooks とコネクタ**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) を使用すると、外部サービスがメッセージを会話に投稿し、ユーザーがサービスにメッセージを送信できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-117">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="ac0c9-118">Teams、チャネル、グループチャットに関するデータを取得するための[**Microsoft GRAPH REST API**](https://docs.microsoft.com/graph/teams-concept-overview) 。 teams プロセスの自動化と管理に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="ac0c9-119">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="ac0c9-119">Personal apps</span></span>

<span data-ttu-id="ac0c9-120">[個人用アプリ](~/concepts/design/personal-apps.md) は、1人のユーザーとの対話に重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-120">[Personal apps](~/concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="ac0c9-121">このコンテキストの動作は、各ユーザーに固有です。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-121">The experience in this context is unique to each user.</span></span> <span data-ttu-id="ac0c9-122">ユーザーは、個人用アプリを左側のナビゲーションレールにピン留めして、簡単にアクセスできるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-122">Users can pin personal apps to the left navigation rail for quick access.</span></span>

<span data-ttu-id="ac0c9-123">Teams 機能が個人コンテキストでよく使用される方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-123">Here's how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="ac0c9-124">[**ボット**](~/bots/what-are-bots.md) には、1対1のユーザーとの会話があります。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-124">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="ac0c9-125">マルチターン会話を必要とするボット、または特定のユーザーにのみ関連する通知を提供する場合は、個人コンテキストに適しています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-125">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal contexts.</span></span>

* <span data-ttu-id="ac0c9-126">[**タブ**](~/tabs/what-are-tabs.md) には、個々のユーザーにとって有用な全画面表示の web 環境が用意されています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-126">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that's meaningful to individual users.</span></span>

## <a name="ui-components"></a><span data-ttu-id="ac0c9-127">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="ac0c9-127">UI components</span></span>

<span data-ttu-id="ac0c9-128">通常、アプリは1つ以上の標準 Teams UI コンポーネントを示しています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-128">Apps typically exhibit one or more standard Teams UI components.</span></span> <span data-ttu-id="ac0c9-129">これらのコンポーネントを使用してアプリを構築すると、Teams ユーザーにネイティブなエクスペリエンスを実現できます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-129">Building out your app using these components leads to rich experiences that feel native to Teams users.</span></span>

### <a name="cards"></a><span data-ttu-id="ac0c9-130">カード</span><span class="sxs-lookup"><span data-stu-id="ac0c9-130">Cards</span></span>

<span data-ttu-id="ac0c9-131">[カード](~/task-modules-and-cards/what-are-cards.md) は、JSON で定義された UI コンテナーで、書式設定されたテキスト、メディア、コントロール (ドロップダウンやラジオボタンなど) や、アクションをトリガーするボタンを含むことができます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-131">[Cards](~/task-modules-and-cards/what-are-cards.md) are UI containers defined by JSON that can contain formatted text, media, controls (like dropdowns and radio buttons) and buttons that trigger an action.</span></span>

<span data-ttu-id="ac0c9-132">カード アクションは、アプリの API にペイロードを送信したり、リンクを開いたり、認証フローを開始したり、会話にメッセージを送信したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-132">Card actions can send payloads to your app's API, open a link, initiate authentication flows, or send messages to conversations.</span></span> <span data-ttu-id="ac0c9-133">Teams プラットフォームは、アダプティブカード、英雄カード、サムネイルカードなど、複数のカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-133">The Teams platform supports multiple cards, including Adaptive Cards, hero cards, thumbnail cards, and more.</span></span> <span data-ttu-id="ac0c9-134">カードコレクションを結合して、リストまたはカルーセルに表示することができます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-134">You can combine card collections and display in a list or carousel.</span></span>

### <a name="task-modules"></a><span data-ttu-id="ac0c9-135">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="ac0c9-135">Task modules</span></span>

<span data-ttu-id="ac0c9-136">[タスクモジュール](~/task-modules-and-cards/what-are-task-modules.md) は Teams でモーダルエクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-136">[Task modules](~/task-modules-and-cards/what-are-task-modules.md) provide modal experiences in Teams.</span></span> <span data-ttu-id="ac0c9-137">これは、ワークフローの開始、ユーザー入力の収集、またはビデオや Power BI ダッシュボードなどの豊富な情報の表示に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-137">They are especially useful for initiating workflows, collecting user input, or displaying rich information such as videos or Power BI dashboards.</span></span> <span data-ttu-id="ac0c9-138">タスクモジュールでは、カスタムフロントエンドコードを実行したり、ウィジェットを表示したり、アダプティブカードを表示したりすることができ `<iframe>` ます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-138">In task modules, you can run custom front-end code, display an `<iframe>` widget, or show an Adaptive Card.</span></span>

<span data-ttu-id="ac0c9-139">アプリの構築方法を検討する場合は、ユーザーがタブや会話ベースの bot の操作と比較して情報を入力したり、タスクを完了したりすることが自然であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-139">When considering how you want to build your app, remember that modals are natural for users to enter information or complete tasks compared to a tab or a conversation-based bot experience.</span></span>

### <a name="deep-links"></a><span data-ttu-id="ac0c9-140">ディープ リンク</span><span class="sxs-lookup"><span data-stu-id="ac0c9-140">Deep links</span></span>

<span data-ttu-id="ac0c9-141">アプリでは、アプリや Teams クライアントを使用してユーザーを移動するのに役立つ [URL の詳細なリンク](~/concepts/build-and-test/deep-links.md) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-141">Your app can create [URL deep links](~/concepts/build-and-test/deep-links.md) to help navigate your user through your app, and the Teams client.</span></span> <span data-ttu-id="ac0c9-142">Teams 内のほとんどのエンティティに対して深いリンクを作成できます。また (新しい会議出席依頼のような)、URL のクエリ文字列を使用して情報を事前設定することができます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-142">You can create a deep link for most entities within Teams, and some (like a new meeting request) allow you to pre-populate information using query strings in the URL.</span></span>

<span data-ttu-id="ac0c9-143">たとえば、会話の bot が、1対1のメッセージとしてカードを送信するタスクモジュールへの深いリンクを持つチャネルにメッセージを送信すると、特定の日時に特定のユーザーによって新しい会議を作成するための深いリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-143">For example, your conversational bot could send a message to a channel with a deep link to a task module that results in a card being sent as a one-to-one message to a user, that in turn contains a deep link to create a new meeting with a specific user at a certain date/time.</span></span> <span data-ttu-id="ac0c9-144">ディープ リンクを使用すれば、アプリで利用可能なさまざまな拡張ポイントを横断的に接続し、ユーザーを常に正しいコンテキストに維持することができます。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-144">Use deep links to connect across the various extension points available to your app, keeping your user in the correct context at all times.</span></span>

### <a name="web-based-content"></a><span data-ttu-id="ac0c9-145">Web ベースのコンテンツ</span><span class="sxs-lookup"><span data-stu-id="ac0c9-145">Web-based content</span></span>

<span data-ttu-id="ac0c9-146">[Web ベースのコンテンツ](~/tabs/how-to/create-tab-pages/content-page.md) は、タブまたはタスクモジュールに埋め込むことができる、ホストする web ページです。</span><span class="sxs-lookup"><span data-stu-id="ac0c9-146">[Web-based content](~/tabs/how-to/create-tab-pages/content-page.md) is a webpage you host that can be embedded in a tab or task module.</span></span>
