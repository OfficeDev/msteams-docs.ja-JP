---
title: Microsoft Teams プラットフォーム用のアプリを構築する
author: heath-hamilton
description: 開発者がカスタムアプリを使用して Microsoft Teams の機能を拡張およびカスタマイズする方法の概要。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6f5f3454885320669ef42383529d39fcfcfdfee8
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604788"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="5bb2a-103">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="5bb2a-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="5bb2a-104">Microsoft Teams アプリは、ユーザーが収集、学習、作業を徐々に行うことができるように、重要な情報、共通ツール、および信頼されたプロセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="5bb2a-105">アプリは、ニーズに合わせて Teams を拡張する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="5bb2a-106">Teams で新しいものを作成するか、既存のアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5bb2a-107">ここから開始</span><span class="sxs-lookup"><span data-stu-id="5bb2a-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="5bb2a-108">Teams アプリとは</span><span class="sxs-lookup"><span data-stu-id="5bb2a-108">What are Teams apps?</span></span>

<span data-ttu-id="5bb2a-109">Teams アプリは、 [機能](concepts/capabilities-overview.md) と [エントリポイント](concepts/extensibility-points.md)の組み合わせです。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="5bb2a-110">たとえば、ユーザーは、*チャネル*(エントリポイント) のアプリの *bot* (機能) とチャットできます。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="5bb2a-111">単純な (通知を送信する) アプリもあれば、複雑なアプリ (患者レコードの管理) もあります。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="5bb2a-112">アプリを計画するときは、Teams がコラボレーションハブであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="5bb2a-113">最良の Teams アプリを使用すると、ユーザーが自分を表現し、連携しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="5bb2a-114">タブ</span><span class="sxs-lookup"><span data-stu-id="5bb2a-114">Tabs</span></span>

<span data-ttu-id="5bb2a-115">**情報をさら** にわかりやすくする: 必要な場合にのみ、簡単に情報を見つけられるようにしましょう。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="5bb2a-116">重要な web ページを [タブ](tabs/what-are-tabs.md)で表示します。これにより、チーム内の静的および動的なコンテンツについて全画面 web を利用できます。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでタブがどのように表示されるかを概念として表します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="5bb2a-118">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="5bb2a-118">Messaging extensions</span></span>

<span data-ttu-id="5bb2a-119">マルチ **タスクを簡単にする**:[メッセージング拡張機能](messaging-extensions/what-are-messaging-extensions.md)を使用すると、会話で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-119">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="5bb2a-120">また、メッセージを操作することもできます。これには、チャネル投稿の内容に基づくヘルプチケットの作成などがあります。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-120">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでメッセージング拡張機能がどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="5bb2a-122">ボット</span><span class="sxs-lookup"><span data-stu-id="5bb2a-122">Bots</span></span>

<span data-ttu-id="5bb2a-123">**単語をアクションにする**: 会話では、多くの場合、何らかの処理が必要になります (注文を生成し、自分のコードを確認し、チケットの状態を確認するなど)。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-123">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="5bb2a-124">[Bot](bots/what-are-bots.md)は、Teams 内でこれらの種類のワークフローを直接開始できます。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-124">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでボットがどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="5bb2a-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="5bb2a-126">Webhooks</span></span>

<span data-ttu-id="5bb2a-127">**外部アプリと通信** する: [受信 web フック](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) は、別のアプリから Teams チャネルに通知を自動的に送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="5bb2a-128">送信用の [webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)を使用して、web サービスに @mention のメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでどのコネクタが表示されるかを概念として表します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="5bb2a-130">Teams の Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="5bb2a-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="5bb2a-131">**Teams データを利用** する: [Microsoft Graph API for teams](https://docs.microsoft.com/graph/teams-concept-overview) は、teams、チャネル、ユーザー、およびメッセージに関する情報へのアクセスを提供します。これは、アプリの機能を作成または拡張するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Teams 用の Microsoft Graph API の概念図。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="5bb2a-133">作業の開始</span><span class="sxs-lookup"><span data-stu-id="5bb2a-133">Get started</span></span>

<span data-ttu-id="5bb2a-134">最初のアプリチュートリアルですぐにジャンプするか、既存のアプリを統合してインポートする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-134">Jump right in with our first app tutorials or find out how to integrate and import existing apps.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="5bb2a-135">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="5bb2a-135">Start building</span></span>

   <span data-ttu-id="5bb2a-136">シンプルなアプリを作成し、一般的に使用される機能を追加することで、Teams の構築にすばやく慣れることができます。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-136">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="5bb2a-137">今すぐ最初のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="5bb2a-137">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="5bb2a-138">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="5bb2a-138">Integrate with Teams</span></span>

   <span data-ttu-id="5bb2a-139">Teams の共同作業機能を使用して、ユーザーが既存の web アプリ、サービス、またはシステムについて気に入った機能を融合します。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-139">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="5bb2a-140">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="5bb2a-140">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="5bb2a-141">少しのコードが長い</span><span class="sxs-lookup"><span data-stu-id="5bb2a-141">A little code goes a long way</span></span>

   <span data-ttu-id="5bb2a-142">魅力的な Teams アプリを構築するために専門のプログラマである必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-142">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="5bb2a-143">いくつかの低コードソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="5bb2a-143">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="5bb2a-144">低コードアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="5bb2a-144">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a><span data-ttu-id="5bb2a-145">リソース</span><span class="sxs-lookup"><span data-stu-id="5bb2a-145">Resources</span></span>

* <span data-ttu-id="5bb2a-146">[Web サイトに [Teams に共有] ボタンを追加する](concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="5bb2a-146">[Add a Share to Teams button to your website](concepts/build-and-test/share-to-teams.md)</span></span>
* <span data-ttu-id="5bb2a-147"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a></span><span class="sxs-lookup"><span data-stu-id="5bb2a-147"><a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a></span></span>
* [<span data-ttu-id="5bb2a-148">Microsoft Teams JavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="5bb2a-148">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="5bb2a-149">[JavaScript のボット FRAMEWORK sdk](https://github.com/Microsoft/botbuilder-js)および[bot framework sdk (.net](https://github.com/Microsoft/botbuilder-dotnet/) )</span><span class="sxs-lookup"><span data-stu-id="5bb2a-149">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="5bb2a-150">アプリを組織または AppSource に発行する</span><span class="sxs-lookup"><span data-stu-id="5bb2a-150">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
