---
title: Microsoft Teams プラットフォーム用アプリを構築する
author: heath-hamilton
description: 開発者がカスタム アプリを使用して Microsoft Teams の機能を拡張する方法の概要について説明します。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 9f043fd5bab441ce88b0e04b4254b925aff25aad
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911885"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="9bb9f-103">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="9bb9f-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="9bb9f-104">Microsoft Teams アプリは、重要な情報、一般的なツール、信頼できるプロセスを提供し、ユーザーの収集、学習、作業が増えています。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="9bb9f-105">アプリは、ニーズに合わせて Teams を拡張する方法です。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="9bb9f-106">Teams の新しいアプリを作成するか、既存のアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9bb9f-107">ここから開始</span><span class="sxs-lookup"><span data-stu-id="9bb9f-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="9bb9f-108">Teams アプリとは</span><span class="sxs-lookup"><span data-stu-id="9bb9f-108">What are Teams apps?</span></span>

<span data-ttu-id="9bb9f-109">Teams アプリは、機能と [エントリ ポイントの](concepts/capabilities-overview.md) 組み [合わせです](concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="9bb9f-110">たとえば、ユーザーはチャネル *(エントリ* ポイント) でアプリのボット(機能) とチャットできます。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="9bb9f-111">一部のアプリは単純な (通知を送信する) 一方で、他のアプリは複雑です (患者の記録を管理します)。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="9bb9f-112">アプリを計画する際には、Teams はコラボレーション ハブです。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="9bb9f-113">最高の Teams アプリは、ユーザーが自分自身を表現し、より良く一緒に作業するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="9bb9f-114">タブ</span><span class="sxs-lookup"><span data-stu-id="9bb9f-114">Tabs</span></span>

<span data-ttu-id="9bb9f-115">**情報をより便利に取得** する : 場合によっては、見つけやすくする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="9bb9f-116">タブに重要な Web [ページを表示](tabs/what-are-tabs.md)します。このタブは、Teams の静的および動的なコンテンツに対して、全画面の Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでのタブの外観の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="9bb9f-118">ボット</span><span class="sxs-lookup"><span data-stu-id="9bb9f-118">Bots</span></span>

<span data-ttu-id="9bb9f-119">**単語をアクション** に変換する : 会話の結果、多くの場合、何かを行う必要があります (注文の生成、コードの確認、チケットの状態の確認など)。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="9bb9f-120">ボット [は](bots/what-are-bots.md) 、Teams 内でこの種のワークフローを開始できます。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでのボットの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="9bb9f-122">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="9bb9f-122">Messaging extensions</span></span>

<span data-ttu-id="9bb9f-123">**マルチタスクを容易にする**: メッセージング [拡張機能](messaging-extensions/what-are-messaging-extensions.md)を使用すると、会話内で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="9bb9f-124">また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理を実行できます。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでのメッセージング拡張機能の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="9bb9f-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="9bb9f-126">Webhooks</span></span>

<span data-ttu-id="9bb9f-127">**外部アプリと通信** する : [受信 Webhook は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 、別のアプリから Teams チャネルに自動的に通知を送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="9bb9f-128">送信 [Webhook を使用して、Web](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)サービスにメッセージを送信@mention。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでのコネクタの外観の概念表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="9bb9f-130">Teams 用 Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="9bb9f-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="9bb9f-131">**Teams データ** の利用 : Teams 用 [Microsoft Graph API](https://docs.microsoft.com/graph/teams-concept-overview) は、アプリの機能の作成や強化に役立つ、チーム、チャネル、ユーザー、メッセージに関する情報へのアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API for Teams の概念表現。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="9bb9f-133">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="9bb9f-133">Start building</span></span>

   <span data-ttu-id="9bb9f-134">簡単なアプリを作成し、一般的に使用される機能を追加することで、Teams の構築についてすぐに理解できます。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-134">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="9bb9f-135">最初のアプリを今すぐビルドする</span><span class="sxs-lookup"><span data-stu-id="9bb9f-135">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="9bb9f-136">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="9bb9f-136">Integrate with Teams</span></span>

   <span data-ttu-id="9bb9f-137">ユーザーが既存の Web アプリ、サービス、またはシステムについて気に入った機能を、Teams の共同作業機能とブレンドします。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="9bb9f-138">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="9bb9f-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="9bb9f-139">簡単なコードは長い道のりを行く</span><span class="sxs-lookup"><span data-stu-id="9bb9f-139">A little code goes a long way</span></span>

   <span data-ttu-id="9bb9f-140">You don't need to be an expert programmer to build a great Teams app.</span><span class="sxs-lookup"><span data-stu-id="9bb9f-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="9bb9f-141">いくつかの低コード ソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="9bb9f-141">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="9bb9f-142">低コード アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="9bb9f-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="9bb9f-143">リソース</span><span class="sxs-lookup"><span data-stu-id="9bb9f-143">Resources</span></span>

* <span data-ttu-id="9bb9f-144">[Web サイトに [Share-to-Teams] ボタンを追加する](concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="9bb9f-144">[Add a Share-to-Teams button to your website](concepts/build-and-test/share-to-teams.md)</span></span>
* [<span data-ttu-id="9bb9f-145">Teams アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="9bb9f-145">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="9bb9f-146">Microsoft Teams JavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="9bb9f-146">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="9bb9f-147">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) および [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="9bb9f-147">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="9bb9f-148">Teams アプリを公開する</span><span class="sxs-lookup"><span data-stu-id="9bb9f-148">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
