---
title: Microsoft Teams 開発者プラットフォーム
author: clearab
description: 開発者が Teams プラットフォームを使用して Microsoft Teams の機能を拡張およびカスタマイズする方法の概要について説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 73cbd4f68d8878872147bd412972495de1b5de6e
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964572"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="bac3c-103">Microsoft Teams の構築</span><span class="sxs-lookup"><span data-stu-id="bac3c-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="bac3c-104">Microsoft Teams アプリは、ユーザーが収集、学習、作業を徐々に行うことができるように、重要な情報、共通ツール、および信頼されたプロセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="bac3c-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="bac3c-105">アプリは、ニーズに合わせて Teams を拡張する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="bac3c-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="bac3c-106">Teams で新しいものを作成するか、既存のアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="bac3c-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="bac3c-107">Teams アプリとは</span><span class="sxs-lookup"><span data-stu-id="bac3c-107">What are Teams apps?</span></span>

<span data-ttu-id="bac3c-108">ユーザーは、一連のプラットフォーム [機能](capabilities-overview.md)を通じて Teams アプリを見つけて使用します。</span><span class="sxs-lookup"><span data-stu-id="bac3c-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="bac3c-109">単純な (通知を送信する) アプリもあれば、複雑なものもあります (患者の記録の表示)。</span><span class="sxs-lookup"><span data-stu-id="bac3c-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="bac3c-110">アプリを計画するときは、Teams がコラボレーションハブであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bac3c-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="bac3c-111">最良の Teams アプリを使用すると、ユーザーが自分を表現し、連携しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="bac3c-111">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="bac3c-112">タブ</span><span class="sxs-lookup"><span data-stu-id="bac3c-112">Tabs</span></span>

<span data-ttu-id="bac3c-113">**情報をさら**にわかりやすくする: 必要な場合にのみ、簡単に情報を見つけられるようにしましょう。</span><span class="sxs-lookup"><span data-stu-id="bac3c-113">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="bac3c-114">重要な web ページを [タブ](../tabs/what-are-tabs.md)で表示します。これにより、チーム内の静的および動的なコンテンツについて全画面 web を利用できます。</span><span class="sxs-lookup"><span data-stu-id="bac3c-114">Display an important webpage in a [tab](../tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="doc-links/images/overview-tabs.png" alt-text="Teams クライアントでタブがどのように表示されるかを概念として表します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="bac3c-116">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="bac3c-116">Messaging extensions</span></span>

<span data-ttu-id="bac3c-117">マルチ**タスクを簡単にする**:[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)を使用すると、会話で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="bac3c-117">**Make it easier to multitask**: With [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="bac3c-118">また、メッセージを操作することもできます。これには、チャネル投稿の内容に基づくヘルプチケットの作成などがあります。</span><span class="sxs-lookup"><span data-stu-id="bac3c-118">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="doc-links/images/overview-messaging.png" alt-text="Teams クライアントでメッセージング拡張機能がどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="bac3c-120">ボット</span><span class="sxs-lookup"><span data-stu-id="bac3c-120">Bots</span></span>

<span data-ttu-id="bac3c-121">**単語をアクションにする**: 会話では、多くの場合、何らかの処理が必要になります (注文を生成し、自分のコードを確認し、チケットの状態を確認するなど)。</span><span class="sxs-lookup"><span data-stu-id="bac3c-121">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="bac3c-122">[Bot](../bots/what-are-bots.md)は、Teams 内でこれらの種類のワークフローを直接開始できます。</span><span class="sxs-lookup"><span data-stu-id="bac3c-122">A [bot](../bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="doc-links/images/overview-bots.png" alt-text="Teams クライアントでボットがどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="bac3c-124">Webhook</span><span class="sxs-lookup"><span data-stu-id="bac3c-124">Webhooks</span></span>

<span data-ttu-id="bac3c-125">**外部アプリと通信**する: [受信 web フック](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) は、別のアプリから Teams チャネルに通知を自動的に送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="bac3c-125">**Communicate with external apps**: [Incoming webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="bac3c-126">送信用の [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)を使用して、web サービスに @mention のメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="bac3c-126">With [outgoing webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="doc-links/images/overview-connectors.png" alt-text="Teams クライアントでどのコネクタが表示されるかを概念として表します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="bac3c-128">Teams の Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="bac3c-128">Microsoft Graph for Teams</span></span>

<span data-ttu-id="bac3c-129">**Teams データを利用**する: [MICROSOFT Graph REST API for teams](https://docs.microsoft.com/graph/teams-concept-overview) は、teams、チャネル、ユーザー、およびメッセージに関する情報へのアクセスを提供し、アプリの機能を作成または拡張するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="bac3c-129">**Utilize Teams data**: The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="doc-links/images/overview-graph.png" alt-text="Teams の Microsoft Graph REST API の概念図。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="bac3c-131">作業の開始</span><span class="sxs-lookup"><span data-stu-id="bac3c-131">Get started</span></span>

<span data-ttu-id="bac3c-132">「最初のアプリのチュートリアル」では、既存のアプリを統合およびインポートする方法や、Teams アプリ開発ライフサイクルについて学ぶための時間を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="bac3c-132">Jump right in with our first app tutorials, find out how to integrate and import existing apps, or take your time to learn about the Teams app development lifecycle.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="bac3c-133">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="bac3c-133">Start building</span></span>

   <span data-ttu-id="bac3c-134">シンプルなアプリを作成し、一般的に使用される機能を追加することで、Teams の構築にすばやく慣れることができます。</span><span class="sxs-lookup"><span data-stu-id="bac3c-134">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="bac3c-135">今すぐ最初のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="bac3c-135">Build your first app now</span></span>](build-your-first-app/building-real-world-app.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="bac3c-136">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="bac3c-136">Integrate with Teams</span></span>

   <span data-ttu-id="bac3c-137">Teams の共同作業機能を使用して、ユーザーが既存の web アプリ、サービス、またはシステムについて気に入った機能を融合します。</span><span class="sxs-lookup"><span data-stu-id="bac3c-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="bac3c-138">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="bac3c-138">Integrate an existing app</span></span>](migrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="bac3c-139">少しのコードが長い</span><span class="sxs-lookup"><span data-stu-id="bac3c-139">A little code goes a long way</span></span>

   <span data-ttu-id="bac3c-140">魅力的な Teams アプリを構築するために専門のプログラマである必要はありません。</span><span class="sxs-lookup"><span data-stu-id="bac3c-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="bac3c-141">いくつかの低コードソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="bac3c-141">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="bac3c-142">低コードアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="bac3c-142">Create a low-code app</span></span>](low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="trust-the-process"></a><span data-ttu-id="bac3c-143">プロセスを信頼する</span><span class="sxs-lookup"><span data-stu-id="bac3c-143">Trust the process</span></span>

   <span data-ttu-id="bac3c-144">Teams プラットフォーム開発プロセス全体を調べて、組織または他のユーザーのためにアプリを効果的に計画、設計、構築、および発行します。</span><span class="sxs-lookup"><span data-stu-id="bac3c-144">Learn the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="bac3c-145">アプリの計画を開始する</span><span class="sxs-lookup"><span data-stu-id="bac3c-145">Start planning your app</span></span>](../concepts/extensibility-points.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="bac3c-146">リソース</span><span class="sxs-lookup"><span data-stu-id="bac3c-146">Resources</span></span>

* <span data-ttu-id="bac3c-147">[Web サイトに [Teams に共有] ボタンを追加する](../concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="bac3c-147">[Add a Share to Teams button to your website](../concepts/build-and-test/share-to-teams.md)</span></span>
* [<span data-ttu-id="bac3c-148">Fluent デザインシステム</span><span class="sxs-lookup"><span data-stu-id="bac3c-148">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="bac3c-149">Microsoft Teams JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="bac3c-149">Microsoft Teams JavaScript SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="bac3c-150">[JavaScript のボット FRAMEWORK sdk](https://github.com/Microsoft/botbuilder-js)および[bot framework sdk (.net](https://github.com/Microsoft/botbuilder-dotnet/) )</span><span class="sxs-lookup"><span data-stu-id="bac3c-150">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="bac3c-151">アプリを組織または AppSource に発行する</span><span class="sxs-lookup"><span data-stu-id="bac3c-151">Publish your app to an organization or AppSource</span></span>](../concepts/deploy-and-publish/overview.md)
