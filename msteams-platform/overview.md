---
title: アプリケーション プラットフォーム用のアプリMicrosoft Teamsする
author: heath-hamilton
description: 開発者がカスタム アプリを使用して機能を拡張Microsoft Teams概要を確認します。
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 796353a4c556794a518a451e8a45989351729eb9
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646524"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="7fab2-103">Microsoft Teams のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="7fab2-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="7fab2-104">Microsoft Teamsアプリは、重要な情報、一般的なツール、信頼できるプロセスを、人々がますます収集、学習、作業する場所に提供します。</span><span class="sxs-lookup"><span data-stu-id="7fab2-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="7fab2-105">アプリは、ニーズに合わせてTeams拡張する方法です。</span><span class="sxs-lookup"><span data-stu-id="7fab2-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="7fab2-106">新しいアプリを作成し、Teamsアプリを統合します。</span><span class="sxs-lookup"><span data-stu-id="7fab2-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fab2-107">ここから開始</span><span class="sxs-lookup"><span data-stu-id="7fab2-107">Start here</span></span>](get-started/prerequisites.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="7fab2-108">アプリとはTeamsですか?</span><span class="sxs-lookup"><span data-stu-id="7fab2-108">What are Teams apps?</span></span>

<span data-ttu-id="7fab2-109">Teamsは機能の組み[合わせです](concepts/capabilities-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7fab2-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md).</span></span> <span data-ttu-id="7fab2-110">一部のアプリは単純 (通知の送信) ですが、複雑なアプリもあります (患者レコードの管理)。</span><span class="sxs-lookup"><span data-stu-id="7fab2-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="7fab2-111">アプリを計画する場合は、Teamsハブに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7fab2-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="7fab2-112">アプリの最適Teamsは、ユーザーが自分自身を表現し、より良く一緒に作業するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7fab2-112">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="personal-apps"></a><span data-ttu-id="7fab2-113">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="7fab2-113">Personal apps</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="7fab2-114">**ユーザーの集中を** 支援 [](concepts/design/personal-apps.md)する: 個人用アプリは、ユーザーが自分のタスクに集中したり、重要なアクティビティを表示したりするのに役立つ専用のスペースまたはボットです。</span><span class="sxs-lookup"><span data-stu-id="7fab2-114">**Help people focus**: A [personal app](concepts/design/personal-apps.md) is a dedicated space or bot to help users focus on their own tasks or view activities important to them.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="クライアントでの個人用アプリの外観の概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a><span data-ttu-id="7fab2-116">タブ</span><span class="sxs-lookup"><span data-stu-id="7fab2-116">Tabs</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="7fab2-117">**共同作業の便利さ**: Web ベースのコンテンツをタブ [](tabs/what-are-tabs.md)に表示し、ユーザーが一緒に話し合って作業できます。</span><span class="sxs-lookup"><span data-stu-id="7fab2-117">**Collaborate more conveniently**: Display your web-based content in a [tab](tabs/what-are-tabs.md) where people can discuss and work on it together.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="クライアント内のタブの外観を概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a><span data-ttu-id="7fab2-119">ボット</span><span class="sxs-lookup"><span data-stu-id="7fab2-119">Bots</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="7fab2-120">**単語をアクションに** 変換する: 会話は、多くの場合、何かをする必要があります (注文の生成、コードの確認、チケットの状態の確認など)。</span><span class="sxs-lookup"><span data-stu-id="7fab2-120">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="7fab2-121">ボット[は、](bots/what-are-bots.md)これらの種類のワークフローをワークフローの内部で開始Teams。</span><span class="sxs-lookup"><span data-stu-id="7fab2-121">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="クライアントでのボットの外観の概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a><span data-ttu-id="7fab2-123">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="7fab2-123">Messaging extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="7fab2-124">**マルチタスクを容易にする**: メッセージング拡張機能 [を](messaging-extensions/what-are-messaging-extensions.md)使用すると、会話で外部情報をすばやく共有できます。</span><span class="sxs-lookup"><span data-stu-id="7fab2-124">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="7fab2-125">また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理できます。</span><span class="sxs-lookup"><span data-stu-id="7fab2-125">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="クライアントでのメッセージング拡張機能の外観の概念Teamsします。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a><span data-ttu-id="7fab2-127">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="7fab2-127">Meeting extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="7fab2-128">**会議用アプリを作成する**: アプリを通話エクスペリエンスに組み込むTeams [があります](apps-in-teams-meetings/design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="7fab2-128">**Create apps for meetings**: There are a few options for [incorporating your app into the Teams calling experience](apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="会議の拡張機能がクライアントでどのような表示をTeamsします。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a><span data-ttu-id="7fab2-130">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="7fab2-130">Webhooks and connectors</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="7fab2-131">**外部アプリと通信** する:[受信 Webhooks は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)、別のアプリから別のチャネルに通知を自動的に送信Teamsです。</span><span class="sxs-lookup"><span data-stu-id="7fab2-131">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="7fab2-132">送信 [Webhooks を使用して](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)、Web サービスにメッセージを送信@mention。</span><span class="sxs-lookup"><span data-stu-id="7fab2-132">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="クライアントでのコネクタの外観の概念Teamsします。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="7fab2-134">Microsoft Graph Teams</span><span class="sxs-lookup"><span data-stu-id="7fab2-134">Microsoft Graph for Teams</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="7fab2-135">**Teams** データを利用する : [Microsoft Graph API for Teams](/graph/teams-concept-overview)では、チーム、チャネル、ユーザー、メッセージに関する情報にアクセスし、アプリの機能 (リッチ通知など) の作成や強化に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7fab2-135">**Utilize Teams data**: The [Microsoft Graph API for Teams](/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app (such as rich notifications).</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API の概念Teams。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="7fab2-137">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="7fab2-137">Start building</span></span>

<span data-ttu-id="7fab2-138">環境をセットアップし、簡単なアプリTeamsを作成することで、アプリの構築にすばやく慣れ親しむ必要があります。</span><span class="sxs-lookup"><span data-stu-id="7fab2-138">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fab2-139">初めてのアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="7fab2-139">Build your first app</span></span>](get-started/prerequisites.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="7fab2-140">Teams との統合</span><span class="sxs-lookup"><span data-stu-id="7fab2-140">Integrate with Teams</span></span>

<span data-ttu-id="7fab2-141">既存の Web アプリ、サービス、またはシステムに関するユーザーが気に入る機能と、ユーザーの共同作業機能を組み合Teams。</span><span class="sxs-lookup"><span data-stu-id="7fab2-141">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fab2-142">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="7fab2-142">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="7fab2-143">小さなコードは長い道のりを行く</span><span class="sxs-lookup"><span data-stu-id="7fab2-143">A little code goes a long way</span></span>

<span data-ttu-id="7fab2-144">素晴らしいアプリを構築するために専門家のプログラマである必要Teams。</span><span class="sxs-lookup"><span data-stu-id="7fab2-144">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="7fab2-145">いくつかの低コードソリューションのいずれかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="7fab2-145">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fab2-146">低コード アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="7fab2-146">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="7fab2-147">アプリのアイデアを取得する</span><span class="sxs-lookup"><span data-stu-id="7fab2-147">Get ideas for your app</span></span>

<span data-ttu-id="7fab2-148">アプリ開発のインスピレーションをお探しですか?</span><span class="sxs-lookup"><span data-stu-id="7fab2-148">Looking for app development inspiration?</span></span> <span data-ttu-id="7fab2-149">高忠実度の概念モックを使用して、実際のシナリオと業界のソリューションの一覧を参照して、アプリがユーザーに役立つさまざまなTeamsを理解します。</span><span class="sxs-lookup"><span data-stu-id="7fab2-149">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fab2-150">アプリのシナリオを見る</span><span class="sxs-lookup"><span data-stu-id="7fab2-150">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="7fab2-151">関連項目</span><span class="sxs-lookup"><span data-stu-id="7fab2-151">See also</span></span>

* <span data-ttu-id="7fab2-152">[Web サイトに [共有Teams] ボタンを追加する](concepts/build-and-test/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="7fab2-152">[Add a Share-to-Teams button to your website](concepts/build-and-test/share-to-teams.md)</span></span>
* [<span data-ttu-id="7fab2-153">アプリをTeamsする</span><span class="sxs-lookup"><span data-stu-id="7fab2-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="7fab2-154">Microsoft TeamsJavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="7fab2-154">Microsoft Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="7fab2-155">JavaScript および[.NET](https://github.com/Microsoft/botbuilder-dotnet/)用[ボット フレームワーク](https://github.com/Microsoft/botbuilder-js)SDK</span><span class="sxs-lookup"><span data-stu-id="7fab2-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="7fab2-156">アプリをTeamsする</span><span class="sxs-lookup"><span data-stu-id="7fab2-156">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
