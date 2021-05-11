---
title: UI テンプレートを使用したアプリの設計
author: heath-hamilton
description: 標準化された UI コンポーネント、レイアウト、およびパターンを使用して、アプリを迅速に設計し、Microsoft Teams。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: d627ce3b29ffa071d0d7e238c572c7cb69fa4cd9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020766"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>UI テンプレートをMicrosoft Teamsアプリを設計する

UI テンプレートを使用Microsoft Teamsアプリを迅速に設計します。 テンプレートは、一般的な Teams の使用例で動作する Fluent UI ベースのコンポーネントのコレクションで、ユーザーに最適なエクスペリエンスを把握する時間が広がっています。

## <a name="getting-started-with-tools-and-samples"></a>ツールとサンプルの使用を開始する

次のリソースは、UI テンプレートを使用してアプリを設計および開発するのに役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

アプリ設計の UI テンプレートを Microsoft Teams UI キットから取得します。これには、使用状況、解剖学、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。

> [!div class="nextstepaction"]
> [UI キットを取得する (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft TeamsUI ライブラリ

ブラウザーで UI テンプレートTeams関連するコンポーネントを個別に表示およびテストします。

> [!div class="nextstepaction"]
> [UI ライブラリ (プレイグラウンド) を試す](https://dev-int.teams.microsoft.com/storybook/main/index.html)

これらのテンプレートと関連コンポーネントをアプリ プロジェクトに直接Teamsインポートします。

> [!div class="nextstepaction"]
> [UI ライブラリを取得する (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>サンプル アプリ

サンプル アプリをインストールして、UI テンプレートの外観と動作を各コンテキストTeamsします。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a>List

リストを使用して、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、リスト UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* データの表示
* アプリ コンテンツに関するコンテキスト アクション

## <a name="dashboard"></a>ダッシュボード

ダッシュボードには、さまざまな種類のコンテンツが中央の場所に表示されます (Teamsまたはタブ)。 ユーザーは、ダッシュボードに表示される機能の少なくとも一部をカスタマイズできる必要があります。

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例は、ダッシュボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* データの分析
* レポートの指標
* 異なる情報を 1 か所に整理する

## <a name="form"></a>フォーム

フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。 ユーザー エクスペリエンスを向上するには、入力フィールドの明確なラベル付けと論理グループ化が重要です。

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、フォーム UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* サインインする
* ユーザー プロファイル
* 設定
* ユーザー入力コレクション

## <a name="sign-in"></a>サインインする

さまざまなコンテキストと ID プロバイダー用にアプリ Teamsフローを設計できます。 次の例では、シングル サインオン (SSO) を含み、最も簡単な認証エクスペリエンスをお勧めします。

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、サインイン UI テンプレートを示しています。" border="false":::

### <a name="top-use-case"></a>トップ の使用例

* ユーザーの認証

## <a name="task-board"></a>タスク ボード

タスク ボード (カンバン ボードまたはスイム レーンとも呼ばれる) は、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。 また、任意の種類のコンテンツをカテゴリに並べ替える場合にも使用できます。 列間でカードを編集および移動できます。

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、タスク ボードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* プロジェクトの管理。 タスクの割り当てと追跡状態
* ブレインストーミング。 さまざまなカテゴリにアイデアを追加する
* 並べ替えの演習。 任意の種類の情報をバケットに整理する

## <a name="data-visualization"></a>データ可視化

異なるカード サイズ (シングル、ダブル、フル) を使用して、データの視覚化を同じページで積み重ね、整理できます。 カードは、列のレイアウトに合わせて拡大縮小され、空白を入力します。

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、データ可視化 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* 複雑な情報を表示する
* ダッシュボードの作成

## <a name="wizard"></a>ウィザード

ウィザードは、ユーザーが複数の画面を介してタスク (セットアップ プロセスなど) を完了する方法を案内します。

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例は、ウィザードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* セットアップ
* オンボード
* 初回実行エクスペリエンス

## <a name="empty-state"></a>空の状態

空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。 柔軟性が高く、次の設計で 1 つ、少数、またはすべてのコンポーネントを使用できます。

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、空の状態 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* サインインする
* ウェルカム メッセージと初回実行エクスペリエンス
* 成功メッセージ
* エラー メッセージ

## <a name="notification-bar"></a>通知バー

通知バーは、ユーザーが即座にアクションを実行する必要が生じない、簡潔で重要なメッセージを表示するための専用の領域です。 特定の背景色とアイコンは、特定の種類のメッセージに関連付けられる (以下を参照)。

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、通知バー テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* 重大なメッセージ、エラー、および警告
* 成功メッセージ
* 情報メッセージまたはプロモーション メッセージ

## <a name="left-nav"></a>左ナビゲーション

左側のナビゲーションを使用して、[ページ] タブ内の複数Teamsします。次の例では、左側のナビゲーションはチャネル リストとタブ コンテンツの間にあります。

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、左側のナビゲーション テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* [ページ] タブ内の複数のページTeamsする
* 複雑なアプリを複数のページに分割する

## <a name="breadcrumb"></a>Breadcrumb

Breadcrumbs は、アプリの階層を伝えるナビゲーション支援です。 ユーザーは、表示しているページが全体的なエクスペリエンスに適合する方法を理解し、その階層内の上位レベルへの 1 回のクリックアクセスを許可するのに役立ちます。

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、パンくずテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* コミュニケーション階層
* ナビゲーション

## <a name="toolbar"></a>ツール バー

ツールバーは、コントロールのセットをグループ化するコンテナーです。

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="ツール バー テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* アプリ コンテンツに関するコンテキスト アクション
* コンテキスト フィルターと検索
* ナビゲーションとパンくず

## <a name="stage"></a>ステージ

Stage は、ユーザーが別のアプリやブラウザーでエンティティを開く代わりに、Teams、ファイル、web サイトなど、エンティティを開く方法を提供します。 ステージの主な使用例は表示です。サーフェスを複雑な操作に使用する必要があります。

(実装ノート: 大規模なタスク モジュールを使用してステージ [をビルド](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)します。)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="ステージ テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>上位の使用例

* 別のアプリやブラウザーではなくTeamsでエンティティを開く
* スポットライト メディアまたは他のコンテンツ
