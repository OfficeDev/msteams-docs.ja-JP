---
title: Teams アプリのコンテキストを決定する
author: heath-hamilton
description: Teams アプリの計画では、共同作業スペース、個人スペース、またはその両方でアプリを使用するかどうかを決定する必要があります。
ms.openlocfilehash: 05c92aa8b199cbdb58e477fb4a64467c150edbfd
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652075"
---
# <a name="getting-to-know-teams-ui-conventions"></a><span data-ttu-id="b69ef-103">Teams の UI 規則について学ぶ</span><span class="sxs-lookup"><span data-stu-id="b69ef-103">Getting to know Teams UI conventions</span></span>

<span data-ttu-id="b69ef-104">通常、アプリは1つ以上の標準 Teams の UI 規則を示しています。</span><span class="sxs-lookup"><span data-stu-id="b69ef-104">Apps typically exhibit one or more standard Teams UI conventions.</span></span> <span data-ttu-id="b69ef-105">これらの規則を使用してアプリの機能を構築することで、Teams ユーザーにネイティブなエクスペリエンスを実現できます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-105">Building out your app's capabilities using these conventions leads to rich experiences that feel native to Teams users.</span></span>

## <a name="cards"></a><span data-ttu-id="b69ef-106">カード</span><span class="sxs-lookup"><span data-stu-id="b69ef-106">Cards</span></span>

<span data-ttu-id="b69ef-107">[カード](~/task-modules-and-cards/what-are-cards.md) は、複数のプロパティと添付ファイルを含むことができる schematized JSON によって定義された UI コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="b69ef-107">[Cards](~/task-modules-and-cards/what-are-cards.md) are UI containers defined by schematized JSON that can contain multiple properties and attachments.</span></span> <span data-ttu-id="b69ef-108">書式設定されたテキスト、メディア、コントロール (ドロップダウンボックスやラジオボタンなど) や、カードアクションをトリガーするボタンを含むことができます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-108">They can contain formatted text, media, controls (like dropdown boxes and radio buttons) and buttons that trigger card actions.</span></span>

<span data-ttu-id="b69ef-109">カード アクションは、アプリの API にペイロードを送信したり、リンクを開いたり、認証フローを開始したり、会話にメッセージを送信したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-109">Card actions can send payloads to your app's API, open a link, initiate authentication flows, or send messages to conversations.</span></span> <span data-ttu-id="b69ef-110">Teams プラットフォームでは、アダプティブカード、英雄カード、サムネイルカードなど、複数の種類のカードがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b69ef-110">The Teams platform supports multiple types of cards, including Adaptive Cards, hero cards, thumbnail cards, and more.</span></span> <span data-ttu-id="b69ef-111">カードコレクションを結合して、リストまたはカルーセルに表示することができます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-111">You can combine card collections and displayed in a list or carousel.</span></span>

## <a name="task-modules"></a><span data-ttu-id="b69ef-112">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="b69ef-112">Task modules</span></span>

<span data-ttu-id="b69ef-113">[タスクモジュール](~/task-modules-and-cards/what-are-task-modules.md) は Teams でモーダルポップアップエクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="b69ef-113">[Task modules](~/task-modules-and-cards/what-are-task-modules.md) provide modal popup experiences in Teams.</span></span> <span data-ttu-id="b69ef-114">これは、ワークフローの開始、ユーザー入力の収集、またはビデオや Power BI ダッシュボードなどの豊富な情報の表示に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="b69ef-114">They are especially useful for initiating workflows, collecting user input, or displaying rich information such as videos or Power BI dashboards.</span></span> <span data-ttu-id="b69ef-115">タスクモジュールでは、カスタムフロントエンドコードを実行したり、ウィジェットを表示したり、アダプティブカードを表示したりすることができ `<iframe>` ます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-115">In task modules, you can run custom front-end code, display an `<iframe>` widget, or show an Adaptive Card.</span></span>

<span data-ttu-id="b69ef-116">アプリの構築方法を検討する場合は、ユーザーがタブや会話ベースの bot の操作と比較して情報を入力したり、タスクを完了したりすることが自然であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b69ef-116">When considering how you want to build your app, remember that modals are natural for users to enter information or complete tasks compared to a tab or a conversation-based bot experience.</span></span>

## <a name="deep-links"></a><span data-ttu-id="b69ef-117">ディープ リンク</span><span class="sxs-lookup"><span data-stu-id="b69ef-117">Deep links</span></span>

<span data-ttu-id="b69ef-118">アプリでは、アプリや Teams クライアントを使用してユーザーを移動するのに役立つ [URL の詳細なリンク](~/concepts/build-and-test/deep-links.md) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-118">Your app can create [URL deep links](~/concepts/build-and-test/deep-links.md) to help navigate your user through your app, and the Teams client.</span></span> <span data-ttu-id="b69ef-119">ディープ リンクは Teams 内のほとんどのエンティティに対して作成することができ、一部のエンティティ (新しい会議出席依頼など) では、クエリ文字列を使用して URL に情報を事前設定しておくことができます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-119">You can create a deeplink for most entities within Teams, and some (like a new meeting request) allow you to pre-populate information using query strings in the URL.</span></span> 

<span data-ttu-id="b69ef-120">たとえば、会話ボットは、タスク モジュールへのディープ リンクを持つチャネルにメッセージを送信し、その結果、カードはユーザーに 1 対 1 のメッセージとして送信され、そこには特定の日時に特定のユーザーとの新しい会議を作成するディープ リンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b69ef-120">For example, your conversational bot could send a message to a channel with a deeplink to a task module that results in a card being sent as a one-to-one message to a user, that in turn contains a deeplink to create a new meeting with a specific user at a certain date/time.</span></span> <span data-ttu-id="b69ef-121">ディープ リンクを使用すれば、アプリで利用可能なさまざまな拡張ポイントを横断的に接続し、ユーザーを常に正しいコンテキストに維持することができます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-121">Use deep links to connect across the various extension points available to your app, keeping your user in the correct context at all times.</span></span>

## <a name="web-based-content"></a><span data-ttu-id="b69ef-122">Web ベースのコンテンツ</span><span class="sxs-lookup"><span data-stu-id="b69ef-122">Web-based content</span></span>

<span data-ttu-id="b69ef-123">[Web ベースのコンテンツ](~/tabs/how-to/create-tab-pages/content-page.md) は、タブまたはタスクモジュールに埋め込むことができる、ホストする web ページです。</span><span class="sxs-lookup"><span data-stu-id="b69ef-123">[Web-based content](~/tabs/how-to/create-tab-pages/content-page.md) is a webpage you host that can be embedded in a tab or task module.</span></span> <span data-ttu-id="b69ef-124">Web ページを Teams クライアントに埋め込むには、次のものを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b69ef-124">To embed your webpage in the Teams client, it must:</span></span>

* <span data-ttu-id="b69ef-125">`HTTPS`URL に含めます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-125">Include `HTTPS` in the URL.</span></span>
* <span data-ttu-id="b69ef-126">に埋め込むことができ `<iframe>` ます。</span><span class="sxs-lookup"><span data-stu-id="b69ef-126">Be embedded in an `<iframe>`.</span></span>
* <span data-ttu-id="b69ef-127">Microsoft Teams JavaScript クライアント SDK を含み、 `initialize()` ページ読み込み時に SDK のメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b69ef-127">Include the Microsoft Teams JavaScript client SDK and invoke the SDK's `initialize()` method on page load.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b69ef-128">次のステップ</span><span class="sxs-lookup"><span data-stu-id="b69ef-128">Next steps</span></span>

* [<span data-ttu-id="b69ef-129">アプリの設計</span><span class="sxs-lookup"><span data-stu-id="b69ef-129">Designing your app</span></span>](../../tabs/design/tabs.md)
