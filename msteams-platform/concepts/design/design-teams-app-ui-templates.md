---
title: UI テンプレートを使用してアプリを設計する
author: heath-hamilton
description: Microsoft Teams 全体でよく見られる標準化された UI コンポーネント、レイアウト、パターンを使用して、アプリをより迅速に設計します。
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 144c18ab03d76e442a4de64a5c61af76cb2b8b5f
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606081"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>UI テンプレートを使用して Microsoft Teams アプリを設計する

UI テンプレートを使用して、より迅速に Microsoft Teams アプリを設計します。 テンプレートは、一般的なチームのユースケースの間で機能する Fluent UI ベースのコンポーネントのコレクションであり、ユーザーにとって最適な環境を得るための時間を増やすことができます。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットから UI テンプレートを取得することができます。これには、利用状況、構造、アクセシビリティ、およびベストプラクティスに関する広範な情報も含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="list"></a>リスト

リストを使用して、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにすることができます。

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、リスト UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* データの表示
* アプリコンテンツに対するコンテキストアクション

## <a name="dashboard"></a>ダッシュボード

ダッシュボードは、さまざまな種類のコンテンツを中央の場所 (Teams の個人アプリまたはタブ) に表示します。 ダッシュボードに表示される情報の一部をユーザーがカスタマイズできるようにする必要があります。

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例はダッシュボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* データを分析する
* レポートの指標
* 異なる情報を1か所にまとめます。

## <a name="form"></a>フォーム

フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。 適切なユーザー環境では、入力フィールドのラベルと論理グループを明確にすることが重要です。

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、フォーム UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* サインイン
* ユーザー プロファイル
* 設定
* ユーザー入力のコレクション

## <a name="sign-in"></a>サインイン

さまざまなチームコンテキストと id プロバイダーに対してアプリのサインインフローを設計できます。 次の例には、シングルサインオン (SSO) が含まれています。これは、最も簡単な認証手順にすることをお勧めします。

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、サインイン UI テンプレートを示しています。" border="false":::

### <a name="top-use-case"></a>トップユースケース

* ユーザーを認証する

## <a name="task-board"></a>タスクボード

タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。 また、任意の種類のコンテンツをカテゴリ別に並べ替えるために使用することもできます。 列間でカードを編集し、移動することができます。

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、タスクボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* プロジェクトの管理。 タスクの割り当てと進捗状況の追跡
* ブレイン. さまざまなカテゴリにアイデアを追加する
* 演習の並べ替え。 任意の種類の情報をバケットに編成する

## <a name="data-visualization"></a>データ可視化

1つのページでデータの視覚エフェクトを積み重ねて整理するには、異なるカードサイズ (単一、2、完全) を使用できます。 カードは、列のレイアウトに合わせて拡大または縮小されます。

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、データビジュアライゼーション UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* 複雑な情報を表示する
* ダッシュボードを作成する

## <a name="wizard"></a>ウィザード

ウィザードを使用すると、1つのタスクを完了するためにユーザーが複数の画面を移動できます (セットアッププロセスなど)。

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例は、ウィザードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* セットアップ
* オンボード
* 初回実行時のエクスペリエンス

## <a name="empty-state"></a>空の状態

空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。 次の設計では、1つまたはいくつかのコンポーネントを使用するように柔軟に適応できます。

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、ウィザードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* サインイン
* ウェルカムメッセージと初回実行時のエクスペリエンス
* 成功メッセージ
* エラー メッセージ

## <a name="notification-bar"></a>通知バー

通知バーは、ユーザーがすぐにアクションを実行しなくてもよい、簡単な重要なメッセージを表示するための専用の領域です。 特定の種類のメッセージ (下の図を参照) には、特定の背景色とアイコンが関連付けられています。

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、通知バーテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* 重要なメッセージ、エラー、および警告
* 成功メッセージ
* 情報メッセージまたはプロモーションメッセージ

## <a name="left-nav"></a>左ナビゲーション

左側のナビゲーションを使用して、Teams タブ内の複数のページを参照します。次の例では、左側のナビゲーションはチャネルリストとタブのコンテンツの間にあります。

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、左側のナビゲーションテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* [Teams] タブ内の複数のページを参照する
* 複雑なアプリを複数のページに分割する

## <a name="breadcrumb"></a>Breadcrumb

階層リンクは、アプリの階層を伝達するナビゲーション支援者です。 これにより、ユーザーが表示しているページが全体的な効果にどのように適合し、1回のクリックでその階層の上位レベルにアクセスできるかを理解することができます。

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、階層リンクテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* コミュニケーション階層
* ナビゲーション

## <a name="toolbar"></a>ツールバー

ツールバーは、コントロールのセットをグループ化するためのコンテナーです。

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="例は、ツールバーテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* アプリコンテンツに対するコンテキストアクション
* コンテキストフィルターと検索
* ナビゲーションとブレッドクラム

## <a name="stage"></a>ステージ

ステージを使用すると、ユーザーは、画像、ファイル、web サイトなどのエンティティを、別のアプリやブラウザーで開くのではなく、Teams で開くことができます。 ステージの主なユースケースが表示されています。複雑な対話には、サーフェスを使用しないでください。

(実装メモ: 大規模な [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用して、ステージを構築します。)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="例は、ステージテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a>主なユースケース

* 別のアプリまたはブラウザーではなく Teams でエンティティを開く
* スポットライトメディアまたはその他のコンテンツ

## <a name="microsoft-teams-ui-library-coming-soon"></a>Microsoft Teams UI ライブラリ (近日公開予定)

Microsoft Teams UI ライブラリを使用すると、これらの運用可能な UI テンプレートをアプリプロジェクトに直接インポートすることができます。
