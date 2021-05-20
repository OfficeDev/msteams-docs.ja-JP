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
# <a name="build-apps-for-microsoft-teams"></a>Microsoft Teams のアプリを作成する

Microsoft Teamsアプリは、重要な情報、共通のツール、信頼できるプロセスを、人々がますます集まり、学び、働く場所に提供します。

アプリは、ニーズに合わせてTeamsを拡張する方法です。 Teamsのために何か新しいものを作成するか、既存のアプリを統合します。

> [!div class="nextstepaction"]
> [ここから開始](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>Teamsアプリとは何ですか?

Teamsアプリは[、機能](concepts/capabilities-overview.md)と[エントリ ポイント](concepts/extensibility-points.md)の組み合わせです。 たとえば、*チャンネル*(エントリ ポイント) でアプリの *ボット*(機能) とチャットできます。

アプリの中には単純なもの(通知を送信する)、複雑なアプリ(患者レコードの管理)があります。 アプリを計画する際は、Teamsがコラボレーション ハブであることを覚えておいてください。 最高のTeamsアプリは、人々が自分自身を表現し、より良い一緒に働くのに役立ちます。

:::row:::
   :::column span="":::

### <a name="tabs"></a>タブ

**情報をより便利に入手** する : 見つけやすい情報を得る必要がある場合もあります。 [タブ](tabs/what-are-tabs.md)に重要な Web ページを表示すると、Teamsで静的コンテンツと動的コンテンツのフルスクリーン Web エクスペリエンスが提供されます。

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでのタブの外観の概念図。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>ボット

**単語をアクションに変換する**: 会話は、多くの場合、何かをする必要があります (注文を生成する、コードを確認する、チケットの状態を確認するなど)。 [ボット](bots/what-are-bots.md)は、Teamsの内部でこのようなワークフローを開始できます。

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでのボットの外観の概念図。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>メッセージング拡張機能

**マルチタスクを簡単に** する : [メッセージング拡張機能](messaging-extensions/what-are-messaging-extensions.md)を使用すると、会話内の外部情報を素早く共有できます。 また、チャネル投稿の内容に基づいてヘルプチケットを作成するなど、メッセージに対して行動することもできます。

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでのメッセージング拡張機能の概念表現。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhook

**外部アプリとの通信**:[受信 webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)は、別のアプリからTeams チャネルに通知を自動的に送信する簡単な方法です。 [送信 Webhook を使用して、web](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)サービスに@mentionをメッセージします。

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでコネクタがどのような外観を持つのかを概念的に表します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>マイクロソフトのTeams Graph

**Teamsデータを利用** する : [Teams用の Microsoft Graph API](/graph/teams-concept-overview)は、アプリの機能を作成または強化するのに役立つチーム、チャネル、ユーザー、およびメッセージに関する情報にアクセスできるようにします。

:::image type="content" source="assets/images/overview-graph.png" alt-text="Teams用のマイクロソフト Graph API の概念図。" border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>建物の開始

環境をセットアップし、簡単なアプリを作成することで、Teams用の構築にすぐに慣れ親しみます。

> [!div class="nextstepaction"]
> [初めてのアプリを構築する](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Teams との統合

既存の Web アプリ、サービス、またはシステムに関してユーザーが愛する機能と、Teamsのコラボレーション機能を組み合わせます。

> [!div class="nextstepaction"]
> [既存のアプリを統合する](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>小さなコードは長い道のりを行く

優れたTeamsアプリを構築するために、エキスパートプログラマーである必要はありません。 いくつかの低コード ソリューションのいずれかを試してみてください。

> [!div class="nextstepaction"]
> [低コード アプリを作成する](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>アプリのアイデアを入手する

アプリ開発のインスピレーションをお探しですか? 忠実度の高い概念モックを使用して、実世界のシナリオと業界ソリューションのリストを参照して、アプリがユーザーに役立つさまざまな方法Teams理解してください。

> [!div class="nextstepaction"]
> [アプリのシナリオを見る](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>関連項目

* [ウェブサイトに共有Teamsボタンを追加する](concepts/build-and-test/share-to-teams.md)
* [Teams アプリを設計する](concepts/design/design-teams-app-overview.md)
* [Microsoft Teamsクライアント SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* ボット フレームワーク SDK 用 [JavaScript](https://github.com/Microsoft/botbuilder-js) および [.NET](https://github.com/Microsoft/botbuilder-dotnet/)
* [Teams アプリを配布する](concepts/deploy-and-publish/apps-publish-overview.md)
