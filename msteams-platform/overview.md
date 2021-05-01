---
title: アプリケーション プラットフォーム用のアプリMicrosoft Teamsする
author: heath-hamilton
description: 開発者がカスタム アプリを使用して機能を拡張Microsoft Teams概要を確認します。
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 69c36cf5f925bdb9802e7ec081a7765187a06128
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101843"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="82017-103">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="82017-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="82017-104">Microsoft Teamsアプリは、重要な情報、一般的なツール、信頼できるプロセスを、人々がますます収集、学習、作業する場所に提供します。</span><span class="sxs-lookup"><span data-stu-id="82017-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="82017-105">アプリは、ニーズに合わせてTeams拡張する方法です。</span><span class="sxs-lookup"><span data-stu-id="82017-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="82017-106">新しいアプリを作成し、Teamsアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="82017-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82017-107">ここから開始</span><span class="sxs-lookup"><span data-stu-id="82017-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="82017-108">アプリとはTeamsですか?</span><span class="sxs-lookup"><span data-stu-id="82017-108">What are Teams apps?</span></span>

<span data-ttu-id="82017-109">Teamsは、機能とエントリ ポイント[の組み](concepts/capabilities-overview.md)[合わせです](concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="82017-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="82017-110">たとえば、ユーザーはチャネル *(エントリ* ポイント) でアプリのボット(機能) とチャットできます。</span><span class="sxs-lookup"><span data-stu-id="82017-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="82017-111">一部のアプリは単純 (通知の送信) ですが、複雑なアプリもあります (患者レコードの管理)。</span><span class="sxs-lookup"><span data-stu-id="82017-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="82017-112">アプリを計画する場合は、Teamsハブに注意してください。</span><span class="sxs-lookup"><span data-stu-id="82017-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="82017-113">アプリの最適Teamsは、ユーザーが自分自身を表現し、より良く一緒に作業するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="82017-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="82017-114">タブ</span><span class="sxs-lookup"><span data-stu-id="82017-114">Tabs</span></span>

<span data-ttu-id="82017-115">**情報をより便利に取得する**: 場合によっては、見つけやすくする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="82017-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="82017-116">タブに重要な Web[ページを表示](tabs/what-are-tabs.md)します。このページでは、静的コンテンツと動的コンテンツのフルスクリーン Web エクスペリエンスを提供Teams。</span><span class="sxs-lookup"><span data-stu-id="82017-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="クライアント内のタブの外観を概念Teamsします。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="82017-118">ボット</span><span class="sxs-lookup"><span data-stu-id="82017-118">Bots</span></span>

<span data-ttu-id="82017-119">**単語をアクションに** 変換する: 会話は、多くの場合、何かをする必要があります (注文の生成、コードの確認、チケットの状態の確認など)。</span><span class="sxs-lookup"><span data-stu-id="82017-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="82017-120">ボット[は、](bots/what-are-bots.md)これらの種類のワークフローをワークフローの内部で開始Teams。</span><span class="sxs-lookup"><span data-stu-id="82017-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="クライアントでのボットの外観の概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="82017-122">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="82017-122">Messaging extensions</span></span>

<span data-ttu-id="82017-123">**マルチタスクを容易にする**: メッセージング拡張機能 [を](messaging-extensions/what-are-messaging-extensions.md)使用すると、会話で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="82017-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="82017-124">また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理できます。</span><span class="sxs-lookup"><span data-stu-id="82017-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="クライアントでのメッセージング拡張機能の外観の概念Teamsします。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="82017-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="82017-126">Webhooks</span></span>

<span data-ttu-id="82017-127">**外部アプリと通信** する:[受信 Webhooks は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)、別のアプリから別のチャネルに通知を自動的に送信Teamsです。</span><span class="sxs-lookup"><span data-stu-id="82017-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="82017-128">送信 [Webhooks を使用して](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)、Web サービスにメッセージを送信@mention。</span><span class="sxs-lookup"><span data-stu-id="82017-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="クライアントでのコネクタの外観の概念Teamsします。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="82017-130">Microsoft Graph Teams</span><span class="sxs-lookup"><span data-stu-id="82017-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="82017-131">**Teams** データを利用する : [microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview)では、アプリの機能の作成や強化に役立つチーム、チャネル、ユーザー、メッセージに関する情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="82017-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API の概念Teams。" border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="82017-133">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="82017-133">Start building</span></span>

<span data-ttu-id="82017-134">環境をセットアップし、簡単なアプリTeamsを作成することで、アプリの構築にすばやく慣れ親しむ必要があります。</span><span class="sxs-lookup"><span data-stu-id="82017-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82017-135">初めてのアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="82017-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="82017-136">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="82017-136">Integrate with Teams</span></span>

<span data-ttu-id="82017-137">既存の Web アプリ、サービス、またはシステムに関するユーザーが気に入る機能と、ユーザーの共同作業機能を組み合Teams。</span><span class="sxs-lookup"><span data-stu-id="82017-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82017-138">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="82017-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="82017-139">小さなコードは長い道のりを行く</span><span class="sxs-lookup"><span data-stu-id="82017-139">A little code goes a long way</span></span>

<span data-ttu-id="82017-140">素晴らしいアプリを構築するために専門家のプログラマである必要Teams。</span><span class="sxs-lookup"><span data-stu-id="82017-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="82017-141">いくつかの低コードソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="82017-141">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82017-142">低コード アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="82017-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="82017-143">アプリのアイデアを取得する</span><span class="sxs-lookup"><span data-stu-id="82017-143">Get ideas for your app</span></span>

<span data-ttu-id="82017-144">アプリ開発のインスピレーションをお探しですか?</span><span class="sxs-lookup"><span data-stu-id="82017-144">Looking for app development inspiration?</span></span> <span data-ttu-id="82017-145">高忠実度の概念モックを使用して、実際のシナリオと業界のソリューションの一覧を参照して、アプリがユーザーに役立つさまざまなTeamsを理解します。</span><span class="sxs-lookup"><span data-stu-id="82017-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82017-146">アプリのシナリオを見る</span><span class="sxs-lookup"><span data-stu-id="82017-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="82017-147">関連項目</span><span class="sxs-lookup"><span data-stu-id="82017-147">See also</span></span>

* <span data-ttu-id="82017-148">[Web サイトに [共有Teams] ボタンを追加する](concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="82017-148">[Add a Share-to-Teams button to your website](concepts/build-and-test/share-to-teams.md)</span></span>
* [<span data-ttu-id="82017-149">アプリをTeamsする</span><span class="sxs-lookup"><span data-stu-id="82017-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="82017-150">Microsoft TeamsJavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="82017-150">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="82017-151">JavaScript および[.NET](https://github.com/Microsoft/botbuilder-dotnet/)用[ボット フレームワーク](https://github.com/Microsoft/botbuilder-js)SDK</span><span class="sxs-lookup"><span data-stu-id="82017-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="82017-152">アプリをTeamsする</span><span class="sxs-lookup"><span data-stu-id="82017-152">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
