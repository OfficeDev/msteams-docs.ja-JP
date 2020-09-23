---
title: Microsoft Teams プラットフォーム用のアプリを構築する
author: heath-hamilton
description: 開発者がカスタムアプリを使用して Microsoft Teams の機能を拡張およびカスタマイズする方法の概要。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: c430add71e7c23a44a552270c5e3c1bacbe650e4
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209800"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="acc1f-103">Microsoft Teams のアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="acc1f-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="acc1f-104">Microsoft Teams アプリは、ユーザーが収集、学習、作業を徐々に行うことができるように、重要な情報、共通ツール、および信頼されたプロセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="acc1f-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="acc1f-105">アプリは、ニーズに合わせて Teams を拡張する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="acc1f-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="acc1f-106">Teams で新しいものを作成するか、既存のアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="acc1f-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="acc1f-107">Teams アプリとは</span><span class="sxs-lookup"><span data-stu-id="acc1f-107">What are Teams apps?</span></span>

<span data-ttu-id="acc1f-108">Teams アプリは、 [機能](concepts/capabilities-overview.md) と [エントリポイント](concepts/extensibility-points.md)の組み合わせです。</span><span class="sxs-lookup"><span data-stu-id="acc1f-108">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="acc1f-109">たとえば、ユーザーは、*チャネル*(エントリポイント) のアプリの*bot* (機能) とチャットできます。</span><span class="sxs-lookup"><span data-stu-id="acc1f-109">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="acc1f-110">単純な (通知を送信する) アプリもあれば、複雑なアプリ (患者レコードの管理) もあります。</span><span class="sxs-lookup"><span data-stu-id="acc1f-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="acc1f-111">アプリを計画するときは、Teams がコラボレーションハブであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="acc1f-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="acc1f-112">最良の Teams アプリを使用すると、ユーザーが自分を表現し、連携しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="acc1f-112">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="acc1f-113">タブ</span><span class="sxs-lookup"><span data-stu-id="acc1f-113">Tabs</span></span>

<span data-ttu-id="acc1f-114">**情報をさら**にわかりやすくする: 必要な場合にのみ、簡単に情報を見つけられるようにしましょう。</span><span class="sxs-lookup"><span data-stu-id="acc1f-114">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="acc1f-115">重要な web ページを [タブ](tabs/what-are-tabs.md)で表示します。これにより、チーム内の静的および動的なコンテンツについて全画面 web を利用できます。</span><span class="sxs-lookup"><span data-stu-id="acc1f-115">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでタブがどのように表示されるかを概念として表します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="acc1f-117">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="acc1f-117">Messaging extensions</span></span>

<span data-ttu-id="acc1f-118">マルチ**タスクを簡単にする**:[メッセージング拡張機能](messaging-extensions/what-are-messaging-extensions.md)を使用すると、会話で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="acc1f-118">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="acc1f-119">また、メッセージを操作することもできます。これには、チャネル投稿の内容に基づくヘルプチケットの作成などがあります。</span><span class="sxs-lookup"><span data-stu-id="acc1f-119">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでメッセージング拡張機能がどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="acc1f-121">ボット</span><span class="sxs-lookup"><span data-stu-id="acc1f-121">Bots</span></span>

<span data-ttu-id="acc1f-122">**単語をアクションにする**: 会話では、多くの場合、何らかの処理が必要になります (注文を生成し、自分のコードを確認し、チケットの状態を確認するなど)。</span><span class="sxs-lookup"><span data-stu-id="acc1f-122">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="acc1f-123">[Bot](bots/what-are-bots.md)は、Teams 内でこれらの種類のワークフローを直接開始できます。</span><span class="sxs-lookup"><span data-stu-id="acc1f-123">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでボットがどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="acc1f-125">Webhook</span><span class="sxs-lookup"><span data-stu-id="acc1f-125">Webhooks</span></span>

<span data-ttu-id="acc1f-126">**外部アプリと通信**する: [受信 web フック](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) は、別のアプリから Teams チャネルに通知を自動的に送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="acc1f-126">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="acc1f-127">送信用の [webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)を使用して、web サービスに @mention のメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="acc1f-127">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでどのコネクタが表示されるかを概念として表します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="acc1f-129">Teams の Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="acc1f-129">Microsoft Graph for Teams</span></span>

<span data-ttu-id="acc1f-130">**Teams データを利用**する: [Microsoft Graph API for teams](https://docs.microsoft.com/graph/teams-concept-overview) は、teams、チャネル、ユーザー、およびメッセージに関する情報へのアクセスを提供します。これは、アプリの機能を作成または拡張するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="acc1f-130">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Teams 用の Microsoft Graph API の概念図。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="acc1f-132">概要</span><span class="sxs-lookup"><span data-stu-id="acc1f-132">Get started</span></span>

<span data-ttu-id="acc1f-133">最初のアプリチュートリアルですぐにジャンプするか、既存のアプリを統合してインポートする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="acc1f-133">Jump right in with our first app tutorials or find out how to integrate and import existing apps.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="acc1f-134">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="acc1f-134">Start building</span></span>

   <span data-ttu-id="acc1f-135">シンプルなアプリを作成し、一般的に使用される機能を追加することで、Teams の構築にすばやく慣れることができます。</span><span class="sxs-lookup"><span data-stu-id="acc1f-135">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="acc1f-136">今すぐ最初のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="acc1f-136">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="acc1f-137">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="acc1f-137">Integrate with Teams</span></span>

   <span data-ttu-id="acc1f-138">Teams の共同作業機能を使用して、ユーザーが既存の web アプリ、サービス、またはシステムについて気に入った機能を融合します。</span><span class="sxs-lookup"><span data-stu-id="acc1f-138">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="acc1f-139">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="acc1f-139">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="acc1f-140">少しのコードが長い</span><span class="sxs-lookup"><span data-stu-id="acc1f-140">A little code goes a long way</span></span>

   <span data-ttu-id="acc1f-141">魅力的な Teams アプリを構築するために専門のプログラマである必要はありません。</span><span class="sxs-lookup"><span data-stu-id="acc1f-141">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="acc1f-142">いくつかの低コードソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="acc1f-142">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="acc1f-143">低コードアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="acc1f-143">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a><span data-ttu-id="acc1f-144">リソース</span><span class="sxs-lookup"><span data-stu-id="acc1f-144">Resources</span></span>

* <span data-ttu-id="acc1f-145">[Web サイトに [Teams に共有] ボタンを追加する](concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="acc1f-145">[Add a Share to Teams button to your website](concepts/build-and-test/share-to-teams.md)</span></span>
* [<span data-ttu-id="acc1f-146">Fluent デザインシステム</span><span class="sxs-lookup"><span data-stu-id="acc1f-146">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="acc1f-147">Microsoft Teams JavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="acc1f-147">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="acc1f-148">[JavaScript のボット FRAMEWORK sdk](https://github.com/Microsoft/botbuilder-js)および[bot framework sdk (.net](https://github.com/Microsoft/botbuilder-dotnet/) )</span><span class="sxs-lookup"><span data-stu-id="acc1f-148">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="acc1f-149">アプリを組織または AppSource に発行する</span><span class="sxs-lookup"><span data-stu-id="acc1f-149">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
