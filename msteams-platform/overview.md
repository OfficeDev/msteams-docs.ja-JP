---
title: Microsoft Teams プラットフォーム用のアプリをビルドする
author: heath-hamilton
description: 開発者がカスタム アプリを使用して Microsoft Teams の機能を拡張する方法の概要を確認します。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: b4f5d5fa3014d2acc5e4178a89c84ddb5a250132
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596211"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="c7c59-103">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="c7c59-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="c7c59-104">Microsoft Teams アプリは、重要な情報、一般的なツール、信頼できるプロセスを、ユーザーがますます収集、学習、作業する場所に提供します。</span><span class="sxs-lookup"><span data-stu-id="c7c59-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="c7c59-105">アプリは、ニーズに合わせて Teams を拡張する方法です。</span><span class="sxs-lookup"><span data-stu-id="c7c59-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="c7c59-106">Teams 用に新しいアプリを作成するか、既存のアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="c7c59-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c59-107">ここから開始</span><span class="sxs-lookup"><span data-stu-id="c7c59-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="c7c59-108">Teams アプリとは</span><span class="sxs-lookup"><span data-stu-id="c7c59-108">What are Teams apps?</span></span>

<span data-ttu-id="c7c59-109">Teams アプリは、機能とエントリ[ポイントの組み](concepts/capabilities-overview.md)[合わせです](concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="c7c59-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="c7c59-110">たとえば、ユーザーはチャネル *(エントリ* ポイント) でアプリのボット(機能) とチャットできます。</span><span class="sxs-lookup"><span data-stu-id="c7c59-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="c7c59-111">一部のアプリは単純 (通知の送信) ですが、複雑なアプリもあります (患者レコードの管理)。</span><span class="sxs-lookup"><span data-stu-id="c7c59-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="c7c59-112">アプリを計画する際は、Teams はコラボレーション ハブです。</span><span class="sxs-lookup"><span data-stu-id="c7c59-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="c7c59-113">最高の Teams アプリは、ユーザーが自分自身を表現し、より良い仕事を共にするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c7c59-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="c7c59-114">タブ</span><span class="sxs-lookup"><span data-stu-id="c7c59-114">Tabs</span></span>

<span data-ttu-id="c7c59-115">**情報をより便利に取得する**: 場合によっては、見つけやすくする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="c7c59-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="c7c59-116">タブに重要な Web [ページを](tabs/what-are-tabs.md)表示し、Teams の静的コンテンツと動的コンテンツのフルスクリーン Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="c7c59-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでのタブの外観の概念的表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="c7c59-118">ボット</span><span class="sxs-lookup"><span data-stu-id="c7c59-118">Bots</span></span>

<span data-ttu-id="c7c59-119">**単語をアクションに** 変換する: 会話は、多くの場合、何かをする必要があります (注文の生成、コードの確認、チケットの状態の確認など)。</span><span class="sxs-lookup"><span data-stu-id="c7c59-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="c7c59-120">ボット [は、Teams](bots/what-are-bots.md) の内部でこれらの種類のワークフローを開始できます。</span><span class="sxs-lookup"><span data-stu-id="c7c59-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでのボットの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="c7c59-122">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="c7c59-122">Messaging extensions</span></span>

<span data-ttu-id="c7c59-123">**マルチタスクを容易にする**: メッセージング拡張機能 [を](messaging-extensions/what-are-messaging-extensions.md)使用すると、会話で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="c7c59-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="c7c59-124">また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理できます。</span><span class="sxs-lookup"><span data-stu-id="c7c59-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでのメッセージング拡張機能の外観の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="c7c59-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="c7c59-126">Webhooks</span></span>

<span data-ttu-id="c7c59-127">**外部アプリと通信** する : [受信 Webhooks は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 、別のアプリから Teams チャネルに通知を自動的に送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="c7c59-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="c7c59-128">送信 [Webhooks を使用して](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)、Web サービスにメッセージを送信@mention。</span><span class="sxs-lookup"><span data-stu-id="c7c59-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでのコネクタの外観の概念的表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="c7c59-130">Microsoft Graph for Teams</span><span class="sxs-lookup"><span data-stu-id="c7c59-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="c7c59-131">**Teams データの利用**: [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) では、アプリの機能の作成や強化に役立つチーム、チャネル、ユーザー、メッセージに関する情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c7c59-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API for Teams の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="c7c59-133">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="c7c59-133">Start building</span></span>

<span data-ttu-id="c7c59-134">環境をセットアップし、簡単なアプリを作成することで、Teams の構築についてすぐに理解できます。</span><span class="sxs-lookup"><span data-stu-id="c7c59-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c59-135">初めてのアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="c7c59-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="c7c59-136">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="c7c59-136">Integrate with Teams</span></span>

<span data-ttu-id="c7c59-137">既存の Web アプリ、サービス、またはシステムに関するユーザーが気に入る機能と、Teams の共同作業機能をブレンドします。</span><span class="sxs-lookup"><span data-stu-id="c7c59-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c59-138">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="c7c59-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="c7c59-139">小さなコードは長い道のりを行く</span><span class="sxs-lookup"><span data-stu-id="c7c59-139">A little code goes a long way</span></span>

<span data-ttu-id="c7c59-140">素晴らしい Teams アプリを構築するために、エキスパート プログラマである必要はなんらない。</span><span class="sxs-lookup"><span data-stu-id="c7c59-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="c7c59-141">いくつかの低コードソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="c7c59-141">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c59-142">低コード アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="c7c59-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="c7c59-143">アプリのアイデアを取得する</span><span class="sxs-lookup"><span data-stu-id="c7c59-143">Get ideas for your app</span></span>

<span data-ttu-id="c7c59-144">アプリ開発のインスピレーションをお探しですか?</span><span class="sxs-lookup"><span data-stu-id="c7c59-144">Looking for app development inspiration?</span></span> <span data-ttu-id="c7c59-145">高忠実度の概念モックを使用して、実際のシナリオと業界ソリューションのリストを参照して、Teams アプリがユーザーに役立つさまざまな方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="c7c59-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c59-146">アプリのシナリオを見る</span><span class="sxs-lookup"><span data-stu-id="c7c59-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="c7c59-147">関連項目</span><span class="sxs-lookup"><span data-stu-id="c7c59-147">See also</span></span>

* [<span data-ttu-id="c7c59-148">Share-to-Teams ボタンを Web サイトに追加する</span><span class="sxs-lookup"><span data-stu-id="c7c59-148">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="c7c59-149">Teams アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="c7c59-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="c7c59-150">Microsoft Teams JavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="c7c59-150">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="c7c59-151">JavaScript および[.NET](https://github.com/Microsoft/botbuilder-dotnet/)用[ボット フレームワーク](https://github.com/Microsoft/botbuilder-js)SDK</span><span class="sxs-lookup"><span data-stu-id="c7c59-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="c7c59-152">Teams アプリを発行する</span><span class="sxs-lookup"><span data-stu-id="c7c59-152">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
