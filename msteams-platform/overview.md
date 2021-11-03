---
title: アプリケーション プラットフォーム用のアプリMicrosoft Teamsする
author: heath-hamilton
description: 開発者がカスタム アプリを使用して機能を拡張Microsoft Teams概要を確認します。
ms.topic: overview
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: fcec0e01f6f9d635896ef14eb4efee5e56f9e761
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720114"
---
# <a name="build-apps-for-microsoft-teams"></a>Microsoft Teams のアプリを作成する

Microsoft Teamsアプリは、重要な情報、一般的なツール、信頼できるプロセスを、人々がますます収集、学習、作業する場所に提供します。

アプリは、ニーズに合わせてTeams拡張する方法です。 新しいアプリを作成し、Teamsアプリを統合します。

> [!div class="nextstepaction"]
> [ここから開始](get-started/get-started-overview.md)

## <a name="what-are-teams-apps"></a>アプリとはTeamsですか?

Teamsは機能の組み[合わせです](concepts/capabilities-overview.md)。 一部のアプリは単純 (通知の送信) ですが、複雑なアプリもあります (患者レコードの管理)。 アプリを計画する場合は、Teamsハブに注意してください。 アプリの最適Teamsは、ユーザーが自分自身を表現し、より良く一緒に作業するのに役立ちます。

### <a name="personal-apps"></a>個人用アプリ

:::row:::
   :::column span="1":::

**ユーザーの集中を** 支援 [](concepts/design/personal-apps.md)する: 個人用アプリは、ユーザーが自分のタスクに集中したり、重要なアクティビティを表示したりするのに役立つ専用のスペースまたはボットです。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="クライアントでの個人用アプリの外観の概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a>タブ

:::row:::
   :::column span="1":::

**共同作業の便利さ**: Web ベースのコンテンツをタブ [](tabs/what-are-tabs.md)に表示し、ユーザーが一緒に話し合って作業できます。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="クライアント内のタブの外観を概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a>ボット

:::row:::
   :::column span="1":::

**単語をアクションに** 変換する: 会話は、多くの場合、何かをする必要があります (注文の生成、コードの確認、チケットの状態の確認など)。 ボット[は、](bots/what-are-bots.md)これらの種類のワークフローをワークフローの内部で開始Teams。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="クライアントでのボットの外観の概念Teamsします。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a>メッセージング拡張機能

:::row:::

   :::column span="1":::

**マルチタスクを容易にする**: メッセージング拡張機能 [を](messaging-extensions/what-are-messaging-extensions.md)使用すると、会話で外部情報をすばやく共有できます。 また、チャネル投稿のコンテンツに基づいてヘルプ チケットを作成するなどのメッセージに対して処理できます。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="クライアントでのメッセージング拡張機能の外観の概念Teamsします。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a>ミーディング拡張機能

:::row:::

   :::column span="1":::

**会議用アプリを作成する**: アプリを通話エクスペリエンスに組み込むTeams [があります](apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="会議の拡張機能がクライアントでどのような表示をTeamsします。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a>Webhook とコネクタ

:::row:::

   :::column span="":::

**外部アプリと通信** する:[受信 Webhooks は](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)、別のアプリから別のチャネルに通知を自動的に送信Teamsです。 送信 [Webhooks を使用して](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)、Web サービスにメッセージを送信@mention。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="クライアントでのコネクタの外観の概念Teamsします。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph Teams

:::row:::

   :::column span="":::

**Teams** データを利用する : [Microsoft Graph API for Teams](/graph/teams-concept-overview)では、チーム、チャネル、ユーザー、メッセージに関する情報にアクセスし、アプリの機能 (リッチ通知など) の作成や強化に役立ちます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API の概念Teams。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>構築を開始する

環境をセットアップし、簡単なアプリTeamsを作成することで、アプリの構築にすばやく慣れ親しむ必要があります。

> [!div class="nextstepaction"]
> [初めてのアプリを構築する](get-started/get-started-overview.md)

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
