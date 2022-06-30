---
title: UI テンプレートを使用したアプリの設計
author: heath-hamilton
description: Microsoft Teams で一般的に見られる標準化された UI コンポーネント、レイアウト、パターンを使用して、アプリをより迅速に設計する方法について説明します。
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: c4a8b0b626092e4980ccac95f98148829dc06ccd
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558724"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>UI テンプレートを使用した Microsoft Teams アプリの設計

UI テンプレートを使用して Microsoft Teams アプリを迅速に設計します。 テンプレートは、一般的な Teams ユース ケースで動作する Fluent UI ベースのコンポーネントのコレクションであり、ユーザーにとって最適なエクスペリエンスを把握する時間を増やします。

## <a name="getting-started-with-tools-and-samples"></a>ツールとサンプルの概要

次のリソースは、UI テンプレートを使用してアプリを設計および開発するのに役立ちます。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit からアプリ設計用の UI テンプレートを入手します。これには、使用状況、構造、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。

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

サンプル アプリをインストールして、TEAMS コンテキスト内での UI テンプレートの外観と動作を確認します。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="calendar"></a>カレンダー

Teams では、予定表は、ユーザーが自分またはグループの今後および過去のイベントを表示、スケジュール、管理する場所です。

### <a name="top-use-cases"></a>上位のユース ケース

* 会議とイベントをスケジュールする
* 今後の会議やイベントのリマインダーを取得する
* スケジュールを表示する

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/desktop-calendar.png" alt-text="デスクトップ上の予定表 UI テンプレートの例を示します。":::

## <a name="dashboard"></a>ダッシュボード

ダッシュボードには、中央の場所 (Teams 個人用アプリやタブなど) にさまざまな種類のコンテンツが表示されます。 ユーザーは、ダッシュボードに表示される内容の少なくとも一部をカスタマイズできる必要があります。

### <a name="top-use-cases"></a>上位のユース ケース

* データを分析する
* レポート メトリック
* 1 か所で異なる情報を整理する

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="モバイル上のダッシュボード UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="デスクトップ上のダッシュボード UI テンプレートの例を示します。":::

## <a name="data-visualization"></a>データ可視化

異なるカード サイズ (シングル、ダブル、フル) を使用して、同じページにデータ視覚化を積み重ねて整理できます。 カードは、列のレイアウトに合わせてスケーリングされ、空白を埋めます。

### <a name="top-use-cases"></a>上位のユース ケース

* 複雑な情報を表示する
* ダッシュボードを作成する

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="モバイルでのデータ視覚化 UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="デスクトップ上のデータ視覚化 UI テンプレートの例を示します。":::

## <a name="empty-state"></a>空の状態

空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。 柔軟性が高く、次の設計で 1 つ、いくつかのコンポーネント、またはすべてのコンポーネントを使用するように調整します。

### <a name="top-use-cases"></a>上位のユース ケース

* サインイン
* ウェルカム メッセージと初回実行エクスペリエンス
* 成功メッセージ
* エラー メッセージ

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="モバイル上の空の状態 UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="デスクトップ上の空の状態 UI テンプレートの例を示します。":::

## <a name="filter"></a>Filter

フィルターを使用すると、選択した条件に基づいて表示される情報を減らすことができます。 テーブル、リスト、カード、およびコンテンツを整理するその他のコンポーネントを含むフィルターを含めることができます。

### <a name="top-use-cases"></a>上位のユース ケース

コンテンツの整理:

* リスト
* テーブル
* ダッシュボード
* データ可視化

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="フィルター テンプレートの例を示します。":::

## <a name="form"></a>フォーム

フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。 適切なユーザー エクスペリエンスを実現するには、入力フィールドの明確なラベル付けと論理的なグループ化が重要です。

### <a name="top-use-cases"></a>上位のユース ケース

* サインイン
* ユーザー プロファイル
* Settings
* ユーザー入力コレクション

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="モバイル上のフォーム UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/form.png" alt-text="デスクトップ上のフォーム UI テンプレートの例を示します。":::

## <a name="list"></a>リスト

リストを使用して、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。

### <a name="top-use-cases"></a>上位のユース ケース

* データを表示する
* アプリ コンテンツに対するコンテキスト アクション

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="モバイル上のリスト UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="デスクトップ上のリスト UI テンプレートの例を示します。":::

## <a name="sign-in"></a>サインイン

さまざまな Teams コンテキストと ID プロバイダーのアプリ サインイン フローを設計できます。 次の例にはシングル サインオン (SSO) が含まれており、最も簡単な認証エクスペリエンスをお勧めします。

### <a name="top-use-case"></a>上位のユース ケース

* ユーザーを認証する

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="モバイルでのサインイン UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="デスクトップでのサインイン UI テンプレートの例を示します。":::

## <a name="settings"></a>Settings

設定画面では、ユーザーがアプリで自分の設定を構成できます。 (注: 設定は [、基本的な UI コンポーネント](~/concepts/design/design-teams-app-basic-ui-components.md)のコンテナーです。

### <a name="top-use-case"></a>上位のユース ケース

* アプリの機能を管理する

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="設定テンプレートの例を示します。":::

## <a name="task-board"></a>タスク ボード

タスク ボードは、かんばんボードやスイム レーンとも呼ばれ、作業項目またはチケットの状態を追跡するためによく使用されるカードのコレクションです。 また、任意の種類のコンテンツをカテゴリに並べ替えるためにも使用できます。 列間でカードを編集および移動できます。

### <a name="top-use-cases"></a>上位のユース ケース

* プロジェクトの管理。 タスクの割り当てと状態の追跡。
* ブレーンストーミング。 さまざまなカテゴリにアイデアを追加する。
* 並べ替えの演習。 あらゆる種類の情報をバケットに整理する。

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="モバイル上のタスク ボード UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="デスクトップ上のタスク ボード UI テンプレートの例を示します。":::

## <a name="wizard"></a>ウィザード

ウィザードでは、ユーザーが複数の画面を案内してタスク (セットアップ プロセスなど) を完了します。

### <a name="top-use-cases"></a>上位のユース ケース

* セットアップ
* オンボード
* 初回実行エクスペリエンス

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="モバイル上のウィザード UI テンプレートの例を示します。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="デスクトップ上のウィザード UI テンプレートの例を示します。":::

## <a name="see-also"></a>関連項目

* [基本的な Fluent UI コンポーネントを使用してアプリを設計する](~/concepts/design/design-teams-app-basic-ui-components.md)
* [高度な UI コンポーネントを使用した Microsoft Teams アプリの設計](~/concepts/design/design-teams-app-advanced-ui-components.md)
* [ボット メッセージの書式を設定する](~/bots/how-to/format-your-bot-messages.md)
