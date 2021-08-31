---
title: アプリを設計する - アプリの構造を理解する
description: アプリを設計する際に、アプリでカスタマイズMicrosoft Teamsを理解します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: eb7e26a726313c366765f3ee4fd36aebc064ca78
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408581"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>アプリ構造Microsoft Teams理解する

アプリを構築する際には、アプリでカスタマイズできる機能とカスタマイズできない機能を知Microsoft Teams。 この情報は、コントロールするアプリ エクスペリエンスの部分をよりよく理解するのに役立ちます。

次のワイヤーフレームを使用すると、次の情報が表示されます。

* 各アプリ機能でカスタマイズできるTeams (ピンクで示されています)。
* 各機能がサポートするスコープ。

> [!TIP]
> **スコープとはどういう意味ですか?** スコープは、ユーザーがアプリをTeamsできる領域です。 アプリには、個人、チャネル、チャット、会議など、1 つ以上のスコープを設定できます。

## <a name="personal-apps"></a>個人用アプリ

個人用アプリは、個々のユーザーのアプリ コンテンツをホストする大きなキャンバスを提供します。

***サポートされているスコープ**: 個人用*

### <a name="mobile"></a>モバイル

キャンバスは Web ビューなので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="開発者がモバイル上の個人用アプリ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

### <a name="desktop"></a>デスクトップ

キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="開発者がデスクトップ上の個人用アプリ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

## <a name="tabs"></a>タブ

タブは、ユーザーグループのアプリ コンテンツをホストする大きなキャンバスを提供します。 チャネル、チャット、会議出席招待などの共有スペースにタブを含めることができます。

***サポートされているスコープ**: チャネル、チャット、会議*

### <a name="mobile"></a>モバイル

キャンバスは Web ビューなので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="開発者がモバイル上のタブ用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

### <a name="desktop"></a>デスクトップ

キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="開発者がデスクトップ上のタブ用にカスタマイズTeamsフロントエンド領域を示す概念イメージ。" border="false":::

## <a name="bots"></a>ボット

ボットは、ネイティブ メッセージング機能Teams統合する会話型アプリなので、UI の作業が処理されます。 デザインの観点からは、自然言語処理 (NLP) サポートとアダプティブ カード プラットフォームを使用して、個性、カスタム機能、豊富で操作可能な情報を追加する機会がまだ存在します。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="開発者がモバイル上のボット用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="開発者がデスクトップ上のボット用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

## <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージング拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作したりするためのショートカットです。 アクション ベースのメッセージング拡張機能を使用すると、エクスペリエンスの制御が向上しますが、Teamsベースのメッセージング拡張機能のレンダリングの多くを処理できます。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="開発者がモバイル上のメッセージング拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="開発者がデスクトップ上のメッセージング拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

## <a name="meeting-extensions"></a>ミーディング拡張機能

会議拡張機能は、ライブ会議を強化するアプリです。 会議の前、中、後など、いくつかのシナリオでアプリ コンテンツをホストできます。

***サポートされているスコープ**: 会議、チャット*

### <a name="mobile"></a>モバイル

サーフェスは Web ビューで、エクスペリエンスをカスタマイズできますが、会議中にこれらのアプリは暗いテーマを使用することを念頭に置いておきます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="開発者がモバイルでの会議拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::

### <a name="desktop"></a>デスクトップ

サーフェスは iframe であり、エクスペリエンスをカスタマイズできますが、会議中にこれらのアプリは暗いテーマを使用し、狭いという念頭に置いておきます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="開発者がデスクトップ上の会議拡張機能用にカスタマイズTeamsフロントエンド領域を示す概念的なイメージ。" border="false":::
