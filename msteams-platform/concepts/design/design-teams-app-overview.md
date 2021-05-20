---
title: カスタム アプリの設計
author: heath-hamilton
description: Microsoft Teamsアプリを設計する方法については、こちらをご覧ください。 リソースには、Microsoft Teams UI キット、ベスト プラクティス、例などが含まれます。
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565117"
---
# <a name="designing-your-microsoft-teams-app"></a>Microsoft Teams アプリの設計

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams設計ガイドラインを紹介する概念図。":::

デザイナー、プロダクト マネージャー、開発者、またはメーカーが低コード ツールを使用している場合でも、これらのガイドラインは、Microsoft Teams アプリに適したデザインの決定をすばやく行う上で役立ちます。

## <a name="teams-app-design-principles"></a>Teamsアプリの設計原則

Teamsアプリは、人々がより多くを一緒に達成するのに役立ちます。 これらの原則を使用して、設計を導きます。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>コラボレイティブ

Teamsアプリは、人々がより多くを一緒に達成するのに役立ちます。 これらの原則を使用して、設計を導きます。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>頼もしい

アプリは安全で準拠しています。 ユーザーは、プライバシーに関する情報を簡単に見つけることができます。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>グローバルインクルーシブ

すべての背景、スキルセット、および専門分野のユーザーは、アプリを使用することができます。 それは文化的、人種的、社会的に認識しています。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>低負荷

アプリは、Teamsワークフローとブレンドコア シナリオに焦点を当てています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>ネイティブまたは個別

アプリは、ネイティブTeams設計コンポーネントまたは独自のコンポーネントを使用します。 配色やコントロールなどのブレンドはありません。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>便利

アプリは、ユーザーがTeamsで行う必要があるシナリオに基づいています。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>使いやすい

UI は理解しやすく、見た目やトーンが楽しく、人々の生産性を向上させます。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>速い

アプリはデバイスと画面に依存しません。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>アクセシビリティ

アプリは、色のコントラスト、ナビゲーションの代替、および多くの点でTeamsアクセシビリティ要件を満たしています。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>よく説明

テキスト、アイコン、および画像により、アプリの目的と使用方法が明確になります。

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>まとまりのあるエクスペリエンスを作成する

Teamsアプリの設計は、従来の Web アプリの設計と似ていますが、少し異なります。 効果的なデザインでは、アプリの独自の属性を強調しながら、Teams機能とコンテキストに自然に適合します。

これらのガイドラインとリソースは、そのバランスを取る際に役立ちます。 Teams アプリを設計する際の操作と回避方法 (タブ内の複数レベルのナビゲーションなど) を把握できます。

## <a name="planning-your-app"></a>アプリの計画

高品質のTeamsアプリを設計するには、まずアプリの実行方法と、アプリの使用方法を理解する必要があります。 まだお持ちの場合は、しばらく時間をかけて [アプリを適切に計画してください](../../concepts/extensibility-points.md)。

## <a name="design-fundamentals"></a>デザインの基本事項

レイアウト[、配色など、Teamsアプリデザインの基本](design-teams-app-fundamentals.md)について説明します。

## <a name="basic-fluent-ui-components-for-teams"></a>Teams用の基本的な Fluent UI コンポーネント

Fluent UI に基づいて、これらは[使い慣れたTeamsインターフェイスを作成するためのコア要素です](design-teams-app-basic-ui-components.md)。

## <a name="ui-templates"></a>UI テンプレート

[一般的なTeamsのユースケースやワークフロー用のテンプレート](design-teams-app-ui-templates.md)を使用して、複雑で忠実度の高いデザインをすばやく作成できます。

## <a name="app-capabilities"></a>アプリの機能

デザインの各機能を最大限に活用するために、Teamsアプリの追加、使用、管理の方法を理解します。

* [個人用アプリ](../../concepts/design/personal-apps.md)
* [タブ](../../tabs/design/tabs.md)
* [メッセージング拡張機能](../../messaging-extensions/design/messaging-extension-design.md)
* [ボット](../../bots/design/bots.md)
* [ミーディング拡張機能](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [アダプティブ カード](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a>アプリのカスタマイズ

Teams管理者が組織のニーズに応じてアプリをカスタマイズまたはブランド変更する方法を理解します。 このカスタマイズは、マニフェスト スキーマで を定義する場合 `configurableProperties` に有効になります。 詳しくは[、Microsoft Teamsでのアプリのカスタマイズを](/MicrosoftTeams/customize-apps)参照してください。

> [!NOTE]
> アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれるアプリのルック アンド フィールを変更できます。 たとえば、Teams管理者が *Contoso* から *Contoso エージェント* にアプリの名前をカスタマイズすると、アプリは新しい名前の *Contoso エージェント* をユーザーに表示されます。 ただし、チャットにコネクタを追加する間は、一覧に表示されるコネクタには、Contoso *というアプリ* の名前が表示されます。
> 
> ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。 詳細については、「 [Microsoft Teams でアプリをカスタマイズする](/MicrosoftTeams/customize-apps)」を参照してください。

## <a name="tools-and-samples"></a>ツールとサンプル

デザイナーや開発者が使い始めるには、次のツールが役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じてドラッグ、ドロップ、および変更できる UI コンポーネント、テンプレート、例を使用して、Teamsアプリを設計します。 UI キットには、さまざまなTeamsシナリオでアプリがどのように見え、動作するかについての包括的な情報も含まれています。

> [!div class="nextstepaction"]
> [UIキットを入手する(Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft TeamsUI ライブラリ

ブラウザーで個々のTeams UI テンプレートおよび関連コンポーネントを表示およびテストします。

> [!div class="nextstepaction"]
> [UIライブラリ(プレイグラウンド)を試してみてください](https://dev-int.teams.microsoft.com/storybook/main/index.html)

これらのテンプレートと関連コンポーネントをTeams アプリ プロジェクトに直接インポートします。

> [!div class="nextstepaction"]
> [UI ライブラリを取得する (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>サンプル アプリ

サンプル アプリをインストールして、UI テンプレートの外観と動作をTeamsコンテキストで確認します。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>その他のリソース

詳細については、次のいずれかのリソースを試してください。

### <a name="fluent-ui-documentation"></a>流暢な UI ドキュメント

Teams エクスペリエンスの構築に使用される Fluent UI ベースのコンポーネントのコード サンプルと実装の詳細を取得します。

> [!div class="nextstepaction"]
> [UI コンポーネントTeams試す (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>アダプティブカードデザイナー

アダプティブカードは、ウェブベースのツールでデザインできます。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)
