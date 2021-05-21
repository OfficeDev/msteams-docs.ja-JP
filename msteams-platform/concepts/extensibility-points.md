---
title: Teams アプリのエントリー ポイント
author: heath-hamilton
description: ユーザーが Teams でアプリを発見し、使用できる場所を説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: c26b938f56af6f09c0e4ba274b9b3f4da19d08ee
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566174"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="eac09-103">Teams アプリのエントリー ポイント</span><span class="sxs-lookup"><span data-stu-id="eac09-103">Entry points for Teams apps</span></span>

<span data-ttu-id="eac09-104">このTeamsプラットフォームは、チーム、チャネル、チャットなどの柔軟なエントリ ポイントセットを提供し、ユーザーがアプリを検出して使用できます。</span><span class="sxs-lookup"><span data-stu-id="eac09-104">The Teams platform provides a flexible set of entry points, such as team, channel, and chat where people can discover and use your app.</span></span> <span data-ttu-id="eac09-105">アプリは、既存の Web コンテンツをタブに埋め込むようなシンプルなものから、ユーザーが複数のコンテキストで操作する多面的なものまであります。</span><span class="sxs-lookup"><span data-stu-id="eac09-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>
<span data-ttu-id="eac09-106">最も成功したアプリは、Teamsネイティブなので、アプリのエントリ ポイントを慎重に選択します。</span><span class="sxs-lookup"><span data-stu-id="eac09-106">The most successful apps are native to Teams, so choose your app's entry points carefully.</span></span>

## <a name="shared-app-experiences"></a><span data-ttu-id="eac09-107">共有アプリ エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="eac09-107">Shared app experiences</span></span>

<span data-ttu-id="eac09-108">チーム、チャネル、チャットはコラボレーション スペースです。</span><span class="sxs-lookup"><span data-stu-id="eac09-108">Team, channel, and chat are collaboration spaces.</span></span> <span data-ttu-id="eac09-109">これらのコンテキストのアプリは、その領域内のすべてのユーザーが利用できます。</span><span class="sxs-lookup"><span data-stu-id="eac09-109">Apps in these contexts are available to everyone in that space.</span></span> <span data-ttu-id="eac09-110">通常、コラボレーション スペースは、追加のワークフローに焦点を当てたり、新しいソーシャル操作のロックを解除したりします。</span><span class="sxs-lookup"><span data-stu-id="eac09-110">Collaboration spaces typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="eac09-111">次の一覧は、コラボレーション コンテキストTeamsアプリの機能が一般的に使用される方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="eac09-111">The following list shows how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="eac09-112">[**タブ**](~/tabs/what-are-tabs.md) には、チーム、チャネル、またはグループ チャットに合わせて構成される全画面の組み込み Web エクスペリエンスがあります。</span><span class="sxs-lookup"><span data-stu-id="eac09-112">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="eac09-113">すべてのメンバーが同じ Web ベースのコンテンツを操作します。そのため、ステートレスな単一ページ アプリ エクスペリエンスが一般的です。</span><span class="sxs-lookup"><span data-stu-id="eac09-113">All members interact with the same web-based content, so a stateless single-page app experience is typical.</span></span>

* <span data-ttu-id="eac09-114">[**メッセージング拡張**](~/messaging-extensions/what-are-messaging-extensions.md) は、外部のコンテンツを会話に挿入したり、Teams を離れることなくメッセージにアクションを起こすためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="eac09-114">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="eac09-115">[リンク解除は、共通](~/messaging-extensions/how-to/link-unfurling.md) の URL からコンテンツを共有するときにリッチ コンテンツを提供します。</span><span class="sxs-lookup"><span data-stu-id="eac09-115">[Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="eac09-116">[**ボットは**](~/bots/what-are-bots.md) 、チャットを通じて会話のメンバーと対話し、新しいメンバーの追加やチャネルの名前の変更などのイベントに応答します。</span><span class="sxs-lookup"><span data-stu-id="eac09-116">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events, such as adding a new member or renaming a channel.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="eac09-117">これらのコンテキストでのボットとの会話は、チーム、チャネル、またはグループのすべてのメンバーに表示されます。そのため、ボットの会話は全員に関連している必要があります。</span><span class="sxs-lookup"><span data-stu-id="eac09-117">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations must be relevant to everyone.</span></span>

* <span data-ttu-id="eac09-118">[**Webhook とコネクタ**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) では、外部サービスが会話にメッセージを投稿したり、ユーザーがサービスにメッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="eac09-118">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="eac09-119">[**Microsoft Graph REST API**](/graph/teams-concept-overview) では、チーム、チャネル、グループ チャットに関するデータを取得し、Teams プロセスの自動化や管理に役立てます。</span><span class="sxs-lookup"><span data-stu-id="eac09-119">[**Microsoft Graph REST API**](/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-app-experiences"></a><span data-ttu-id="eac09-120">個人用アプリエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="eac09-120">Personal app experiences</span></span>

<span data-ttu-id="eac09-121">[個人用アプリ](../concepts/design/personal-apps.md) は、1 人のユーザーとのやりとりに焦点を当てます。</span><span class="sxs-lookup"><span data-stu-id="eac09-121">[Personal apps](../concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="eac09-122">このコンテキストでのエクスペリエンスは、それぞれのユーザーに固有のものです。</span><span class="sxs-lookup"><span data-stu-id="eac09-122">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="eac09-123">次の一覧は、Teams機能が個人のコンテキストで一般的に使用される方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="eac09-123">The following list shows how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="eac09-124">[**ボット**](~/bots/what-are-bots.md) はユーザーと 1 対 1 で会話します。</span><span class="sxs-lookup"><span data-stu-id="eac09-124">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="eac09-125">複数回の会話が必要なものや、特定のユーザーにのみ関連する通知を提供するボットは、個人用アプリに最適です。</span><span class="sxs-lookup"><span data-stu-id="eac09-125">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="eac09-126">[**タブ**](~/tabs/what-are-tabs.md) は、それを見ているユーザーにとって意味のある、フルスクリーンの埋め込み Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="eac09-126">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that is meaningful to the user looking at it.</span></span>

## <a name="see-also"></a><span data-ttu-id="eac09-127">関連項目</span><span class="sxs-lookup"><span data-stu-id="eac09-127">See also</span></span>

[<span data-ttu-id="eac09-128">Teamsの設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="eac09-128">Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="eac09-129">次の手順</span><span class="sxs-lookup"><span data-stu-id="eac09-129">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eac09-130">使用例を理解する</span><span class="sxs-lookup"><span data-stu-id="eac09-130">Understand use cases</span></span>](../concepts/design/understand-use-cases.md)
