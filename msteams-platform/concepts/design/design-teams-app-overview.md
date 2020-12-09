---
title: カスタムアプリを設計する
author: heath-hamilton
description: Microsoft Teams アプリを設計する方法について説明します。 リソースには、Microsoft Teams UI Kit、ベストプラクティス、例などが含まれます。
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0160a59ed4ebc51e900acbb5d74735ccae0b6083
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606015"
---
# <a name="designing-your-microsoft-teams-app"></a>Microsoft Teams アプリを設計する

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams 設計ガイドラインの概要を説明するイメージ。":::

低コードツールを使用して、デザイナー、製品マネージャー、開発者、または開発者であるかどうかにかかわらず、これらのガイドラインは、Microsoft Teams アプリに対して適切な設計上の決定を迅速に行うのに役立ちます。

## <a name="teams-app-design-principles"></a>Teams アプリ設計の原則

Teams アプリは、ユーザーがより多くのことを実現するのに役立ちます。 設計をガイドするには、これらの原則を使用します。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>業務

Teams アプリは、ユーザーがより多くのことを実現するのに役立ちます。 設計をガイドするには、これらの原則を使用します。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>信用

アプリはセキュリティで保護され、準拠しています。 ユーザーは、プライバシーに関する情報を簡単に見つけることができます。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>グローバル包括

すべての背景、skillsets、および分野の人々は、アプリを使用できます。 カルチャ、racially、および socially に対応します。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>低負荷

アプリは、Teams ワークフローと組み合わせたコアシナリオに重点を置いています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>ネイティブまたは個別

アプリでは、ネイティブの Teams デザインコンポーネントまたは独自のコンポーネントを使用します。 配色パターン、コントロールなどは混在していません。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>とき

アプリは、ユーザーが Teams で行う必要のあるシナリオに基づいています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>使いやすい

UI は、わかりやすく、ルックアンドトーンがよく、ユーザーの生産性を向上させるのに役立ちます。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>速い

アプリはデバイスと画面に依存しません。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>アクセシビリティ

アプリは、色のコントラスト、移動方法など、Teams のアクセシビリティ要件を満たしています。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>よく説明

テキスト、アイコン、画像によって、アプリの用途と使用方法が明確になります。

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>凝集した環境を作成する

Teams アプリを設計することは、従来の web アプリの設計に似ていますが、多少異なるものです。 効果的なデザインでは、アプリの一意の属性を強調表示する一方で、Teams の機能やコンテキストを自然に調整します。

これらのガイドラインとリソースは、そのバランスを取るのに役立ちます。 Teams アプリを設計するときに何ができるか、何を回避するか (タブ内の複数レベルのナビゲーションなど) について説明します。

## <a name="planning-your-app"></a>アプリを計画する

高品質 Teams アプリを設計するには、まず、アプリに対して実行する操作とその使用方法を理解する必要があります。 まだ作業していない場合は、アプリを正しく [計画](../../concepts/extensibility-points.md)するためにしばらく時間がかかります。

## <a name="design-fundamentals"></a>設計の基礎

レイアウト、配色など、 [Teams アプリデザインの基本事項](design-teams-app-fundamentals.md)について説明します。

## <a name="basic-fluent-ui-components-for-teams"></a>Teams の基本的な Fluent UI コンポーネント

Fluent UI に基づいて、これらは [一般的な Teams インターフェイスを作成するための中心的な要素](design-teams-app-basic-ui-components.md)です。

## <a name="app-capabilities"></a>アプリの機能

ユーザーがチームアプリを追加、使用、および管理して、設計の各機能を最大限に活用する方法について理解します。

* [個人用アプリ](../../concepts/design/personal-apps.md)
* [タブ](../../tabs/design/tabs.md)
* [メッセージング拡張機能](../../messaging-extensions/design/messaging-extension-design.md)
* [ボット](../../bots/design/bots.md)
* [会議の内線番号](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [アダプティブ カード](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="ui-templates"></a>UI テンプレート

[一般的な Teams のユースケースとワークフローのテンプレート](design-teams-app-ui-templates.md)を使用して、複雑で忠実なデザインをすばやく作成できます。

## <a name="get-started-with-the-microsoft-teams-ui-kit"></a>Microsoft Teams UI キットを使用して作業を開始する

Microsoft Teams UI キットには、UI コンポーネント、テンプレート、および、必要に応じてドラッグ、ドロップ、および変更できる例があります。 UI キットには、さまざまな Teams シナリオでのアプリの外観や動作に関する包括的な情報も含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="other-resources"></a>その他のリソース

詳細については、次のいずれかのリソースを参照してください。

### <a name="fluent-ui"></a>Fluent UI

Teams エクスペリエンスの構築に使用される Fluent UI ベースコンポーネントのコードサンプルと実装の詳細を取得します。

> [!div class="nextstepaction"]
> [Teams UI コンポーネントを試す (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>アダプティブカードデザイナー

Web ベースのツールでアダプティブカードをデザインします。

> [!div class="nextstepaction"]
> [アダプティブカードデザイナーを試す](https://adaptivecards.io/designer/)
