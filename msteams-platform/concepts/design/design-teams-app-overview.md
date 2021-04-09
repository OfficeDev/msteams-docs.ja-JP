---
title: カスタム アプリの設計
author: heath-hamilton
description: Microsoft Teams アプリを設計する方法について説明します。 リソースには、Microsoft Teams UI キット、ベスト プラクティス、例などがあります。
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 7a6786cdf9091b04f89ebd6c8bb03799eb7d127a
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634496"
---
# <a name="designing-your-microsoft-teams-app"></a>Microsoft Teams アプリの設計

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams の設計ガイドラインを紹介する概念図。":::

低コード ツールを使用しているデザイナー、製品マネージャー、開発者、メーカーなど、これらのガイドラインは、Microsoft Teams アプリに対して適切な設計上の意思決定を迅速に行うのに役立ちます。

## <a name="teams-app-design-principles"></a>Teams アプリの設計原則

Teams アプリは、ユーザーが一緒に多くの成果を達成するのに役立ちます。 設計をガイドするには、次の原則を使用します。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>共同作業

Teams アプリは、ユーザーが一緒に多くの成果を達成するのに役立ちます。 設計をガイドするには、次の原則を使用します。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>信頼できる

アプリは安全で準拠しています。 ユーザーは、プライバシーに関する情報を簡単に見つくことができます。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>グローバルに包括的

すべてのバックグラウンド、スキルセット、および専門分野のユーザーは、アプリを使用できます。 文化的、人種的、社会的に認識しています。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>低負荷

このアプリは、Teams ワークフローと組み合うコア シナリオに焦点を当てしています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>ネイティブまたは個別

アプリは、ネイティブの Teams デザイン コンポーネントまたは独自のコンポーネントを使用します。 配色、コントロールなどのブレンドはありません。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>役に立つ

アプリは、Teams でユーザーが行う必要があるシナリオに基づいて作成されます。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>使いやすい

UI はわかりやすいので、見た目とトーンが快適で、ユーザーの生産性が向上します。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>速い

アプリはデバイスであり、画面に依存しない。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>アクセシビリティ

アプリは、色のコントラスト、ナビゲーションの選択肢など、Teams のアクセシビリティ要件を満たしています。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>よく説明

テキスト、アイコン、画像を使用すると、アプリが何を使用し、どのように使うのかを明確にできます。

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>一つ一つのエクスペリエンスを作成する

Teams アプリの設計は、従来の Web アプリの設計と似たものですが、少し異なります。 効果的な設計は、Teams の機能とコンテキストに自然に適合しながら、アプリの固有の属性を強調します。

これらのガイドラインとリソースは、バランスを取る際に役立ちます。 Teams アプリを設計する際の操作と回避方法 (タブ内のマルチレベル ナビゲーションなど) が分かっています。

## <a name="planning-your-app"></a>アプリの計画

高品質の Teams アプリを設計するには、まずアプリで実行する操作と、ユーザーがアプリを使用すると思う方法を理解する必要があります。 まだ計画していない場合は、アプリを適切に計画 [するために少し時間を取ってください](../../concepts/extensibility-points.md)。

## <a name="design-fundamentals"></a>デザインの基本事項

レイアウト、 [配色など、Teams](design-teams-app-fundamentals.md)アプリ設計の基本について学習します。

## <a name="basic-fluent-ui-components-for-teams"></a>Teams の基本的な Fluent UI コンポーネント

Fluent UI に基づいて、これらは使い慣れた Teams インターフェイス [を作成するための主要な要素です](design-teams-app-basic-ui-components.md)。

## <a name="ui-templates"></a>UI テンプレート

一般的な Teams の使用例とワークフロー用のテンプレートを使用して、複雑で忠実度の高いデザイン [をすばやく作成できます](design-teams-app-ui-templates.md)。

## <a name="app-capabilities"></a>アプリの機能

ユーザーが Teams アプリを追加、使用、および管理して、デザイン内の各機能を有効に利用する方法を理解します。

* [個人用アプリ](../../concepts/design/personal-apps.md)
* [タブ](../../tabs/design/tabs.md)
* [メッセージング拡張機能](../../messaging-extensions/design/messaging-extension-design.md)
* [ボット](../../bots/design/bots.md)
* [ミーディング拡張機能](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [アダプティブ カード](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a>アプリのカスタマイズ

Teams 管理者が組織のニーズに基づいてアプリをカスタマイズまたは再ブランド化する方法を理解します。 このカスタマイズは、マニフェスト スキーマで定義 `configurableProperties` する場合に有効になります。 詳細については [、「Microsoft Teams でアプリをカスタマイズする」を参照してください](/MicrosoftTeams/customize-apps)。

> [!NOTE]
> この機能は現在、開発者プレビューでのみ利用できます。
> 
> アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれたアプリの外観を変更できます。 たとえば、Teams 管理者が Contoso から *Contoso Agent* にアプリの名前をカスタマイズすると、そのアプリは Contoso *Agent* という新しい名前でユーザーに表示されます。 ただし、チャットにコネクタを追加している間、一覧でコネクタは引き続きアプリの名前を Contoso として表示 *します*。
> 
> ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。 詳細については [、「Microsoft Teams でのアプリのカスタマイズ」を参照してください](/MicrosoftTeams/customize-apps)。

## <a name="tools-and-samples"></a>ツールとサンプル

次のツールは、デザイナーと開発者が始めるのに役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

UI コンポーネント、テンプレート、および必要に応じてドラッグ、ドロップ、および変更できる例を使用して Teams アプリを設計します。 UI キットには、さまざまな Teams シナリオでのアプリの外観と動作に関する包括的な情報も含まれています。

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

### <a name="fluent-ui-documentation"></a>Fluent UI のドキュメント

Teams エクスペリエンスの構築に使用する Fluent UI ベースのコンポーネントのコード サンプルと実装の詳細を取得します。

> [!div class="nextstepaction"]
> [Teams UI コンポーネントを試す (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー

Web ベースのツールでアダプティブ カードを設計します。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)
