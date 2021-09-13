---
title: UI テンプレートを使用したアプリの設計
author: heath-hamilton
description: 標準化された UI コンポーネント、レイアウト、およびパターンを使用して、アプリを迅速に設計し、Microsoft Teams。
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: ef1fbe41c7618518dab64c25b3ac17eaf8f925d1
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156936"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>UI テンプレートをMicrosoft Teamsアプリを設計する

UI テンプレートを使用Microsoft Teamsアプリを迅速に設計します。 テンプレートは、Fluent UI ベースのコンポーネントのコレクションで、Teams の一般的な使用例全体で機能し、ユーザーに最適なエクスペリエンスを把握する時間を広く提供します。

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

## <a name="dashboard"></a>ダッシュボード

ダッシュボードには、さまざまな種類のコンテンツが中央の場所に表示されます (Teamsまたはタブ)。 ユーザーは、ダッシュボードに表示される機能の少なくとも一部をカスタマイズできる必要があります。

### <a name="top-use-cases"></a>上位の使用例

* データの分析
* レポートの指標
* 異なる情報を 1 か所に整理する

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="例は、モバイルでのダッシュボード UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例は、デスクトップ上のダッシュボード UI テンプレートを示しています。" border="false":::

## <a name="data-visualization"></a>データ可視化

異なるカード サイズ (シングル、ダブル、フル) を使用して、データの視覚化を同じページで積み重ね、整理できます。 カードは、列のレイアウトに合わせて拡大縮小され、空白を入力します。

### <a name="top-use-cases"></a>上位の使用例

* 複雑な情報を表示する
* ダッシュボードの作成

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="例は、モバイルでのデータ可視化 UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、デスクトップ上のデータ可視化 UI テンプレートを示しています。" border="false":::

## <a name="empty-state"></a>空の状態

空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。 柔軟性が高く、次の設計で 1 つ、少数、またはすべてのコンポーネントを使用できます。

### <a name="top-use-cases"></a>上位の使用例

* サインイン
* ウェルカム メッセージと初回実行エクスペリエンス
* 成功メッセージ
* エラー メッセージ

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="例は、モバイル上の空の状態 UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、デスクトップ上の空の状態 UI テンプレートを示しています。" border="false":::

## <a name="filter"></a>フィルター

フィルターを使用すると、選択した条件に基づいて表示される情報を減らします。 コンテンツを整理するテーブル、リスト、カード、その他のコンポーネントを含むフィルターを含めできます。

### <a name="top-use-cases"></a>上位の使用例

次の場所でコンテンツを整理します。

* リスト
* テーブル
* ダッシュボード
* データ可視化

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="例は、フィルター テンプレートを示しています。" border="false":::

## <a name="form"></a>フォーム

フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。 ユーザー エクスペリエンスを向上するには、入力フィールドの明確なラベル付けと論理グループ化が重要です。

### <a name="top-use-cases"></a>上位の使用例

* サインイン
* ユーザー プロファイル
* 設定
* ユーザー入力コレクション

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="例は、モバイルでのフォーム UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、デスクトップ上のフォーム UI テンプレートを示しています。" border="false":::

## <a name="list"></a>リスト

リストを使用して、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。

### <a name="top-use-cases"></a>上位の使用例

* データの表示
* アプリ コンテンツに関するコンテキスト アクション

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="例は、モバイルのリスト UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、デスクトップ上のリスト UI テンプレートを示しています。" border="false":::

## <a name="sign-in"></a>サインイン

さまざまなコンテキストと ID プロバイダー用にアプリ Teamsフローを設計できます。 次の例では、シングル サインオン (SSO) を含み、最も簡単な認証エクスペリエンスをお勧めします。

### <a name="top-use-case"></a>トップ の使用例

* ユーザーの認証

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="例は、モバイルでのサインイン UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、デスクトップ上の UI テンプレートのサインインを示しています。" border="false":::

## <a name="settings"></a>設定

設定は、ユーザーがアプリで自分の設定を構成できる画面です。 (注: 設定は基本的な UI コンポーネント[のコンテナーです](~/concepts/design/design-teams-app-basic-ui-components.md)。)

### <a name="top-use-case"></a>トップ の使用例

* アプリの機能を管理する

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="設定テンプレートの例を示します。" border="false":::

## <a name="task-board"></a>タスク ボード

タスク ボード (カンバン ボードまたはスイム レーンとも呼ばれる) は、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。 また、任意の種類のコンテンツをカテゴリに並べ替える場合にも使用できます。 列間でカードを編集および移動できます。

### <a name="top-use-cases"></a>上位の使用例

* プロジェクトの管理。 タスクの割り当てと追跡状態
* ブレインストーミング。 さまざまなカテゴリにアイデアを追加する
* 並べ替えの演習。 任意の種類の情報をバケットに整理する

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="例は、モバイル上のタスク ボード UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、デスクトップ上のタスク ボード UI テンプレートを示しています。" border="false":::

## <a name="wizard"></a>ウィザード

ウィザードは、ユーザーが複数の画面を介してタスク (セットアップ プロセスなど) を完了する方法を案内します。

### <a name="top-use-cases"></a>上位の使用例

* セットアップ
* オンボード
* 初回実行エクスペリエンス

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="例は、モバイルでのウィザード UI テンプレートを示しています。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例では、デスクトップにウィザード UI テンプレートを表示します。" border="false":::
