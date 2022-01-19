---
title: Microsoft Teams プラットフォーム用のアプリを構築する
author: heath-hamilton
description: 開発者がカスタム アプリを使用して Microsoft Teams の機能を拡張する方法の概要について説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 1a7957c8ea6d889ffe5ab7e40c8a5bb1377b6ca5
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059624"
---
# <a name="build-apps-for-microsoft-teams"></a>Microsoft Teams のアプリを作成する

Microsoft Teams アプリは、重要な情報、共通のツール、信頼できるプロセスを提供し、ユーザーが集まり、学習し、仕事をする場を増やします。

アプリは、ニーズに合わせて Teams を拡張するための方法です。 Teams 用に新しいものを作成するか、既存のアプリを統合します。

> [!div class="nextstepaction"]
> [ここから開始](get-started/get-started-overview.md)

## <a name="what-are-teams-apps"></a>Teams アプリとは

Teams アプリは、[機能](concepts/capabilities-overview.md)の組み合わせです。 アプリにはシンプルなもの (例: 通知の送信) もあれば、複雑なもの (例: 患者の記録の管理) もあります。 アプリを計画するときには、Teams がコラボレーション ハブであることにご注意ください。 ユーザーによる自分自身を表現や、より良い共同作業の実施をサポートするアプリこそが、最高の Teams アプリです。

### <a name="personal-apps"></a>個人用アプリ

:::row:::
   :::column span="1":::

**ユーザーがに集中できるようにする:** [個人用アプリ](concepts/design/personal-apps.md) は、ユーザーが自分のタスクに集中したり、重要なアクティビティを表示したりするのに役立つ専用のスペースまたはボットです。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="Teams クライアントでの個人用アプリの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a>タブ

:::row:::
   :::column span="1":::

**共同作業をより便利に**: web ベースのコンテンツを [タブ](tabs/what-are-tabs.md)に表示、他のユーザーが話し合って共同作業を行うことができます。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="Teams クライアントでタブがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a>ボット

:::row:::
   :::column span="1":::

**言葉を行動に変える**: 会話は、多くの場合何らかの行動の必要性 (注文の生成、自分のコードの確認、チケットの状態の確認など) につながります。 [ボット](bots/what-are-bots.md)は、このようなワークフローを Teams 内で開始することができます。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="Teams クライアントでボットがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a>メッセージング拡張機能

:::row:::

   :::column span="1":::

**マルチタスクを容易にする**: [メッセージング拡張機能](messaging-extensions/what-are-messaging-extensions.md)を使用すれば、外部の情報をすばやく会話の中で共有することができます。 また、チャネル投稿の内容に基づいてヘルプ チケットを作成するなど、メッセージに対して操作を行うこともできます。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="Teams クライアントでメッセージング拡張機能がどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a>ミーディング拡張機能

:::row:::

   :::column span="1":::

**会議用アプリの作成**:[Teams の通話エクスペリエンスにアプリを組み込む](apps-in-teams-meetings/design/designing-apps-in-meetings.md)には、いくつかのオプションがあります。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="Teams クライアントでの会議拡張機能の概念表現。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a>Webhook とコネクタ

:::row:::

   :::column span="":::

**外部アプリとのコミュニケーション**: [受信 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) は、他のアプリから Teams チャネルに通知を自動的に送信するためのシンプルな方法です。 [発信 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks) では、@mention を使用して Web サービスにメッセージを送信します。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでコネクタがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

:::row:::

   :::column span="":::

**Teams のデータを活用する**: [Microsoft Graph API for Teams](/graph/teams-concept-overview) は、アプリの機能を作成または強化するのに役立つ、チーム、チャネル、ユーザー、メッセージに関する情報へのアクセスを提供します。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph for Teams についての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>構築の開始

シンプルなアプリの作成や、一般的な機能の追加を通して、Teams 用アプリの作成にすばやく慣れていきましょう。

> [!div class="nextstepaction"]
> [初めてのアプリを構築する](get-started/get-started-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Teams との統合

ユーザーが慣れ親しんでいる既存の Web アプリ、サービス、システムの機能と Teams のコラボレーション機能を融合させましょう。

> [!div class="nextstepaction"]
> [既存のアプリを統合する](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>小さなコードが大きな意味を持つ

優れた Teams アプリを構築するのに、専門のプログラマーである必要はありません。 いくつかのローコード ソリューションの中から、1 つを試してみましょう。

> [!div class="nextstepaction"]
> [ローコード アプリの作成](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>アプリのアイデアを入手する

アプリ開発のインスピレーションをお探しですか? 忠実度の高い概念モックを使用した実際のシナリオと業界ソリューションの一覧を参照して、Teams アプリがユーザーを支援するさまざまな方法を理解します。

> [!div class="nextstepaction"]
> [アプリのシナリオを見る](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="test-your-app-running-across-microsoft-365"></a>Microsoft 365で実行されているアプリをテストする

Microsoft Teams JavaScript クライアント SDK v2 Preview を使用すると、他の高使用率Microsoft 365エクスペリエンスで実行されている Teams アプリをプレビューできます。

> [!div class="nextstepaction"]
> [アプリを拡張する](m365-apps/overview.md)

## <a name="see-also"></a>関連項目

* [アプリの基本事項](~/concepts/app-fundamentals-overview.md)
* [Teams アプリを設計する](~/concepts/design/design-teams-app-process.md)
* [ユース ケースを Teams アプリの機能にマップ](~/concepts/design/map-use-cases.md)
