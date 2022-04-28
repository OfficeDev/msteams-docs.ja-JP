---
title: アプリを設計する - アプリ構造を理解する
description: アプリの設計時にMicrosoft Teamsでカスタマイズできることとカスタマイズできないことを理解します。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
keywords: ワイヤーフレーム チャネル チャット会議メッセージ拡張機能モバイル デスクトップ
ms.openlocfilehash: 8353fa74dce12642e5ca96c85c34dc06fc0da203
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103286"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Microsoft Teams アプリの構造を理解する

アプリをビルドするときは、Microsoft Teamsでカスタマイズできることとカスタマイズできないことを把握することが重要です。 この情報は、制御するアプリ エクスペリエンスのどの部分を理解するのに役立ちます。

次のワイヤーフレームが表示されます。

* 各Teamsアプリ機能でカスタマイズできるサーフェス (ピンクで囲まれています)。
* 各機能がサポートするスコープ。

> [!TIP]
> **スコープとは何を意味しますか?** スコープは、ユーザーがアプリを使用できるTeamsの領域です。 アプリには、個人用、チャネル、チャット、会議など、1 つまたは複数のスコープを設定できます。

## <a name="personal-apps"></a>個人用アプリ

個人用アプリは、個々のユーザーのアプリ コンテンツをホストするための大きなキャンバスを提供します。

***サポートされているスコープ**: Personal*

### <a name="mobile"></a>Mobile

キャンバスは Web ビューであるため、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="開発者がモバイル上の個人用アプリ用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

### <a name="desktop"></a>Desktop

キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="開発者がデスクトップ上の個人用アプリ用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

## <a name="tabs"></a>タブ

タブは、ユーザーのグループのアプリ コンテンツをホストするための大きなキャンバスを提供します。 共有スペースには、チャネル、チャット、会議出席依頼などのタブを含めることができます。

***サポートされているスコープ**: チャネル、チャット、会議*

### <a name="mobile"></a>Mobile

キャンバスは Web ビューであるため、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="開発者がモバイル上のタブ用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

### <a name="desktop"></a>Desktop

キャンバスは iframe なので、エクスペリエンスを完全にカスタマイズできます。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="開発者がデスクトップ上のタブ用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

## <a name="bots"></a>ボット

ボットは、Teamsネイティブ メッセージング機能と統合された会話型アプリであるため、UI 作業が自動的に処理されます。 デザインの観点からは、自然言語処理 (NLP) のサポートとアダプティブ カード プラットフォームを使用して、パーソナリティ、カスタム機能、豊富で実用的な情報を追加する機会はまだあります。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="開発者がモバイルでボット用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="開発者がデスクトップ上のボット用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

## <a name="message-extensions"></a>メッセージ拡張機能

メッセージ拡張機能は、アプリ コンテンツを挿入したり、会話から離れることなくメッセージを操作したりするためのショートカットです。 アクション ベースのメッセージ拡張機能を使用すると、エクスペリエンスをより詳細に制御できますが、Teamsは検索ベースのメッセージ拡張機能のレンダリングの多くを処理します。

***サポートされているスコープ**: 個人用、チャネル、チャット、会議*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="開発者がモバイルでメッセージ拡張機能をカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="開発者がデスクトップ上のメッセージ拡張機能用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

## <a name="meeting-extensions"></a>ミーディング拡張機能

会議の拡張機能は、ライブ会議を強化するためのアプリです。 会議の前、中、後など、いくつかのシナリオでアプリ コンテンツをホストできます。

***サポートされているスコープ**: 会議、チャット*

### <a name="mobile"></a>Mobile

サーフェスは Web ビューであり、エクスペリエンスをカスタマイズできますが、会議中にこれらのアプリはダーク テーマを使用することに注意してください。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="開発者がモバイルで会議拡張機能用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::

### <a name="desktop"></a>Desktop

サーフェスは iframe であり、エクスペリエンスをカスタマイズできますが、会議中にこれらのアプリは暗いテーマを使用し、狭い点に注意してください。

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="開発者がデスクトップ上の会議拡張機能用にカスタマイズできるTeamsのフロントエンド領域を示す概念図。" border="false":::
