---
title: アプリを設計する - アプリ構造を理解する
description: このモジュールでは、アプリ構造を設計するときに Microsoft Teams でカスタマイズできることとカスタマイズできないことについて説明します。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 6a409accc5f55aa0a9c245aa061efde5b67d81f3
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558759"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Microsoft Teams アプリの構造を理解する

アプリをビルドするときは、Microsoft Teams でカスタマイズできることとカスタマイズできないことを把握することが重要です。 この情報は、アプリ エクスペリエンスのどの部分を制御しているかをよりよく理解するのに役立ちます。

次のワイヤーフレームが表示されます。

* 各 Teams アプリ機能でカスタマイズできるサーフェス (ピンクで囲まれています)。
* 各機能がサポートするスコープ。

> [!TIP]
> **スコープとは** スコープは、ユーザーがアプリを使用できる Teams の領域です。 アプリには、個人用、チャネル、チャット、会議など、1 つまたは複数のスコープを設定できます。

## <a name="personal-apps"></a>個人用アプリ

個人用アプリは、個々のユーザーのアプリ コンテンツをホストするための大きなキャンバスを提供します。

***サポートされているスコープ**: Personal*

### <a name="mobile"></a>Mobile

キャンバスは Web ビューであるため、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="開発者がモバイル上の個人用アプリ用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

### <a name="desktop"></a>Desktop

キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="開発者がデスクトップ上の個人用アプリ用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

## <a name="tabs"></a>タブ

タブは、ユーザーのグループのアプリ コンテンツをホストするための大きなキャンバスを提供します。 共有スペースには、チャネル、チャット、会議出席依頼などのタブを含めることができます。

***サポートされているスコープ**: チャネル、チャット、会議*

### <a name="mobile"></a>Mobile

キャンバスは Web ビューであるため、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="開発者がモバイル上のタブ用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

### <a name="desktop"></a>Desktop

キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="開発者がデスクトップ上のタブ用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

## <a name="bots"></a>ボット

ボットは、Teams ネイティブ メッセージング機能と統合された会話型アプリであるため、UI 作業が自動的に処理されます。 デザインの観点からは、自然言語処理 (NLP) のサポートとアダプティブ カード プラットフォームを使用して、パーソナリティ、カスタム機能、豊富で実用的な情報を追加する機会はまだあります。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="開発者がモバイルでボット用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="開発者がデスクトップ上のボット用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

## <a name="message-extensions"></a>メッセージの拡張機能

メッセージ拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作したりするためのショートカットです。 アクション ベースのメッセージ拡張機能を使用すると、エクスペリエンスをより詳細に制御できますが、Teams は検索ベースのメッセージ拡張機能のレンダリングの多くを処理します。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="開発者がモバイルでメッセージ拡張機能をカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="開発者がデスクトップ上のメッセージ拡張機能用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

## <a name="meeting-extensions"></a>ミーディング拡張機能

会議の拡張機能は、ライブ会議を強化するためのアプリです。 会議の前、中、後など、いくつかのシナリオでアプリ コンテンツをホストできます。

***サポートされているスコープ**: 会議、チャット*

### <a name="mobile"></a>Mobile

サーフェスは Web ビューであり、エクスペリエンスをカスタマイズできますが、会議中にこれらのアプリはダーク テーマを使用することに注意してください。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="開発者がモバイルで会議拡張機能用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::

### <a name="desktop"></a>Desktop

サーフェスは iframe であるため、エクスペリエンスをカスタマイズできますが、会議中はこれらのアプリはダーク テーマを使用し、幅が狭いことに注意してください。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="開発者がデスクトップ上の会議拡張機能用にカスタマイズできる Teams のフロントエンド領域を示す概念図。":::
