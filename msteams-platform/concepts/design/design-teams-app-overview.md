---
title: カスタム アプリの設計
author: heath-hamilton
description: アプリを設計するMicrosoft Teamsします。 リソースには、MICROSOFT TEAMS UI キット、ベスト プラクティス、例などがあります。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 7a7a6d380341c94f4ed2eef92bf4407ac1a7681f
ms.sourcegitcommit: ca902f505a125641c379a917ee745ab418bd1ce6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2022
ms.locfileid: "63466529"
---
# <a name="designing-your-microsoft-teams-app"></a>アプリのMicrosoft Teamsする

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="設計ガイドラインに関するMicrosoft Teams概念図。":::

低コード ツールを使用しているデザイナー、製品マネージャー、開発者、メーカーなど、これらのガイドラインは、Microsoft Teams アプリに対して適切な設計上の意思決定を迅速に行うのに役立ちます。

## <a name="creating-a-cohesive-experience"></a>一つ一つのエクスペリエンスを作成する

アプリのTeamsは、従来の Web アプリの設計と同じですが、少し異なります。 効果的な設計では、アプリの固有の属性を強調しながら、アプリの機能やコンテキストTeams自然に適合します。

これらのガイドラインとリソースは、バランスを取る際に役立ちます。 アプリを設計する際に何を行い、何をTeamsか確認できます (タブ内の複数レベルのナビゲーションなど)。

## <a name="teams-app-design-principles"></a>Teamsの設計原則

Teamsアプリは、ユーザーが一緒に達成するのに役立ちます。 設計をガイドするには、次の原則を使用します。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>共同作業

Teamsアプリは、ユーザー間で協調的で共有されたアクティビティを通じてコラボレーションを促進します。

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

アプリは、ワークフローとブレンドするコア シナリオTeamsします。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>ネイティブまたは個別

アプリは、ネイティブ のTeamsコンポーネントまたは独自のコンポーネントを使用します。 配色、コントロールのブレンドなどはありません。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>役に立つ

アプリは、ユーザーがユーザーが必要とするシナリオに基づいて、Teams。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>使いやすい

UI はわかりやすいので、見た目とトーンが快適で、ユーザーの生産性が向上します。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>応答性が高い

アプリは、デバイスと画面に依存しないです。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>アクセシビリティ

このアプリは、Teamsコントラスト、ナビゲーションの代替など、ユーザー補助の要件を満たしています。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>よく説明

テキスト、アイコン、画像を使用すると、アプリが何を使用し、どのように使うのかを明確にできます。

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a>Teams設計システム

レイアウト[、配色Teamsなど、](design-teams-app-fundamentals.md)アプリ設計の基本について学習します。

## <a name="app-capabilities"></a>アプリの機能

ユーザーがアプリを追加、使用、管理する方法Teams設計の各機能を有効に利用する方法を理解します。

* [個人用アプリ](../../concepts/design/personal-apps.md)
* [タブ](../../tabs/design/tabs.md)
* [メッセージング拡張機能](../../messaging-extensions/design/messaging-extension-design.md)
* [ボット](../../bots/design/bots.md)
* [ミーディング拡張機能](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a>UI テンプレート

一般的な使用例やワークフロー用のテンプレートを使用して、複雑で忠実度[の高いTeams迅速に作成できます](design-teams-app-ui-templates.md)。

## <a name="basic-ui-components"></a>基本的な UI コンポーネント

これらの要素はFluent UI に基づいて、ユーザーエクスペリエンス[](design-teams-app-basic-ui-components.md)をゼロから作成Teams要素です。

## <a name="tools-and-samples"></a>ツールとサンプル

次のツールは、デザイナーと開発者が始めるのに役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

UI コンポーネントTeamsテンプレート、および必要に応じてドラッグ、ドロップ、および変更できる例を含むアプリを設計します。 UI キットには、さまざまなシナリオでのアプリの外観と動作に関する包括的なTeams含まれています。

> [!div class="nextstepaction"]
> [UI キットを取得する (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams UI ライブラリ

ブラウザーで UI Teams関連コンポーネントを表示およびテストします。

> [!div class="nextstepaction"]
> [UI ライブラリ (プレイグラウンド) を試す](https://dev-int.teams.microsoft.com/storybook/main/index.html)

これらのテンプレートと関連コンポーネントをアプリ プロジェクトに直接Teamsインポートします。

> [!div class="nextstepaction"]
> [UI ライブラリを取得する (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>サンプル アプリ

サンプル アプリをアップロードして、アプリの外観と動作をクライアントで確認Teamsできます。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>その他のリソース

詳細については、次のいずれかのリソースを試してください。

### <a name="fluent-ui-documentation"></a>Fluent UI ドキュメント

エクスペリエンスの構築に使用される基本的な UI Fluentコード サンプルと実装の詳細Teams取得します。

> [!div class="nextstepaction"]
> [UI Teamsを試す (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー。

Web ベースのツールでアダプティブ カードを設計します。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)

## <a name="see-also"></a>関連項目

* [会議のアプリを有効にしてTeamsする](../../apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
* [Microsoft Teams のボットをデザインする](~/bots/design/bots.md)
* [仮想アシスタントを作成する](~/samples/virtual-assistant.md)
* [Microsoft Teams のアプリのタスク モジュールの設計](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)
