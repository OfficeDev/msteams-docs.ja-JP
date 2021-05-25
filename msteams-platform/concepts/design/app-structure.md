---
title: アプリを設計する - アプリの構造を理解する
description: アプリを設計する際に、アプリでカスタマイズMicrosoft Teamsを理解します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631389"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>アプリ構造Microsoft Teams理解する

アプリを構築する際には、アプリでカスタマイズできる機能とカスタマイズできない機能を知Microsoft Teams。 この情報は、コントロールするアプリ エクスペリエンスの部分をよりよく理解するのに役立ちます。

次のワイヤーフレームを使用すると、次の情報が表示されます。

* 各アプリ機能でカスタマイズできるTeams (青で示されています)。
* 各機能がサポートするスコープ。

> [!NOTE]
> **スコープとはどういう意味ですか?** スコープは、ユーザーがアプリをTeamsできる領域です。 アプリには、個人、チャネル、チャット、会議など、1 つ以上のスコープを設定できます。

## <a name="personal-apps"></a>個人用アプリ

個人用アプリは、個々のユーザーのアプリ コンテンツをホストする大きなキャンバスを提供します。 キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

***サポートされているスコープ**: 個人用*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="開発者が個人用アプリ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

## <a name="tabs"></a>タブ

タブは、ユーザーグループのアプリ コンテンツをホストする大きなキャンバスを提供します。 チャネル、チャット、会議出席招待などの共有スペースにタブを含めることができます。 キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

***サポートされているスコープ**: チャネル、チャット、会議*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="開発者がタブ用にカスタマイズできるTeamsフロントエンド領域を示す概念図。" border="false":::

## <a name="bots"></a>ボット

ボットは、ネイティブ メッセージング機能Teams統合する会話型アプリなので、UI の作業が処理されます。 デザインの観点からは、自然言語処理 (NLP) サポートとアダプティブ カード プラットフォームを使用して、個性、カスタム機能、豊富で操作可能な情報を追加する機会がまだ存在します。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="開発者がボット用にカスタマイズできるTeamsフロントエンド領域を示す概念イメージ。" border="false":::

## <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能は、アプリコンテンツを挿入したり、会話から離れることなくメッセージに作用するためのショートカットです。 アクション ベースのメッセージング拡張機能を使用すると、エクスペリエンスの制御が向上しますが、Teamsベースのメッセージング拡張機能のレンダリングの多くを処理できます。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="開発者がメッセージング拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

## <a name="meeting-extensions"></a>ミーディング拡張機能

会議拡張機能は、ライブ会議を強化するアプリです。 会議の前、中、後など、いくつかのシナリオでアプリ コンテンツをホストできます。 サーフェスは iframe であり、エクスペリエンスをカスタマイズできますが、これらのアプリは暗いテーマで、会議中は狭くなります。

***サポートされているスコープ**: 会議、チャット*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="開発者が会議の拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::
