---
title: アプリの機能を理解する
author: heath-hamilton
description: タブ、ボット、メッセージングの拡張機能、Webhooks やコネクタなどの Teams アプリの機能、個人用アプリや共有アプリなどのアプリ スコープの説明
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 09/22/2020
keywords: タブ bot メッセージングの拡張機能 webhook コネクタ
ms.openlocfilehash: ecc7ddc9ff1a80aa4eb5b37c55088f5fa5721b37
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355546"
---
# <a name="understand-microsoft-teams-app-features"></a>Microsoft Teams アプリの機能を理解する

Teams を拡張する方法は複数あり、アプリごとに異なります。 さまざまな方法で Teams アプリをユーザーに表示できます。 Teams アプリの機能には次のものが含まれます。

- アプリの機能
- アプリのスコープ

たとえば、ユーザーは同一のアクティビティを実行するためにキャンバス タブでアプリを操作するか、会話型ボットを使用する場合があります。 Webhook などの機能は 1 つのみですが、他の機能にはユーザーにさまざまなオプションを提供する機能があります。

これらの機能は、さまざまなスコープにまたがって存在する可能性があります。たとえば、アプリでは、中央の共有場所 (タブ) にデータを表示し、その同じ情報を個人の会話インターフェイス (ボット) を介して表示できます。

## <a name="app-capabilities"></a>アプリの機能

アプリを拡張できるようになるには、すべの主要な機能と、共同作業スペースで機能するエントリ ポイントを理解する必要があります。 アプリをビルドするための拡張機能ポイントを試してみることができます。 重要なアプリ プロジェクト コンポーネントは、アプリ ページを正しく構成するのに役立ちます。

Teams アプリには、次の主要な機能のいずれか、またはすべてが含まれます。

:::row:::
   :::column span="":::
### <a name="personal-apps"></a>個人用アプリ

[個人用アプリ](../concepts/design/personal-apps.md)は、ユーザーが自分のタスクに集中したり、重要なアクティビティを表示したりするのに役立つ専用のスペースまたはボットです。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-personal-apps-2021.png" alt-text="Teams クライアントでの個人用アプリの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="tabs"></a>タブ

Web ベースのコンテンツを[タブ](../tabs/what-are-tabs.md)に表示します。こでは、他のユーザーが話し合って共同作業を行うことができます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-channel-chat-apps-2021.png" alt-text="Teams クライアントでタブがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>ボット

多くの場合、会話によって何らかの行動を取る必要性が発生します (注文の生成、自分のコードの確認、チケットの状態の確認など)。 [ボット](../bots/what-are-bots.md)は、このようなワークフローを Teams 内で開始することができます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-bots-2021.png" alt-text="Teams クライアントでボットがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>メッセージング拡張機能

[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)を使用して、外部の情報をすばやく会話の中で共有できます。 また、チャネル投稿の内容に基づいてヘルプ チケットを作成するなど、メッセージに対して操作を行うこともできます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-messaging-extensions-2021.png" alt-text="Teams クライアントでメッセージング拡張機能がどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="meeting-extensions"></a>ミーディング拡張機能

[Teams の通話エクスペリエンスにアプリを組み込む](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)ためのオプションがいくつか用意されています。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-meeting-extensions-2021.png" alt-text="Teams クライアントでの会議拡張機能の概念表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="webhooks-and-connectors"></a>Webhook とコネクタ

[受信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) は、他のアプリから Teams チャネルに通知を自動的に送信するためのシンプルな方法です。 [発信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks) では、@mention を使用して Web サービスにメッセージを送信します。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-connectors.png" alt-text="Teams クライアントでコネクタがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

[Microsoft Graph API for Teams](/graph/teams-concept-overview) は、アプリの機能 (多機能な通知など) を作成または強化するのに役立つチーム、チャネル、ユーザー、メッセージに関する情報へのアクセスを提供します。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-graph.png" alt-text="Microsoft Graph for Teams についての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> Teams ストアは進化しました。以前は、タイルの省略記号を選択することで LOB アプリが更新されました。 Teams ストア エクスペリエンスが更新され、[Teams 管理センター](https://admin.teams.microsoft.com)にログインして LOB アプリを更新できるようになりました。

## <a name="choose-the-correct-scope-for-your-app"></a>アプリの正しいスコープを選択する

アプリのスコープとして、次のいずれかを選択できます。

- 個人用アプリ エクスペリエンス: 個人用アプリは、ユーザーが自分のタスクに集中したり、重要なアクティビティを表示したりするのに役立つ専用のスペースまたはボットです。
- 共有アプリ エクスペリエンス: Teams、チャネル、およびチャットは共同作業スペースです。 これらのコンテキストのアプリは、そのスペース内のすべてのユーザーが利用できます。 通常、共同作業スペースでは、アプリの操作や新しい社会的対話の実現に重点が置かれます。

## <a name="see-also"></a>関連項目

* [Teams 用アプリの作成](../overview.md)
* [最初の Microsoft Teams アプリをビルドする](../build-your-first-app/build-first-app-overview.md)