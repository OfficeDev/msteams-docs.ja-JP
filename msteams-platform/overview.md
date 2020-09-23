---
title: Microsoft Teams プラットフォーム用のアプリを構築する
author: heath-hamilton
description: 開発者がカスタムアプリを使用して Microsoft Teams の機能を拡張およびカスタマイズする方法の概要。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: c430add71e7c23a44a552270c5e3c1bacbe650e4
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209800"
---
# <a name="build-apps-for-microsoft-teams"></a>Microsoft Teams のアプリを構築する

Microsoft Teams アプリは、ユーザーが収集、学習、作業を徐々に行うことができるように、重要な情報、共通ツール、および信頼されたプロセスを提供します。

アプリは、ニーズに合わせて Teams を拡張する方法を示します。 Teams で新しいものを作成するか、既存のアプリを統合します。

## <a name="what-are-teams-apps"></a>Teams アプリとは

Teams アプリは、 [機能](concepts/capabilities-overview.md) と [エントリポイント](concepts/extensibility-points.md)の組み合わせです。 たとえば、ユーザーは、*チャネル*(エントリポイント) のアプリの*bot* (機能) とチャットできます。

単純な (通知を送信する) アプリもあれば、複雑なアプリ (患者レコードの管理) もあります。 アプリを計画するときは、Teams がコラボレーションハブであることに注意してください。 最良の Teams アプリを使用すると、ユーザーが自分を表現し、連携しやすくなります。

:::row:::
   :::column span="":::

### <a name="tabs"></a>タブ

**情報をさら**にわかりやすくする: 必要な場合にのみ、簡単に情報を見つけられるようにしましょう。 重要な web ページを [タブ](tabs/what-are-tabs.md)で表示します。これにより、チーム内の静的および動的なコンテンツについて全画面 web を利用できます。

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams クライアントでタブがどのように表示されるかを概念として表します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a>メッセージングの拡張機能

マルチ**タスクを簡単にする**:[メッセージング拡張機能](messaging-extensions/what-are-messaging-extensions.md)を使用すると、会話で外部情報をすばやく共有できます。 また、メッセージを操作することもできます。これには、チャネル投稿の内容に基づくヘルプチケットの作成などがあります。

:::image type="content" source="assets\images\overview-messaging.png" alt-text="Teams クライアントでメッセージング拡張機能がどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>ボット

**単語をアクションにする**: 会話では、多くの場合、何らかの処理が必要になります (注文を生成し、自分のコードを確認し、チケットの状態を確認するなど)。 [Bot](bots/what-are-bots.md)は、Teams 内でこれらの種類のワークフローを直接開始できます。

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams クライアントでボットがどのように表示されるかを概念的に表現します。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a>Webhook

**外部アプリと通信**する: [受信 web フック](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) は、別のアプリから Teams チャネルに通知を自動的に送信する簡単な方法です。 送信用の [webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)を使用して、web サービスに @mention のメッセージを表示します。

:::image type="content" source="assets/images/overview-connectors.png" alt-text="Teams クライアントでどのコネクタが表示されるかを概念として表します。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Teams の Microsoft Graph

**Teams データを利用**する: [Microsoft Graph API for teams](https://docs.microsoft.com/graph/teams-concept-overview) は、teams、チャネル、ユーザー、およびメッセージに関する情報へのアクセスを提供します。これは、アプリの機能を作成または拡張するのに役立ちます。

:::image type="content" source="assets/images/overview-graph.png" alt-text="Teams 用の Microsoft Graph API の概念図。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a>概要

最初のアプリチュートリアルですぐにジャンプするか、既存のアプリを統合してインポートする方法について説明します。

:::row:::
   :::column span="2":::

### <a name="start-building"></a>構築を開始する

   シンプルなアプリを作成し、一般的に使用される機能を追加することで、Teams の構築にすばやく慣れることができます。

   > [!div class="nextstepaction"]
   > [今すぐ最初のアプリを作成する](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a>Teams との統合

   Teams の共同作業機能を使用して、ユーザーが既存の web アプリ、サービス、またはシステムについて気に入った機能を融合します。

   > [!div class="nextstepaction"]
   > [既存のアプリを統合する](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a>少しのコードが長い

   魅力的な Teams アプリを構築するために専門のプログラマである必要はありません。 いくつかの低コードソリューションのいずれかを試してみてください。

   > [!div class="nextstepaction"]
   > [低コードアプリを作成する](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a>リソース

* [Web サイトに [Teams に共有] ボタンを追加する](concepts/build-and-test/share-to-teams.md)
* [Fluent デザインシステム](https://fluentsite.z22.web.core.windows.net/)
* [Microsoft Teams JavaScript クライアント SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [JavaScript のボット FRAMEWORK sdk](https://github.com/Microsoft/botbuilder-js)および[bot framework sdk (.net](https://github.com/Microsoft/botbuilder-dotnet/) )
* [アプリを組織または AppSource に発行する](concepts/deploy-and-publish/overview.md)
