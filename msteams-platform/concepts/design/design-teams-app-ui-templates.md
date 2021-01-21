---
title: UI テンプレートを使ったアプリの設計
author: heath-hamilton
description: Microsoft Teams で一般的に見られる標準化された UI コンポーネント、レイアウト、パターンを使用して、アプリをより迅速に設計します。
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: b4d244bbf78ac85042d5caf8ec84afe42e79b3c7
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911927"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>UI テンプレートを使用した Microsoft Teams アプリの設計

UI テンプレートを使用して、Microsoft Teams アプリをより迅速に設計します。 テンプレートは、一般的な Teams の使用事例全体で機能する Fluent UI ベースのコンポーネントのコレクションです。ユーザーに最適なエクスペリエンスを見つめる時間が広がっています。

## <a name="getting-started-with-tools-and-samples"></a>ツールとサンプルの使用を開始する

次のリソースは、UI テンプレートを使ったアプリの設計と開発に役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit からアプリ設計用の UI テンプレートを取得します。これには、使用状況、構造、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。

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

## <a name="list"></a>リスト

リストを使用して、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="リスト UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* データの表示
* アプリ コンテンツに対するコンテキスト アクション

## <a name="dashboard"></a>ダッシュボード

ダッシュボードは、さまざまな種類のコンテンツを中央の場所 (Teams 個人用アプリまたはタブ) に表示します。 ユーザーは、ダッシュボードに表示される機能の少なくとも一部をカスタマイズできる必要があります。

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="ダッシュボード UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* データを分析する
* レポートの指標
* 異なる情報を 1 か所に整理する

## <a name="form"></a>フォーム

フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。 ユーザー エクスペリエンスを向上するには、入力フィールドの明確なラベル付けと論理グループが重要です。

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="フォーム UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* サインイン
* ユーザー プロファイル
* 設定
* ユーザー入力のコレクション

## <a name="sign-in"></a>サインイン

さまざまな Teams コンテキストと ID プロバイダーに対してアプリのサインイン フローを設計できます。 次の例にはシングル サインオン (SSO) が含まれています。これは、最も簡単な認証エクスペリエンスに推奨されます。

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、サインイン UI テンプレートを示しています。" border="false":::

### <a name="top-use-case"></a>一番上の使用事例

* ユーザーを認証する

## <a name="task-board"></a>タスク ボード

タスク ボード (カンバボードまたはスレーンとも呼ばれる) は、作業項目やチケットの状態を追跡するためによく使用されるカードのコレクションです。 また、任意の種類のコンテンツをカテゴリに並べ替える場合にも使用できます。 列間でカードの編集と移動を行います。

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="タスク ボード UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* プロジェクトの管理。 タスクの割り当てと状態の追跡
* ブレーンストーミング。 さまざまなカテゴリにアイデアを追加する
* 並べ替えの演習。 任意の種類の情報をバケットに整理する

## <a name="data-visualization"></a>データ可視化

異なるカード サイズ (単一、倍数、および完全) を使用して、データの視覚化を同じページに重ね合わせて整理できます。 カードは列レイアウトに合わせて拡大縮小され、空白スペースで埋めることができます。

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="データ可視化 UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* 複雑な情報を表示する
* ダッシュボードを作成する

## <a name="wizard"></a>ウィザード

ウィザードを使用すると、ユーザーは複数の画面を介してタスク (セットアップ プロセスなど) を完了できます。

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="ウィザード UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* セットアップ
* オンボード
* 初回実行時エクスペリエンス

## <a name="empty-state"></a>空の状態

空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。 柔軟性が高く、次の設計で 1 つのコンポーネント、少数のコンポーネント、またはすべてのコンポーネントを使用するために適応できます。

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="空の状態 UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* サインイン
* ウェルカム メッセージと最初の実行エクスペリエンス
* 成功メッセージ
* エラー メッセージ

## <a name="notification-bar"></a>通知バー

通知バーは、ユーザーがすぐにアクションを実行する必要が生じない、簡潔で重要なメッセージを表示するための専用領域です。 特定の背景色とアイコンは、特定の種類のメッセージに関連付けます (下記を参照)。

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="通知バー テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* 重大なメッセージ、エラー、および警告
* 成功メッセージ
* 情報メッセージまたはプロモーション メッセージ

## <a name="left-nav"></a>左ナビゲーション

左側のナビゲーションを使用して、Teams タブ内の複数のページを参照します。次の例では、左側のナビゲーションはチャネルリストとタブ コンテンツの間にあります。

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="左側のナビゲーション テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* Teams タブ内の複数のページを参照する
* 複雑なアプリを複数のページに分割する

## <a name="breadcrumb"></a>Breadcrumb

階層リンクは、アプリの階層を伝えるナビゲーションの補助です。 ユーザーは、表示しているページが全体的なエクスペリエンスに適合する方法を理解し、その階層内の上位レベルに 1 回のクリックでアクセスできます。

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、階層リンク テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* 通信階層
* ナビゲーション

## <a name="toolbar"></a>ツールバー

ツールバーは、コントロールのセットをグループ化するコンテナーです。

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="ツール バー テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* アプリ コンテンツに対するコンテキスト アクション
* コンテキスト フィルターと検索
* ナビゲーションと階層リンク

## <a name="stage"></a>ステージ

ステージは、ユーザーが別のアプリやブラウザーでエンティティを開くのではなく、Teams で (画像、ファイル、Web サイトなど) エンティティを開く方法を提供します。 ステージの主な使用例は表示中です。サーフェスは複雑な対話操作には使用できません。

(実装メモ: 大規模なタスク モジュールを使用してステージ [をビルドします](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="ステージ テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a>主な使用事例

* 別のアプリまたはブラウザーではなく、Teams でエンティティを開く
* スポットライト メディアまたは他のコンテンツ
