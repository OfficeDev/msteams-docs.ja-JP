---
title: Microsoft Teams プラットフォーム用のアプリを構築する
author: heath-hamilton
description: 開発者がカスタム アプリでMicrosoft Teams機能を拡張する方法の概要を説明します。
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 8724b669476b11aa8cb1aca6d9586fc7ea42587d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566510"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="1b208-103">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="1b208-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="1b208-104">Microsoft Teamsアプリは、重要な情報、共通のツール、信頼できるプロセスを、人々がますます集まり、学び、働く場所に提供します。</span><span class="sxs-lookup"><span data-stu-id="1b208-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="1b208-105">アプリは、ニーズに合わせてTeamsを拡張する方法です。</span><span class="sxs-lookup"><span data-stu-id="1b208-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="1b208-106">Teamsのために何か新しいものを作成するか、既存のアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="1b208-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b208-107">ここから開始</span><span class="sxs-lookup"><span data-stu-id="1b208-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="1b208-108">Teamsアプリとは何ですか?</span><span class="sxs-lookup"><span data-stu-id="1b208-108">What are Teams apps?</span></span>

<span data-ttu-id="1b208-109">Teamsアプリは[、機能](concepts/capabilities-overview.md)と[エントリ ポイント](concepts/extensibility-points.md)の組み合わせです。</span><span class="sxs-lookup"><span data-stu-id="1b208-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="1b208-110">たとえば、*チャンネル*(エントリ ポイント) でアプリの *ボット*(機能) とチャットできます。</span><span class="sxs-lookup"><span data-stu-id="1b208-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="1b208-111">アプリの中には単純なもの(通知を送信する)、複雑なアプリ(患者レコードの管理)があります。</span><span class="sxs-lookup"><span data-stu-id="1b208-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="1b208-112">アプリを計画する際は、Teamsがコラボレーション ハブであることを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="1b208-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="1b208-113">最高のTeamsアプリは、人々が自分自身を表現し、より良い一緒に働くのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="1b208-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="1b208-114">タブ</span><span class="sxs-lookup"><span data-stu-id="1b208-114">Tabs</span></span>

<span data-ttu-id="1b208-115">**情報をより便利に入手** する : 見つけやすい情報を得る必要がある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="1b208-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="1b208-116">[タブ](tabs/what-are-tabs.md)に重要な Web ページを表示すると、Teamsで静的コンテンツと動的コンテンツのフルスクリーン Web エクスペリエンスが提供されます。</span><span class="sxs-lookup"><span data-stu-id="1b208-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでのタブの外観の概念図。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="1b208-118">ボット</span><span class="sxs-lookup"><span data-stu-id="1b208-118">Bots</span></span>

<span data-ttu-id="1b208-119">**単語をアクションに変換する**: 会話は、多くの場合、何かをする必要があります (注文を生成する、コードを確認する、チケットの状態を確認するなど)。</span><span class="sxs-lookup"><span data-stu-id="1b208-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="1b208-120">[ボット](bots/what-are-bots.md)は、Teamsの内部でこのようなワークフローを開始できます。</span><span class="sxs-lookup"><span data-stu-id="1b208-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでのボットの外観の概念図。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="1b208-122">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1b208-122">Messaging extensions</span></span>

<span data-ttu-id="1b208-123">**マルチタスクを簡単に** する : [メッセージング拡張機能](messaging-extensions/what-are-messaging-extensions.md)を使用すると、会話内の外部情報を素早く共有できます。</span><span class="sxs-lookup"><span data-stu-id="1b208-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="1b208-124">また、チャネル投稿の内容に基づいてヘルプチケットを作成するなど、メッセージに対して行動することもできます。</span><span class="sxs-lookup"><span data-stu-id="1b208-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでのメッセージング拡張機能の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="1b208-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="1b208-126">Webhooks</span></span>

<span data-ttu-id="1b208-127">**外部アプリとの通信**:[受信 webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)は、別のアプリからTeams チャネルに通知を自動的に送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="1b208-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="1b208-128">[送信 Webhook を使用して、web](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)サービスに@mentionをメッセージします。</span><span class="sxs-lookup"><span data-stu-id="1b208-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでコネクタがどのような外観を持つのかを概念的に表します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="1b208-130">マイクロソフトのTeams Graph</span><span class="sxs-lookup"><span data-stu-id="1b208-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="1b208-131">**Teamsデータを利用** する : [Teams用の Microsoft Graph API](/graph/teams-concept-overview)は、アプリの機能を作成または強化するのに役立つチーム、チャネル、ユーザー、およびメッセージに関する情報にアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="1b208-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Teams用のマイクロソフト Graph API の概念図。" border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="1b208-133">建物の開始</span><span class="sxs-lookup"><span data-stu-id="1b208-133">Start building</span></span>

<span data-ttu-id="1b208-134">環境をセットアップし、簡単なアプリを作成することで、Teams用の構築にすぐに慣れ親しみます。</span><span class="sxs-lookup"><span data-stu-id="1b208-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b208-135">初めてのアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="1b208-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="1b208-136">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="1b208-136">Integrate with Teams</span></span>

<span data-ttu-id="1b208-137">既存の Web アプリ、サービス、またはシステムに関してユーザーが愛する機能と、Teamsのコラボレーション機能を組み合わせます。</span><span class="sxs-lookup"><span data-stu-id="1b208-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b208-138">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="1b208-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="1b208-139">小さなコードは長い道のりを行く</span><span class="sxs-lookup"><span data-stu-id="1b208-139">A little code goes a long way</span></span>

<span data-ttu-id="1b208-140">優れたTeamsアプリを構築するために、エキスパートプログラマーである必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1b208-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="1b208-141">いくつかの低コード ソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="1b208-141">Try one of the several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b208-142">低コード アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="1b208-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="1b208-143">アプリのアイデアを入手する</span><span class="sxs-lookup"><span data-stu-id="1b208-143">Get ideas for your app</span></span>

<span data-ttu-id="1b208-144">アプリ開発のインスピレーションをお探しですか?</span><span class="sxs-lookup"><span data-stu-id="1b208-144">Looking for app development inspiration?</span></span> <span data-ttu-id="1b208-145">忠実度の高い概念モックを使用して、実世界のシナリオと業界ソリューションのリストを参照して、アプリがユーザーに役立つさまざまな方法Teams理解してください。</span><span class="sxs-lookup"><span data-stu-id="1b208-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b208-146">アプリのシナリオを見る</span><span class="sxs-lookup"><span data-stu-id="1b208-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="1b208-147">関連項目</span><span class="sxs-lookup"><span data-stu-id="1b208-147">See also</span></span>

* [<span data-ttu-id="1b208-148">ウェブサイトに共有Teamsボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="1b208-148">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="1b208-149">Teams アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="1b208-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="1b208-150">Microsoft Teamsクライアント SDK</span><span class="sxs-lookup"><span data-stu-id="1b208-150">Microsoft Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="1b208-151">ボット フレームワーク SDK 用 [JavaScript](https://github.com/Microsoft/botbuilder-js) および [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span><span class="sxs-lookup"><span data-stu-id="1b208-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="1b208-152">Teams アプリを配布する</span><span class="sxs-lookup"><span data-stu-id="1b208-152">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
