---
title: UI テンプレートを使用したアプリの設計
author: heath-hamilton
description: Microsoft Teamsで一般的に見られる標準化された UI コンポーネント、レイアウト、パターンを使用して、アプリをより迅速に設計します。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 0cd5c6c4525e340f9aa53a78749211783880225a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566020"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>UI テンプレートを使用したMicrosoft Teams アプリの設計

UI テンプレートを使用して、Microsoft Teams アプリをより迅速に設計します。 テンプレートは、一般的なTeamsのユースケースで動作する Fluent UI ベースのコンポーネントのコレクションであり、ユーザーにとって最適なエクスペリエンスを把握する時間が増えます。

## <a name="getting-started-with-tools-and-samples"></a>ツールとサンプルの概要

次のリソースは、UI テンプレートを使用してアプリを設計および開発するのに役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

アプリデザイン用の UI テンプレートをMicrosoft Teams UI Kit から取得し、使用状況、解剖学、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。

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

## <a name="list"></a>List

リストを使用して、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、リスト UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* データの表示
* アプリ コンテンツに対するコンテキスト アクション

## <a name="dashboard"></a>ダッシュボード

ダッシュボードには、さまざまな種類のコンテンツが一元的な場所 (個人用アプリまたはタブTeams) に表示されます。 ユーザーは、ダッシュボードに表示される内容の少なくとも一部をカスタマイズできる必要があります。

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例は、ダッシュボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* データの分析
* レポートの指標
* 異なる情報を 1 か所にまとめる

## <a name="form"></a>フォーム

フォームは、構造化された方法でユーザー入力を収集、検証、および送信するために使用されます。 入力フィールドの明確なラベル付けと論理グループ化は、優れたユーザー エクスペリエンスにとって重要です。

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、フォーム UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* サインイン
* ユーザー プロファイル
* 設定
* ユーザー入力コレクション

## <a name="sign-in"></a>サインイン

さまざまなTeams コンテキストと ID プロバイダーに対して、アプリのサインイン フローを設計できます。 次の例には、シングル サインオン (SSO) が含まれています。

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、UI テンプレートのサインを示しています。" border="false":::

### <a name="top-use-case"></a>トップユースケース

* ユーザーの認証

## <a name="task-board"></a>タスクボード

タスク ボードは、かんばんボードまたはスイム レーンとも呼ばれ、作業項目やチケットの状態を追跡するためによく使用されるカードのコレクションです。 また、任意の種類のコンテンツをカテゴリに並べ替えるためにも使用できます。 列間でカードを編集したり移動したりできます。

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、タスク ボードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* Project管理: タスクの割り当てとステータスの追跡。
* ブレーンストーミング: さまざまなカテゴリにアイデアを追加します。
* 分類の練習: あらゆる種類の情報をバケットにまとめる。

## <a name="data-visualization"></a>データ可視化

異なるカード サイズ (シングル、ダブル、フル) を使用して、同じページ上のデータビジュアライゼーションをスタックして整理できます。 カードは列レイアウトに合わせて拡大縮小され、空白スペースに塗りつぶされます。

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、データ視覚化 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* 複雑な情報を表示する
* ダッシュボードの作成

## <a name="wizard"></a>ウィザード

ウィザードは、ユーザーに対して、複数の画面をガイドして、1 つのタスク (セットアッププロセスなど) を完了します。

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例は、ウィザード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* セットアップ
* オンボード
* 最初の実行エクスペリエンス

## <a name="empty-state"></a>空の状態

空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。 柔軟性が高く、次の設計の 1 つ、数個、またはすべてのコンポーネントを使用するように適応します。

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、空の状態 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* サインイン
* ウェルカム メッセージと初回実行エクスペリエンス
* 成功メッセージ
* エラー メッセージ

## <a name="notification-bar"></a>通知バー

通知バーは、ユーザーが直ちに操作を行う必要がない、簡潔で重要なメッセージを表示するための専用領域です。 特定の背景色とアイコンは、特定の種類のメッセージに関連付けられます(下記参照)。

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、通知バー テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* 重大なメッセージ、エラー、および警告
* 成功メッセージ
* 情報メッセージまたはプロモーション メッセージ

## <a name="left-nav"></a>左ナビ

左側のナビゲーションを使用して、Teamsタブ内の複数のページを参照します。次の例では、左側のナビゲーションはチャネル リストとタブ コンテンツの間にあります。

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、左のナビゲーション テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* Teamsタブ内の複数のページを参照します。
* 複雑なアプリを複数のページに分割します。

## <a name="breadcrumb"></a>Breadcrumb

階層リンクは、アプリの階層を伝えるナビゲーション補助です。 ユーザーは、表示しているページが全体的なエクスペリエンスにどのように適合するかを理解し、その階層の上位レベルにワンクリックでアクセスできるようにします。

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、階層リンク テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* 階層の通信
* ナビゲーション

## <a name="toolbar"></a>ツール バー

ツールバーは、コントロールのセットをグループ化するためのコンテナです。

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="例は、ツールバー テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* アプリ コンテンツに対するコンテキスト アクション
* コンテキスト フィルターと検索
* ナビゲーションと階層リンク

## <a name="stage"></a>ステージ

Stage では、別のアプリやブラウザーで開く代わりに、Teamsでエンティティ (画像、ファイル、Web サイトなど) を開くことができます。 ステージの主なユース ケースは表示です。サーフェスは複雑な相互作用には使用しないでください。

(実装ノート: 大きな [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用してステージを構築します。

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="例は、ステージテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>トップユースケース

* 別のアプリやブラウザーではなく、Teamsでエンティティを開きます。
* スポットライトメディアやその他のコンテンツ。
