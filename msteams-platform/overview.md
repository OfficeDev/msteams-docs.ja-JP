---
title: Microsoft Teams プラットフォーム用のアプリをビルドする
author: heath-hamilton
description: 開発者がカスタム アプリを使用して Microsoft Teams の機能を拡張する方法の概要を確認します。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e40d2b0d8b0d12e6275b97f79d103310d22f9720
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475929"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="0a591-103">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="0a591-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="0a591-104">Microsoft Teams アプリは、重要な情報、一般的なツール、信頼できるプロセスを、ユーザーがますます収集、学習、作業する場所に提供します。</span><span class="sxs-lookup"><span data-stu-id="0a591-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="0a591-105">アプリは、ニーズに合わせて Teams を拡張する方法です。</span><span class="sxs-lookup"><span data-stu-id="0a591-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="0a591-106">Teams 用に新しいアプリを作成するか、既存のアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="0a591-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a591-107">ここから開始</span><span class="sxs-lookup"><span data-stu-id="0a591-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="0a591-108">Teams アプリとは</span><span class="sxs-lookup"><span data-stu-id="0a591-108">What are Teams apps?</span></span>

<span data-ttu-id="0a591-109">Teams アプリは、機能とエントリ[ポイントの組み](concepts/capabilities-overview.md)[合わせです](concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="0a591-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="0a591-110">たとえば、ユーザーはチャネル *(エントリ* ポイント) でアプリのボット(機能) とチャットできます。</span><span class="sxs-lookup"><span data-stu-id="0a591-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="0a591-111">一部のアプリは単純 (通知の送信) ですが、複雑なアプリもあります (患者レコードの管理)。</span><span class="sxs-lookup"><span data-stu-id="0a591-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="0a591-112">アプリを計画する際は、Teams はコラボレーション ハブです。</span><span class="sxs-lookup"><span data-stu-id="0a591-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="0a591-113">最高の Teams アプリは、ユーザーが自分自身を表現し、より良い仕事を共にするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0a591-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="0a591-114">タブ</span><span class="sxs-lookup"><span data-stu-id="0a591-114">Tabs</span></span>

<span data-ttu-id="0a591-115">**情報をより便利に取得する**: 場合によっては、見つけやすくする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="0a591-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="0a591-116">タブに重要な Web [ページを](tabs/what-are-tabs.md)表示し、Teams の静的コンテンツと動的コンテンツのフルスクリーン Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="0a591-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでのタブの外観の概念的表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="0a591-118">ボット</span><span class="sxs-lookup"><span data-stu-id="0a591-118">Bots</span></span>

<span data-ttu-id="0a591-119">**単語をアクションに** 変換する: 会話は、多くの場合、何かをする必要があります (注文の生成、コードの確認、チケットの状態の確認など)。</span><span class="sxs-lookup"><span data-stu-id="0a591-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="0a591-120">ボット [は、Teams](bots/what-are-bots.md) の内部でこれらの種類のワークフローを開始できます。</span><span class="sxs-lookup"><span data-stu-id="0a591-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでのボットの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="0a591-122">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="0a591-122">Messaging extensions</span></span>

<span data-ttu-id="0a591-123">**マルチタスクを容易にする**: メッセージング拡張機能 [を](messaging-extensions/what-are-messaging-extensions.md)使用すると、会話で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="0a591-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="0a591-124">また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理できます。</span><span class="sxs-lookup"><span data-stu-id="0a591-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでのメッセージング拡張機能の外観の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="0a591-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="0a591-126">Webhooks</span></span>

<span data-ttu-id="0a591-127">**外部アプリと通信** する : [受信 Webhooks は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 、別のアプリから Teams チャネルに通知を自動的に送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="0a591-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="0a591-128">送信 [Webhooks を使用して](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)、Web サービスにメッセージを送信@mention。</span><span class="sxs-lookup"><span data-stu-id="0a591-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでのコネクタの外観の概念的表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="0a591-130">Microsoft Graph for Teams</span><span class="sxs-lookup"><span data-stu-id="0a591-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="0a591-131">**Teams データの利用**: [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) では、アプリの機能の作成や強化に役立つチーム、チャネル、ユーザー、メッセージに関する情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="0a591-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API for Teams の概念表現。" border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a><span data-ttu-id="0a591-133">Microsoft Teams アプリのソリューションを構築する</span><span class="sxs-lookup"><span data-stu-id="0a591-133">Build solutions for Microsoft Teams apps</span></span>
 
<span data-ttu-id="0a591-134">Microsoft は、業界別に整理された Teams アプリのシナリオ ライブラリである拡張性の外観ブックを提供しています。</span><span class="sxs-lookup"><span data-stu-id="0a591-134">Microsoft offers an extensibility look book, a scenario library for Teams apps organized by industry.</span></span> <span data-ttu-id="0a591-135">このブックは、Teams プラットフォームでアプリを構築し、さまざまな Teams プラットフォーム機能を使用してさまざまなシナリオを理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0a591-135">This book helps you build apps on the Teams platform and understand different possible scenarios using various Teams platform capabilities.</span></span> <span data-ttu-id="0a591-136">ルック ブックのシナリオは、ビジネス上の問題、課題に関連するペルサから始め、ビジネス ニーズに対応する Teams アプリ ソリューションで終了します。</span><span class="sxs-lookup"><span data-stu-id="0a591-136">The look book scenarios start with a business problem, the personas involved along with their challenges, and end with a Teams app solution addressing the business needs.</span></span>

<span data-ttu-id="0a591-137">このライブラリの各シナリオには、一連の忠実度の高いデザイン概念モックが伴います。これは、アプリを設計し、ユーザー エクスペリエンスを向上させるインスピレーションとして役立つ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0a591-137">Each scenario in this library is accompanied by a set of high-fidelity design concept mocks, which can serve as an inspiration for designing your apps and enhancing user experience.</span></span> <span data-ttu-id="0a591-138">さらに、このルック ブックでは、各アプリの構築に続く設計とアーキテクチャのベスト プラクティスが強調表示されています。</span><span class="sxs-lookup"><span data-stu-id="0a591-138">In addition, the look book highlights the design and architecture best practices followed in building each app.</span></span> <span data-ttu-id="0a591-139">詳細については、「機能拡張の一覧」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0a591-139">For more information, see the extensibility look book.</span></span> <span data-ttu-id="0a591-140">詳細については、「機能拡張 [ルック ブック」を参照してください](https://adoption.microsoft.com/extensibility-look-book/scenarios/)。</span><span class="sxs-lookup"><span data-stu-id="0a591-140">For more information, see [extensibility look book](https://adoption.microsoft.com/extensibility-look-book/scenarios/).</span></span> 

## <a name="start-building"></a><span data-ttu-id="0a591-141">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="0a591-141">Start building</span></span>

<span data-ttu-id="0a591-142">簡単なアプリを作成し、一般的に使用される機能を追加することで、Teams の構築についてすぐに理解できます。</span><span class="sxs-lookup"><span data-stu-id="0a591-142">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a591-143">最初のアプリを今すぐビルドする</span><span class="sxs-lookup"><span data-stu-id="0a591-143">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="0a591-144">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="0a591-144">Integrate with Teams</span></span>

<span data-ttu-id="0a591-145">既存の Web アプリ、サービス、またはシステムに関するユーザーが気に入る機能と、Teams の共同作業機能をブレンドします。</span><span class="sxs-lookup"><span data-stu-id="0a591-145">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a591-146">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="0a591-146">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="0a591-147">小さなコードは長い道のりを行く</span><span class="sxs-lookup"><span data-stu-id="0a591-147">A little code goes a long way</span></span>

<span data-ttu-id="0a591-148">素晴らしい Teams アプリを構築するために、エキスパート プログラマである必要はなんらない。</span><span class="sxs-lookup"><span data-stu-id="0a591-148">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="0a591-149">いくつかの低コードソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="0a591-149">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a591-150">低コード アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="0a591-150">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="0a591-151">関連情報</span><span class="sxs-lookup"><span data-stu-id="0a591-151">Resources</span></span>

* [<span data-ttu-id="0a591-152">Share-to-Teams ボタンを Web サイトに追加する</span><span class="sxs-lookup"><span data-stu-id="0a591-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="0a591-153">Teams アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="0a591-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="0a591-154">Microsoft Teams JavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="0a591-154">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="0a591-155">JavaScript および[.NET](https://github.com/Microsoft/botbuilder-dotnet/)用[ボット フレームワーク](https://github.com/Microsoft/botbuilder-js)SDK</span><span class="sxs-lookup"><span data-stu-id="0a591-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="0a591-156">Teams アプリを発行する</span><span class="sxs-lookup"><span data-stu-id="0a591-156">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
