---
title: カスタム アプリの設計
author: heath-hamilton
description: Microsoft Teams アプリの設計方法はこちら。 リソースには、Microsoft Teams UI キット、ベスト プラクティス、例などが含まれます。
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 8e417a59e03fbb57905e2a84490888b8f98a5435
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111277"
---
# <a name="designing-your-microsoft-teams-app"></a>Microsoft Teams のアプリの設計

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams の設計ガイドラインを紹介する概念画像。":::

ローコード ツールを使用しているデザイナー、製品マネージャー、開発者、メーカーのいずれであっても、これらのガイドラインは、Microsoft Teams アプリに適した設計上の決定をすばやく行うのに役立ちます。

## <a name="creating-a-cohesive-experience"></a>まとまりのあるエクスペリエンスを作成する

Teams アプリの設計は、従来の Web アプリ—の設計に似ていますが、少し異なります。 効果的な設計では、Teams の機能とコンテキストに自然に適合しながら、アプリ固有の属性を強調表示します。

これらのガイドラインとリソースは、そのバランスを取るのに役立ちます。 Teams アプリを設計する際の対処方法と回避する方法 (タブ内の複数レベルのナビゲーションなど) を理解できます。

## <a name="teams-app-design-principles"></a>Teams アプリの設計原則

Teams アプリは、ユーザーがより一緒により多くのことを達成するのに役立ちます。 これらの原則を使用して、設計をガイドします。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>コラボレーション

Teams アプリは、ユーザー間の最適化された共有アクティビティを通じてコラボレーションを促進します。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>信頼できる

アプリはセキュリティで保護され、準拠しています。 ユーザーはプライバシーに関する情報を簡単に見つけることができます。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>グローバルに包括的である

あらゆる背景、スキルセット、および分野のユーザーがアプリを使用できます。 文化的、人種的、および社会的に認識されます。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>低負荷

アプリは、Teams ワークフローと融合するコアシナリオに焦点を当てています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>ネイティブまたは個別

アプリでは、ネイティブの Teams デザイン コンポーネントまたは独自のコンポーネントが使用されます。 配色、コントロールなどを組み合わせたものはありません。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>役に立つ

アプリは、ユーザーが Teams で行う必要があるシナリオに基づいています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>使いやすい

UI は理解しやすく、見た目とトーンが楽しく、ユーザーの生産性が向上させます。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>応答性が高い

アプリはデバイスや画面に依存しません。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>アクセシビリティ

このアプリは、色のコントラスト、ナビゲーションの代替手段などの点で、Teams のアクセシビリティ要件を満たしています。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>よく説明されています

テキスト、アイコンおよび画像によって、アプリの用途と使用方法が明確になります。

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a>Teams の設計システム

レイアウト、配色など、[Teams アプリの設計の基礎](design-teams-app-fundamentals.md)について説明します。

## <a name="app-capabilities"></a>アプリの機能

ユーザーが Teams アプリを追加、使用、管理して、設計の各機能を最大限に活用する方法について説明します。

* [個人用アプリ](../../concepts/design/personal-apps.md)
* [タブ](../../tabs/design/tabs.md)
* [メッセージの拡張機能](../../messaging-extensions/design/messaging-extension-design.md)
* [ボット](../../bots/design/bots.md)
* [ミーディング拡張機能](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a>UI テンプレート

[Teams の一般的なユース ケースとワークフロー用の テンプレート](design-teams-app-ui-templates.md)を使用して、複雑で忠実度の高いデザインをすばやく作成します。

## <a name="basic-ui-components"></a>基本的な UI コンポーネント

Fluent UI に基づいて、これらは、Teams エクスペリエンスをゼロから作成するために使用できる[コア要素](design-teams-app-basic-ui-components.md)です。

## <a name="tools-and-samples"></a>ツールとサンプル

以下のツールは、デザイナーや開発者が作業を開始するのに役立ちます:

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じてドラッグ、ドロップ、変更できる UI コンポーネント、テンプレート、および例を使用して、Teams アプリを設計します。 UI キットには、さまざまな Teams シナリオでのアプリの外観と動作に関する包括的な情報も含まれています。

> [!div class="nextstepaction"]
> [UI キットを取得する (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams UI ライブラリ

ブラウザーで個々の Teams UI テンプレートと関連コンポーネントを表示してテストします。

> [!div class="nextstepaction"]
> [UI ライブラリ (プレイグラウンド)を試す](https://dev-int.teams.microsoft.com/storybook/main/index.html)

これらのテンプレートと関連コンポーネントを Teams アプリ プロジェクトに直接インポートします。

> [!div class="nextstepaction"]
> [UI ライブラリ (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)を取得する

### <a name="sample-app"></a>サンプル アプリ

サンプル アプリをアップロードして、Teams クライアントでのアプリの外観と動作を確認できます。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>その他のリソース

詳細については、次のいずれかのリソースを試してください:

### <a name="fluent-ui-documentation"></a>Fluent UI のドキュメント

Teams エクスペリエンスの構築に使用される基本的な Fluent UI コンポーネントのコード サンプルと実装の詳細を取得します。

> [!div class="nextstepaction"]
> [Teams UI コンポーネント (Fluent UI)を試す](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー。

Web ベースのツールでアダプティブ カードを設計します。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)

## <a name="see-also"></a>関連項目

* [Teams 会議用アプリを有効化して構成する](../../apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
* [Microsoft Teams のボットをデザインする](~/bots/design/bots.md)
* [仮想アシスタントを作成する](~/samples/virtual-assistant.md)
* [Microsoft Teams のアプリのタスク モジュールの設計](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)
