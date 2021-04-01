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
# <a name="build-apps-for-microsoft-teams"></a>Microsoft Teams のアプリを作成する

Microsoft Teams アプリは、重要な情報、一般的なツール、信頼できるプロセスを、ユーザーがますます収集、学習、作業する場所に提供します。

アプリは、ニーズに合わせて Teams を拡張する方法です。 Teams 用に新しいアプリを作成するか、既存のアプリを統合します。

> [!div class="nextstepaction"]
> [ここから開始](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Teams アプリとは

Teams アプリは、機能とエントリ[ポイントの組み](concepts/capabilities-overview.md)[合わせです](concepts/extensibility-points.md)。 たとえば、ユーザーはチャネル *(エントリ* ポイント) でアプリのボット(機能) とチャットできます。

一部のアプリは単純 (通知の送信) ですが、複雑なアプリもあります (患者レコードの管理)。 アプリを計画する際は、Teams はコラボレーション ハブです。 最高の Teams アプリは、ユーザーが自分自身を表現し、より良い仕事を共にするのに役立ちます。

:::row:::
   :::column span="":::

### <a name="tabs"></a>タブ

**情報をより便利に取得する**: 場合によっては、見つけやすくする必要がある場合があります。 タブに重要な Web [ページを](tabs/what-are-tabs.md)表示し、Teams の静的コンテンツと動的コンテンツのフルスクリーン Web エクスペリエンスを提供します。

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでのタブの外観の概念的表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>ボット

**単語をアクションに** 変換する: 会話は、多くの場合、何かをする必要があります (注文の生成、コードの確認、チケットの状態の確認など)。 ボット [は、Teams](bots/what-are-bots.md) の内部でこれらの種類のワークフローを開始できます。

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでのボットの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>メッセージング拡張機能

**マルチタスクを容易にする**: メッセージング拡張機能 [を](messaging-extensions/what-are-messaging-extensions.md)使用すると、会話で外部情報をすばやく共有できます。 また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理できます。

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでのメッセージング拡張機能の外観の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhook

**外部アプリと通信** する : [受信 Webhooks は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 、別のアプリから Teams チャネルに通知を自動的に送信する簡単な方法です。 送信 [Webhooks を使用して](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)、Web サービスにメッセージを送信@mention。

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでのコネクタの外観の概念的表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

**Teams データの利用**: [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) では、アプリの機能の作成や強化に役立つチーム、チャネル、ユーザー、メッセージに関する情報にアクセスできます。

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API for Teams の概念表現。" border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a>Microsoft Teams アプリのソリューションを構築する
 
Microsoft は、業界別に整理された Teams アプリのシナリオ ライブラリである拡張性の外観ブックを提供しています。 このブックは、Teams プラットフォームでアプリを構築し、さまざまな Teams プラットフォーム機能を使用してさまざまなシナリオを理解するのに役立ちます。 ルック ブックのシナリオは、ビジネス上の問題、課題に関連するペルサから始め、ビジネス ニーズに対応する Teams アプリ ソリューションで終了します。

このライブラリの各シナリオには、一連の忠実度の高いデザイン概念モックが伴います。これは、アプリを設計し、ユーザー エクスペリエンスを向上させるインスピレーションとして役立つ可能性があります。 さらに、このルック ブックでは、各アプリの構築に続く設計とアーキテクチャのベスト プラクティスが強調表示されています。 詳細については、「機能拡張の一覧」を参照してください。 詳細については、「機能拡張 [ルック ブック」を参照してください](https://adoption.microsoft.com/extensibility-look-book/scenarios/)。 

## <a name="start-building"></a>構築を開始する

簡単なアプリを作成し、一般的に使用される機能を追加することで、Teams の構築についてすぐに理解できます。

> [!div class="nextstepaction"]
> [最初のアプリを今すぐビルドする](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Teams との統合

既存の Web アプリ、サービス、またはシステムに関するユーザーが気に入る機能と、Teams の共同作業機能をブレンドします。

> [!div class="nextstepaction"]
> [既存のアプリを統合する](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>小さなコードは長い道のりを行く

素晴らしい Teams アプリを構築するために、エキスパート プログラマである必要はなんらない。 いくつかの低コードソリューションのいずれかを試してみてください。

> [!div class="nextstepaction"]
> [低コード アプリを作成する](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a>関連情報

* [Share-to-Teams ボタンを Web サイトに追加する](concepts/build-and-test/share-to-teams.md)
* [Teams アプリを設計する](concepts/design/design-teams-app-overview.md)
* [Microsoft Teams JavaScript クライアント SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* JavaScript および[.NET](https://github.com/Microsoft/botbuilder-dotnet/)用[ボット フレームワーク](https://github.com/Microsoft/botbuilder-js)SDK
* [Teams アプリを発行する](concepts/deploy-and-publish/overview.md)
