---
title: アプリのユース ケースと Teams 機能を理解する
author: heath-hamilton
description: この記事では、Microsoft Teams アプリの機能について説明します。また、Teams アプリを計画し、アプリ ユーザーとそのニーズ、Teams アプリで解決できるユーザーの問題を理解し、ユーザー認証とオンボーディング エクスペリエンスを計画します。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 55955972bb9ebfbb3699ebcbc2cc131afc00fbd1
ms.sourcegitcommit: 6189ca81099452a3ab2ff4fff4fb1ded5ba6dcfe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2022
ms.locfileid: "64498232"
---
# <a name="understand-your-use-cases"></a>ユース ケースを理解する

共同作業を行うことのできる Teams のソーシャルなフレームワークでは、Teams アプリを使用してさまざまなユーザー ニーズを解決できます。 たとえば、効果的なコラボレーションを実現する上でギャップを埋めるアプリは最適です。

アプリ ユーザーとアプリの要件は、すべてのアプリの選択を決定する基本的なガイドラインです。 アプリの設計の構築、機能の選択、ビルド環境とテスト環境の決定、アプリの配布は、アプリのユーザーの要件に従います。

アプリでユーザー要件を満たすには、まずユーザーの要件を理解する必要があります。

- **ユーザーを理解する**:
  - ユーザーの問題を認識し、ユーザーが直面する一般的な問題の解決策を特定します。
  - ユーザーのニーズを満たす適切な機能の組み合わせを見つけて、Teams アプリを構築します。
  - ユース ケースを理解して、エンド ユーザーがアプリを操作する方法を理解します。

- **問題を理解する**: アプリが解決する必要のある主要な問題を解決します。

- **統合を検討する**: アプリに必要なアプリとサービス (認証、Microsoft Graph、Web アプリなど) を特定します。

## <a name="microsoft-teams-app-features"></a>Microsoft Teams アプリの機能

Teams を拡張する方法は複数あり、アプリごとに異なります。Teams アプリの機能は次の機能を提供します。

- [アプリの機能](#app-capabilities)
- [アプリのスコープ](#app-scope)

### <a name="app-capabilities"></a>アプリの機能

機能は、アプリで構築することのできる主要な機能です。 また、統合と操作を可能にするため、エントリ ポイントまたは拡張ポイントとも呼ばれます。

Teams アプリには、次の主要な機能のいずれか、またはすべてが含まれます。

:::row:::
   :::column span="":::

#### <a name="personal-apps"></a>個人用アプリ

[個人用アプリ](../../concepts/design/personal-apps.md)は、ユーザーが自分のタスクに集中したり、関連するアクティビティを表示したりするのに役立つ専用のスペースまたはボットです。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-personal-apps-2021.png" alt-text="Teams クライアントでの個人用アプリの外観の概念表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="tabs"></a>タブ

Web ベースのコンテンツを[タブ](../../tabs/what-are-tabs.md)に表示します。こでは、他のユーザーが話し合って共同作業を行うことができます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-channel-chat-apps-2021.png" alt-text="Teams クライアントでタブがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="bots"></a>ボット

多くの場合、会話によって何らかの行動を取る必要性が発生します (注文の生成、コードの確認、チケットの状態の確認など)。 [ボット](../../bots/what-are-bots.md)は、このようなワークフローを Teams 内で開始することができます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-bots-2021.png" alt-text="Teams クライアントでボットがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

#### <a name="messaging-extensions"></a>メッセージング拡張機能

[メッセージング拡張機能](../../messaging-extensions/what-are-messaging-extensions.md)を使用すると、外部の情報を検索して共有できます。 また、チャネル投稿の内容に基づいてヘルプ チケットを作成するなど、メッセージに対して操作を行うこともできます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-messaging-extensions-2021.png" alt-text="Teams クライアントでメッセージング拡張機能がどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="meeting-extensions"></a>ミーディング拡張機能

[Teams の通話エクスペリエンスにアプリを組み込む](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)ためのオプションがいくつか用意されています。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-meeting-extensions-2021.png" alt-text="Teams クライアントでの会議拡張機能の概念表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="webhooks-and-connectors"></a>Webhook とコネクタ

[受信 Webhook](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) は、他のアプリから Teams チャネルに通知を自動的に送信するためのシンプルな方法です。 [発信 Webhook](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks) を使用すると、@メンションを使用して Web サービスにメッセージを送信できます。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-connectors.png" alt-text="Teams クライアントでコネクタがどのように表示されるかについての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

[Microsoft Graph API for Teams](/graph/teams-concept-overview) は、アプリの機能を作成または強化するのに役立つチーム、チャネル、ユーザー、メッセージに関する情報へのアクセスを提供します。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-graph.png" alt-text="Microsoft Graph for Teams についての概念的な表現。" border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> Teams ストアが進化しました。
>
> 以前は、タイルの省略記号を選択すれば LOB アプリが更新されました。 Teams ストア エクスペリエンスが更新され、[Teams 管理センター](https://admin.teams.microsoft.com)にログインして LOB アプリを更新できるようになりました。

### <a name="app-scope"></a>アプリのスコープ

アプリには、次のいずれかのスコープを指定できます。

- **個人用アプリ エクスペリエンス**: 個人用アプリは、ユーザーが自分のタスクに集中したり、重要なアクティビティを表示したりするのに役立つ専用のスペースまたはボットです。
- **共有アプリ エクスペリエンス**: Teams、チャネル、およびチャットは共同作業スペースです。 これらのコンテキストのアプリは、そのスペース内のすべてのユーザーが利用できます。 通常、共同作業スペースでは、アプリの操作や新しい社会的対話の実現に重点が置かれます。

アプリは、さまざまなスコープにまたがって存在できます。次に例を示します。

- アプリは、中央の共有場所 (タブ) にデータを表示できます。
- また、同じ情報を個人の会話インターフェイス (ボット) を介して表示することもできます。

ユーザーは同一のアクティビティを実行するためにキャンバス タブでアプリを操作するか、会話型ボットを使用する場合があります。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ユース ケースのマップ](../../concepts/design/map-use-cases.md)

## <a name="see-also"></a>関連項目

[デバイス機能の統合](~/concepts/device-capabilities/device-capabilities-overview.md)
