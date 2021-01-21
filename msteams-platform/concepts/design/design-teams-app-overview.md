---
title: カスタム アプリの設計
author: heath-hamilton
description: Microsoft Teams アプリを設計する方法について説明します。 リソースには、Microsoft Teams UI Kit、ベスト プラクティス、例などがあります。
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0c791b1e4733cd2a015e443ca5c4d0c433dd4d31
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911906"
---
# <a name="designing-your-microsoft-teams-app"></a>Microsoft Teams アプリの設計

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams の設計ガイドラインを紹介する概念イメージ。":::

設計者、製品マネージャー、開発者、またはメーカーが低コードツールを使用している場合でも、これらのガイドラインは、Microsoft Teams アプリの適切な設計上の決定をすばやく行うのに役立ちます。

## <a name="teams-app-design-principles"></a>Teams アプリ設計の原則

Teams アプリは、ユーザーが一緒にもっと多くの成果を達成するのに役立ちます。 これらの原則を使用して、設計をガイドします。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>Collaborative

Teams アプリは、ユーザーが一緒にもっと多くの成果を達成するのに役立ちます。 これらの原則を使用して、設計をガイドします。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>信頼できる

アプリはセキュリティで保護され、準拠しています。 ユーザーはプライバシーに関する情報を簡単に検索できます。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>グローバルに包括

すべてのバックグラウンド、スキルセット、および分野のユーザーがアプリを使用できます。 文化的、人種的、社会的な認識を持つ。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>低負荷

このアプリは、Teams のワークフローとブレンドするコア シナリオに重点を当てはっています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>ネイティブまたは個別

アプリは、ネイティブの Teams 設計コンポーネントまたは独自のコンポーネントを使用します。 配色、コントロールなどのブレンドはありません。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>役に立つ

アプリは、ユーザーが Teams で行う必要があるシナリオに基づいて作成されます。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>使いやすい

UI は理解が容易で、外観とトーンが楽で、ユーザーの生産性が向上します。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>速い

アプリはデバイスと画面に依存しない。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>アクセシビリティ

このアプリは、色コントラストやナビゲーションの代替手段など、Teams のアクセシビリティ要件を満たしています。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>よく説明されています

テキスト、アイコン、画像を使って、アプリの意味と使い方を明確に示します。

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>コーヒーティブ なエクスペリエンスの作成

Teams アプリの設計は、従来の Web アプリの設計に似たものですが、少し異なります。 効果的な設計では、Teams の機能やコンテキストに自然に適合しながら、アプリの固有の属性を強調します。

これらのガイドラインとリソースは、そのバランスを取る際に役立ちます。 Teams アプリを設計する際の対応方法と避ける必要がある操作 (タブ内の複数レベルのナビゲーションなど) を確認できます。

## <a name="planning-your-app"></a>アプリの計画

高品質の Teams アプリを設計するには、まず、アプリが何を行い、ユーザーがアプリを使用すると思うのかを理解する必要があります。 まだ計画していない場合は、しばらく時間を取ってアプリを [適切に計画してください](../../concepts/extensibility-points.md)。

## <a name="design-fundamentals"></a>デザインの基本事項

レイアウト [、配色など、Teams](design-teams-app-fundamentals.md)アプリ設計の基本について学習します。

## <a name="basic-fluent-ui-components-for-teams"></a>Teams の基本的な Fluent UI コンポーネント

Fluent UI に基づいて、これらは使い慣れた Teams インターフェイスを作成 [するための主要な要素です](design-teams-app-basic-ui-components.md)。

## <a name="ui-templates"></a>UI テンプレート

一般的な Teams の使用事例とワークフロー用のテンプレートを使用して、複雑で忠実な [設計をすばやく作成できます](design-teams-app-ui-templates.md)。

## <a name="app-capabilities"></a>アプリの機能

ユーザーが Teams アプリを追加、使用、管理して、設計の各機能を有効に利用する方法について説明します。

* [個人用アプリ](../../concepts/design/personal-apps.md)
* [タブ](../../tabs/design/tabs.md)
* [メッセージング拡張機能](../../messaging-extensions/design/messaging-extension-design.md)
* [ボット](../../bots/design/bots.md)
* [ミーディング拡張機能](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [アダプティブ カード](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="tools-and-samples"></a>ツールとサンプル

以下のツールは、デザイナーや開発者の使用を開始するのに役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じてドラッグ、ドロップ、変更できる UI コンポーネント、テンプレート、例を含む Teams アプリを設計します。 UI キットには、さまざまな Teams シナリオでのアプリの外観と動作に関する包括的な情報も含まれています。

> [!div class="nextstepaction"]
> [UI キットを取得する (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams UI ライブラリ

ブラウザーで個々の Teams UI テンプレートと関連コンポーネントを表示およびテストします。

> [!div class="nextstepaction"]
> [UI ライブラリ (プレイグラウンド) を試す](https://dev-int.teams.microsoft.com/storybook/main/index.html)

これらのテンプレートと関連コンポーネントを Teams アプリ プロジェクトに直接インポートします。

> [!div class="nextstepaction"]
> [UI ライブラリを取得する (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>サンプル アプリ

サンプル アプリをインストールして、Teams コンテキスト内での UI テンプレートの外観と動作を確認します。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>その他のリソース

詳細については、次のいずれかのリソースを試してください。

### <a name="fluent-ui-documentation"></a>Fluent UI ドキュメント

Teams エクスペリエンスの構築に使用される Fluent UI ベースのコンポーネントのコード サンプルと実装の詳細を取得します。

> [!div class="nextstepaction"]
> [Teams UI コンポーネントを試す (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー

Web ベースのツールでアダプティブ カードを設計します。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)
