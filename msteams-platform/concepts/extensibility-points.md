---
title: Teams アプリのエントリー ポイント
author: heath-hamilton
description: ユーザーが Teams でアプリを発見し、使用できる場所を説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713628"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="6a529-103">Teams アプリのエントリー ポイント</span><span class="sxs-lookup"><span data-stu-id="6a529-103">Entry points for Teams apps</span></span>

<span data-ttu-id="6a529-104">Teams プラットフォームには、ユーザーがアプリを発見して使用することができる柔軟なエントリー ポイントがあります。</span><span class="sxs-lookup"><span data-stu-id="6a529-104">The Teams platform provides a flexible set of entry points where people can discover and use your app.</span></span> <span data-ttu-id="6a529-105">アプリは、既存の Web コンテンツをタブに埋め込むようなシンプルなものから、ユーザーが複数のコンテキストで操作する多面的なものまであります。</span><span class="sxs-lookup"><span data-stu-id="6a529-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>

<span data-ttu-id="6a529-106">最もうまくいっているアプリは、Teams にネイティブな感覚なので、アプリのエントリー ポイントを慎重に計画することが重要です。</span><span class="sxs-lookup"><span data-stu-id="6a529-106">The most successful apps feel native to Teams, so it's important to carefully plan your app's entry points.</span></span>

## <a name="teams-channels-and-chats"></a><span data-ttu-id="6a529-107">Teams、チャネル、チャット</span><span class="sxs-lookup"><span data-stu-id="6a529-107">Teams, channels, and chats</span></span>

<span data-ttu-id="6a529-108">Teams、チャネル、およびチャットは共同作業スペースです。</span><span class="sxs-lookup"><span data-stu-id="6a529-108">Teams, channels, and chats are collaboration spaces.</span></span> <span data-ttu-id="6a529-109">このようなコンテキストでのアプリは、その空間内のすべてのユーザーが使用でき、一般的には、ワークフローの追加や新しい社会的対話の実現に重点が置かれます。</span><span class="sxs-lookup"><span data-stu-id="6a529-109">Apps in these contexts are available to everyone in that space and typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="6a529-110">ここでは、Teams アプリの機能が共同作業の場でどのように使われているかをご紹介します。</span><span class="sxs-lookup"><span data-stu-id="6a529-110">Here's how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="6a529-111">[**タブ**](~/tabs/what-are-tabs.md) には、チーム、チャネル、またはグループ チャットに合わせて構成される全画面の組み込み Web エクスペリエンスがあります。</span><span class="sxs-lookup"><span data-stu-id="6a529-111">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="6a529-112">すべてのメンバーは同じ Web ベースのコンテンツで会話するため、ステートレスなシングル ページ アプリ エクスペリエンスが一般的です。</span><span class="sxs-lookup"><span data-stu-id="6a529-112">All members interact with the same web-based content, so a stateless single page app experience is typical.</span></span>

* <span data-ttu-id="6a529-113">[**メッセージング拡張**](~/messaging-extensions/what-are-messaging-extensions.md) は、外部のコンテンツを会話に挿入したり、Teams を離れることなくメッセージにアクションを起こすためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="6a529-113">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="6a529-114">リンクの広がりは、共通の URL からコンテンツを共有する場合に、リッチ コンテンツを提供します。</span><span class="sxs-lookup"><span data-stu-id="6a529-114">Link unfurling provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="6a529-115">[**ボット**](~/bots/what-are-bots.md) は、チャットを通じて会話のメンバーと会話したり、イベント (新しいメンバーの追加や、チャネル名の変更など) に対応したりします。</span><span class="sxs-lookup"><span data-stu-id="6a529-115">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events (like adding a new member or renaming a channel).</span></span> <span data-ttu-id="6a529-116">このコンテキストでのボットとの会話は、チーム、チャネル、グループのすべてのメンバーに表示されるので、会話がすべてのユーザーに関連性のあるものであることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6a529-116">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations should be relevant to everyone.</span></span>

* <span data-ttu-id="6a529-117">[**Webhook とコネクタ**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) では、外部サービスが会話にメッセージを投稿したり、ユーザーがサービスにメッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="6a529-117">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="6a529-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) では、チーム、チャネル、グループ チャットに関するデータを取得し、Teams プロセスの自動化や管理に役立てます。</span><span class="sxs-lookup"><span data-stu-id="6a529-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="6a529-119">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="6a529-119">Personal apps</span></span>

<span data-ttu-id="6a529-120">[個人用アプリ](~/concepts/design/personal-apps.md) は、1 人のユーザーとのやりとりに焦点を当てます。</span><span class="sxs-lookup"><span data-stu-id="6a529-120">[Personal apps](~/concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="6a529-121">このコンテキストでのエクスペリエンスは、それぞれのユーザーに固有のものです。</span><span class="sxs-lookup"><span data-stu-id="6a529-121">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="6a529-122">ここでは、Teams の機能が個人的なコンテキストでどのように使われているかをご紹介します。</span><span class="sxs-lookup"><span data-stu-id="6a529-122">Here's how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="6a529-123">[**ボット**](~/bots/what-are-bots.md) はユーザーと 1 対 1 で会話します。</span><span class="sxs-lookup"><span data-stu-id="6a529-123">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="6a529-124">複数回の会話が必要なものや、特定のユーザーにのみ関連する通知を提供するボットは、個人用アプリに最適です。</span><span class="sxs-lookup"><span data-stu-id="6a529-124">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="6a529-125">[**タブ**](~/tabs/what-are-tabs.md) は、閲覧するユーザーにとって意味のある全画面の埋め込み Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="6a529-125">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that's meaningful to the user looking at it.</span></span>

## <a name="examples"></a><span data-ttu-id="6a529-126">例</span><span class="sxs-lookup"><span data-stu-id="6a529-126">Examples</span></span>

<span data-ttu-id="6a529-127">Teams アプリのデザイン ガイドラインでは、ユーザーがどこで Teams アプリを検出し、使用するかを示す詳細を視覚的に提供します。</span><span class="sxs-lookup"><span data-stu-id="6a529-127">The Teams app design guidelines provide detailed visuals showing you where people can find and use Teams apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a529-128">Teams アプリのデザイン ガイドラインを表示する</span><span class="sxs-lookup"><span data-stu-id="6a529-128">See the Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)
