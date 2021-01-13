---
title: Microsoft Teams プラットフォーム用アプリを構築する
author: heath-hamilton
description: 開発者がカスタム アプリで Microsoft Teams の機能を拡張する方法の概要について説明します。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 45be2dd7d0e421ac331cfc02703f0b81eab3dfe5
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797772"
---
# <a name="build-apps-for-microsoft-teams"></a>Microsoft Teams のアプリを作成する

Microsoft Teams アプリは、重要な情報、一般的なツール、信頼できるプロセスを提供し、ユーザーの収集、学習、作業が増えています。

アプリは、ニーズに合わせて Teams を拡張する方法です。 Teams の新しいアプリを作成するか、既存のアプリを統合します。

> [!div class="nextstepaction"]
> [ここから開始](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Teams アプリとは

Teams アプリは、機能と [エントリ ポイントの](concepts/capabilities-overview.md) 組み [合わせです](concepts/extensibility-points.md)。 たとえば、ユーザーはチャネル *(エントリ* ポイント) でアプリのボット(機能) とチャットできます。

一部のアプリは単純な (通知を送信する) 一方で、他のアプリは複雑です (患者の記録を管理します)。 アプリを計画する際には、Teams はコラボレーション ハブです。 最高の Teams アプリは、ユーザーが自分自身を表現し、より良く一緒に作業するのに役立ちます。

:::row:::
   :::column span="":::

### <a name="tabs"></a>タブ

**情報をより便利に取得** する : 場合によっては、見つけやすくする必要がある場合があります。 タブに重要な Web [ページを表示](tabs/what-are-tabs.md)します。このタブは、Teams の静的および動的なコンテンツに対して、全画面の Web エクスペリエンスを提供します。

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでのタブの外観の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>ボット

**単語をアクション** にする : 会話の結果、多くの場合、何かを行う必要があります (注文の生成、コードの確認、チケットの状態の確認など)。 ボット [は](bots/what-are-bots.md) 、Teams 内でこれらの種類のワークフローを開始できます。

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでのボットの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>メッセージング拡張機能

**マルチタスクを容易にする**: メッセージング [](messaging-extensions/what-are-messaging-extensions.md)拡張機能を使用すると、会話内で外部情報をすばやく共有できます。 また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理を実行できます。

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでのメッセージング拡張機能の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhook

**外部アプリと通信** する : [受信 Webhook は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 、別のアプリから Teams チャネルに自動的に通知を送信する簡単な方法です。 送信 [Webhook を使用して、Web](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)サービスにメッセージを送信@mention。

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでのコネクタの外観の概念表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Teams 用 Microsoft Graph

**Teams データ** の利用 : Teams 用 [Microsoft Graph API](https://docs.microsoft.com/graph/teams-concept-overview) は、アプリの機能の作成や強化に役立つ、チーム、チャネル、ユーザー、メッセージに関する情報へのアクセスを提供します。

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API for Teams の概念表現。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>構築を開始する

   簡単なアプリを作成し、一般的に使用される機能を追加することで、Teams の構築にすばやく慣れ親しむ必要があります。

   > [!div class="nextstepaction"]
   > [最初のアプリを今すぐビルドする](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Teams との統合

   ユーザーが既存の Web アプリ、サービス、またはシステムについて気に入った機能と、Teams の共同作業機能をブレンドします。

   > [!div class="nextstepaction"]
   > [既存のアプリを統合する](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>簡単なコードは長い道のりを行く

   You don't need to be an expert programmer to build a great Teams app. いくつかの低コード ソリューションのいずれかを試してみてください。

   > [!div class="nextstepaction"]
   > [低コード アプリを作成する](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a>リソース

* [Web サイトに [Share-to-Teams] ボタンを追加する](concepts/build-and-test/share-to-teams.md)
* <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>
* [Microsoft Teams JavaScript クライアント SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) および [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [組織または AppSource にアプリを公開する](concepts/deploy-and-publish/overview.md)
