---
title: アプリケーション プラットフォーム用のアプリMicrosoft Teamsする
author: heath-hamilton
description: 開発者がカスタム アプリを使用して機能を拡張Microsoft Teams概要を確認します。
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

Microsoft Teamsアプリは、重要な情報、一般的なツール、信頼できるプロセスを、人々がますます収集、学習、作業する場所に提供します。

アプリは、ニーズに合わせてTeams拡張する方法です。 新しいアプリを作成し、Teamsアプリを統合します。

> [!div class="nextstepaction"]
> [ここから開始](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>アプリとはTeamsですか?

Teamsは、機能とエントリ ポイント[の組み](concepts/capabilities-overview.md)[合わせです](concepts/extensibility-points.md)。 たとえば、ユーザーはチャネル *(エントリ* ポイント) でアプリのボット(機能) とチャットできます。

一部のアプリは単純 (通知の送信) ですが、複雑なアプリもあります (患者レコードの管理)。 アプリを計画する場合は、Teamsハブに注意してください。 アプリの最適Teamsは、ユーザーが自分自身を表現し、より良く一緒に作業するのに役立ちます。

:::row:::
   :::column span="":::

### <a name="tabs"></a>タブ

**情報をより便利に取得する**: 場合によっては、見つけやすくする必要がある場合があります。 タブに重要な Web[ページを表示](tabs/what-are-tabs.md)します。このページでは、静的コンテンツと動的コンテンツのフルスクリーン Web エクスペリエンスを提供Teams。

:::image type="content" source="assets/images/overview-tabs.png" alt-text="クライアント内のタブの外観を概念Teamsします。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>ボット

**単語をアクションに** 変換する: 会話は、多くの場合、何かをする必要があります (注文の生成、コードの確認、チケットの状態の確認など)。 ボット[は、](bots/what-are-bots.md)これらの種類のワークフローをワークフローの内部で開始Teams。

:::image type="content" source="assets/images/overview-bots.png" alt-text="クライアントでのボットの外観の概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>メッセージング拡張機能

**マルチタスクを容易にする**: メッセージング拡張機能 [を](messaging-extensions/what-are-messaging-extensions.md)使用すると、会話で外部情報をすばやく共有できます。 また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理できます。

:::image type="content" source="assets\images\overview-messaging.png" alt-text="クライアントでのメッセージング拡張機能の外観の概念Teamsします。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhook

**外部アプリと通信** する:[受信 Webhooks は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)、別のアプリから別のチャネルに通知を自動的に送信Teamsです。 送信 [Webhooks を使用して](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)、Web サービスにメッセージを送信@mention。

:::image type="content" source="assets/images/overview-connectors.png" alt-text="クライアントでのコネクタの外観の概念Teamsします。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph Teams

**Teams** データを利用する : [microsoft Graph API for Teams](/graph/teams-concept-overview)では、アプリの機能の作成や強化に役立つチーム、チャネル、ユーザー、メッセージに関する情報にアクセスできます。

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API の概念Teams。" border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>構築を開始する

環境をセットアップし、簡単なアプリTeamsを作成することで、アプリの構築にすばやく慣れ親しむ必要があります。

> [!div class="nextstepaction"]
> [初めてのアプリを構築する](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>Teams との統合

既存の Web アプリ、サービス、またはシステムに関するユーザーが気に入る機能と、ユーザーの共同作業機能を組み合Teams。

> [!div class="nextstepaction"]
> [既存のアプリを統合する](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>小さなコードは長い道のりを行く

素晴らしいアプリを構築するために専門家のプログラマである必要Teams。 いくつかの低コードソリューションのいずれかを試してみてください。

> [!div class="nextstepaction"]
> [低コード アプリを作成する](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>アプリのアイデアを取得する

アプリ開発のインスピレーションをお探しですか? 高忠実度の概念モックを使用して、実際のシナリオと業界のソリューションの一覧を参照して、アプリがユーザーに役立つさまざまなTeamsを理解します。

> [!div class="nextstepaction"]
> [アプリのシナリオを見る](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>関連項目

* [Web サイトに [共有Teams] ボタンを追加する](concepts/build-and-test/share-to-teams.md)
* [アプリをTeamsする](concepts/design/design-teams-app-overview.md)
* [Microsoft TeamsJavaScript クライアント SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* JavaScript および[.NET](https://github.com/Microsoft/botbuilder-dotnet/)用[ボット フレームワーク](https://github.com/Microsoft/botbuilder-js)SDK
* [アプリをTeamsする](concepts/deploy-and-publish/apps-publish-overview.md)
