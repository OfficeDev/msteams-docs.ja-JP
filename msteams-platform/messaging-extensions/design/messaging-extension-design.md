---
title: メッセージング拡張機能の設計ガイドライン
description: メッセージング拡張機能を作成するためのガイドラインについて説明します。
keywords: teams 設計ガイドラインリファレンスメッセージング拡張のヒントベストプラクティス
author: EmilyyC
ms.author: qinch
ms.openlocfilehash: cf2862b8c8544efcab21616c420d66937fb7406a
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801313"
---
# <a name="start-sharing-with-powerful-messaging-extensions"></a><span data-ttu-id="d8c4e-104">強力なメッセージング拡張機能を使用した共有の開始</span><span class="sxs-lookup"><span data-stu-id="d8c4e-104">Start sharing with powerful messaging extensions</span></span>

<span data-ttu-id="d8c4e-105">メッセージング拡張機能は、アクション可能なコンテンツを共有するために設計されています。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-105">Messaging extensions are designed for sharing actionable content.</span></span> <span data-ttu-id="d8c4e-106">この機能は、スタックでの投資収益率 (ROI) の最大値を表します。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-106">This feature represents the highest return on investment (ROI) in our stack.</span></span> <span data-ttu-id="d8c4e-107">メッセージング拡張機能はチャットとチャネルで機能し、複数のクエリエンドポイントをサポートし、新しいエンティティの作成を有効にし、リンク unfurling を使用してカスタムリンクプレビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-107">Messaging extensions work in chat and channels, support multiple query endpoints, enable the creation of new entities, and work with link unfurling to create custom link previews.</span></span> <span data-ttu-id="d8c4e-108">この機能は強力で非常に便利ですが、簡単に見つけることができません。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-108">The challenge is that while the feature is powerful and incredibly useful, it's not easily discoverable.</span></span> <span data-ttu-id="d8c4e-109">このガイドでは、より多くのユーザーが簡単に見つけて使用できるメッセージング拡張機能を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-109">This guide will help you create messaging extensions that are readily found and utilized by more users.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="d8c4e-110">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="d8c4e-110">Design guidelines</span></span>

### <a name="show-content-as-a-user-type"></a><span data-ttu-id="d8c4e-111">コンテンツをユーザーの種類として表示する</span><span class="sxs-lookup"><span data-stu-id="d8c4e-111">Show content as a user type</span></span>

<span data-ttu-id="d8c4e-112">メッセージング拡張機能では、キーワード検索を使用して、1人以上のユーザーと共有できるアクション可能なコンテンツを検索するための一意の方法が提供されます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-112">Messaging extensions present a unique way to use keyword searches to find actionable content that can be shared with one or more users.</span></span> <span data-ttu-id="d8c4e-113">この優先する操作により、ユーザーは、ユーザーの種類として、遅延した自動クエリを使用して検索用語を入力できます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-113">This preferred interaction allows users to enter search terms with a delayed auto query as the user type.</span></span> <span data-ttu-id="d8c4e-114">このモデルでは、提案された結果をシミュレートすることができ、ユーザーには最小限の文字を入力するよう要求します。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-114">This model does a good job of simulating suggested results and requires users to type minimal characters.</span></span>

> [!TIP]
><span data-ttu-id="d8c4e-115">クエリを送信する前にユーザーに選択させる必要がありますが、望ましいとは限りません `enter` `search` 。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-115">It's possible, but not desirable, to require users to select `enter` or `search` before sending queries.</span></span> <span data-ttu-id="d8c4e-116">バックエンドサービスの負荷は低くなっていますが、このモデルは標準ではないため、ユーザーを混乱させる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-116">While there is less stress on the backend service, this model is not the norm and may confuse users.</span></span>

### <a name="consider-zero-term-queries"></a><span data-ttu-id="d8c4e-117">0個のクエリを考慮する</span><span class="sxs-lookup"><span data-stu-id="d8c4e-117">Consider zero-term queries</span></span>

<span data-ttu-id="d8c4e-118">ゼロを使用したクエリは、ユーザーが検索ボックスに用語を記述するのではなく、ユーザーの操作によって直接開始されます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-118">Zero-term queries are directly triggered by user action, rather than by the user writing terms in a search box.</span></span> <span data-ttu-id="d8c4e-119">すべてのメッセージング拡張機能は、通常、ユーザーが最後にサービスを閲覧したものに基づいて、ゼロのクエリからメリットを得られます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-119">All messaging extensions benefit from zero-term queries, usually based on what the user last saw on the service.</span></span> <span data-ttu-id="d8c4e-120">利点として、ユーザーが最後に閲覧したものが非常に高いことがわかります。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-120">The advantage is that the likelihood of wanting to share something the user last saw is quite high.</span></span> <span data-ttu-id="d8c4e-121">その他のゼロのクエリは、サービスに基づいている場合があります。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-121">Other zero-term queries might be based on the service.</span></span> <span data-ttu-id="d8c4e-122">たとえば、最近の `news` イベントや今後のイベントから、最近投稿されたニュースの内線番号を表示する場合があります。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-122">For instance, `news`  might show recently posted news extensions from recent and upcoming events.</span></span>

<img width="450px" title="[新しい構成] タブ" src="../../assets/images/messaging-extension/zero-term-query.png" />

### <a name="include-link-unfurling"></a><span data-ttu-id="d8c4e-124">リンクの unfurling を含める</span><span class="sxs-lookup"><span data-stu-id="d8c4e-124">Include link unfurling</span></span>

<span data-ttu-id="d8c4e-125">チーム内のコンテンツを共有する最も一般的な方法の1つは、ハイパーリンクを使用して、作業しているタスクであっても、おかしいことが検出されたビデオであるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-125">One of the most common ways to share content in Teams is through a hyperlink, whether it is a task you've been working on or a  video that you found funny.</span></span> <span data-ttu-id="d8c4e-126">ユーザーが Teams でリンクを共有すると、画像、タイトル、説明などのプレビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-126">When a user shares a link in Teams, a  preview including image, title or description is displayed.</span></span> <span data-ttu-id="d8c4e-127">[リンク unfurling](../how-to/link-unfurling.md)を使用すると、これらのプレビューをカスタマイズできるようになります。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-127">With [link unfurling](../how-to/link-unfurling.md) you can now customize these previews.</span></span> <span data-ttu-id="d8c4e-128">ユーザーがプレビューの使用を決定した後で、アプリをインストールするように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-128">Users will also be prompted to install your app after they decide to use your preview.</span></span> <span data-ttu-id="d8c4e-129">Link unfurling 機能をアプリに追加すると、アプリの検出可能性が大幅に向上します。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-129">Adding link unfurling functionality to your app can greatly increase your app discoverability.</span></span>

### <a name="highlight-your-messaging-extension"></a><span data-ttu-id="d8c4e-130">メッセージング拡張機能を強調表示する</span><span class="sxs-lookup"><span data-stu-id="d8c4e-130">Highlight your messaging extension</span></span>

<span data-ttu-id="d8c4e-131">メッセージング拡張機能は、必ずしも簡単に見つけることができません。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-131">Messaging extensions are not always easy to find.</span></span> <span data-ttu-id="d8c4e-132">アプリの詳細ページにアプリのスクリーンショットを含め、ヘルプドキュメントを使用してメッセージングの内線番号を機能させることができます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-132">Include app screenshots in the app detail page and your help documentation to feature your messaging extension.</span></span> <span data-ttu-id="d8c4e-133">また、ボットツアーで、bot との相互作用以外のアプリ全体を強調表示するための*方法*に関するドキュメントを含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-133">You can also include *how-to* documentation for your messaging extension in bot tours to highlight the entire app beyond the bot interactions.</span></span>

### <a name="add-actions-on-card"></a><span data-ttu-id="d8c4e-134">カードにアクションを追加する</span><span class="sxs-lookup"><span data-stu-id="d8c4e-134">Add actions on card</span></span>

<span data-ttu-id="d8c4e-135">ユーザーにテキストを表示するだけではありません。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-135">Don't just display text to users.</span></span> <span data-ttu-id="d8c4e-136">ユーザーが操作して次のアクションを実行できることを示します。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-136">Have something they can interact with and perform the next action.</span></span> <span data-ttu-id="d8c4e-137">たとえば、プレースアプリは、カードにマップを挿入するだけでなく、選択すると、その場所への方向を表示するボタンも持っています。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-137">For example, the Places app doesn't just insert a map on the card, but also has a button that, when selected, will show directions to the location.</span></span> <span data-ttu-id="d8c4e-138">ユーザーは、カードを入手した後で、より多くのタスクを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-138">Users can perform more tasks after obtaining the card.</span></span>

<img width="450px" title="[新しい構成] タブ" src="../../assets/images/messaging-extension/action-on-card.png" />

### <a name="keep-users-in-the-app-context"></a><span data-ttu-id="d8c4e-140">アプリコンテキストでユーザーを保持する</span><span class="sxs-lookup"><span data-stu-id="d8c4e-140">Keep users in the app context</span></span>

<span data-ttu-id="d8c4e-141">カードが足りず、詳細情報を得るためにリンクを提供する必要がある場合は、ユーザーが快適に表示されるように、ブラウザーを開くのではなくタブを開くことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-141">If a card is not enough and you need to provide a link for more information, consider opening a tab instead of opening a browser for a better user experience.</span></span> <span data-ttu-id="d8c4e-142">「[ユーザー設定のチームアプリの wit を拡張する」を](../../tabs/how-to/add-tab.md)*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="d8c4e-142">*See* [Extend you Teams app wit a custom tab](../../tabs/how-to/add-tab.md)</span></span>