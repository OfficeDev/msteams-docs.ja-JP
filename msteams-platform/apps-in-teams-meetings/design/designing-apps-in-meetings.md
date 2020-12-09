---
title: 会議の拡張機能を設計する
author: heath-hamilton
description: Teams 会議でアプリを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606134"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Microsoft Teams の会議の拡張機能を設計する

会議の生産性を高めるために、アプリを作成することができます。 たとえば、通話中にアンケートを完了したり、会議のフローを中断しない簡単なアラームを送信したりするようにユーザーに求めます。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインを見つけることができます。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>会議の内線番号を追加する

会議の前と後に会議の内線番号を追加することができます。 また、Teams ストア (AppSource) から直接特定の会議用アプリを作成することもできます。

### <a name="add-before-a-meeting"></a>会議の前に追加する

会議の前の会議の詳細 [ **タブを追加する]** を選択して、アプリのポップアップを開き、会議用に最適化されたアプリを検索します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線番号を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a>会議中に追加する

会議で、[アプリの追加 **] を選択** し、 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Add an app** 必要なアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線番号を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a>会議の前

会議の前に、タブにコンテンツを追加することができます。次の例は、通話中にユーザーが回答する下書きアンケートの質問を示しています。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、電話をかける前に、会議の詳細のアプリコンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>[構造]: [会議] タブ (会議の前と後)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前後の [会議] タブの構造上の構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**[タブ名**]: タブのナビゲーションラベル。|
|2 |**Tab overflow**: 名前の変更や削除などのタブアクションを開きます。|
|3 |**iframe**: アプリのコンテンツを表示します。|

### <a name="designing-with-ui-templates"></a>UI テンプレートを使用して設計する

次の Teams UI テンプレートのいずれかを使用して、[会議] タブのデザインに役立ててください。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [タスクボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。
* [Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。
* [左](../../concepts/design/design-teams-app-ui-templates.md#left-nav)ナビゲーション: タブにいくつかのナビゲーションが必要な場合は、左側のナビゲーションテンプレートが役立ちます。 一般的に、タブナビゲーションは最小限にする必要があります。

## <a name="use-an-in-meeting-tab"></a>[会議中] タブを使用する

[会議中] タブは、会議中に共同作業を補強するためのキャンバスです。 出席者は、共有またはロールベースのビューを使用して、会議ステージ外の専用の領域にあるアプリコンテンツを表示したり操作したりできます。

### <a name="use-cases"></a>ユース ケース

[会議中] タブを使用して、次のことを行うことができます。

* 詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)
* 会議の参加者用に投票、調査、または仕事アイテムをすばやく作成する
* 会議に関連するメモを表示する (たとえば、販売リードに関する情報)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、[会議中] タブに投票の内容を表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a>分析: [会議中] タブ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、[会議中] タブの構造上の構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリアイコン (選択済み)**:16 ピクセルの透過アプリロゴ。|
|2 |**アプリ名**|
|3 |**Header**: アプリ名を含めます。|
|4 |[**閉じる] ボタン**: タブを閉じます。フッター内のアクションではなく、右上にある閉じるアイコンを常に使用します。|
|5 |**通知バー**: エラー通知はヘッダーのすぐ下に表示され、iframe のコンテンツは20ピクセル下にプッシュされます。|
|6 |**iframe**: アプリのコンテンツを表示します。|

### <a name="spacing"></a>Spacing

280ピクセル幅の iframe 領域内のエッジツーエッジに収まるように、[ミーティング中] タブを最適化します。 Iframe の左側と右側、タブヘッダー間には、20ピクセルのパディングがあります。 Iframe はタブの一番下までの完全な裁ち落としです。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例は、[会議中] タブの間隔の大きさを示しています。" border="false":::

### <a name="scrolling"></a>量

Iframe の内容は垂直方向にスクロールする必要があります。 スクロールした内容のみが表示されます (何も上または下にありません)。 Scrollbar は、iframe コンテンツの一部です。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、[会議中] タブのスクロール方法を示しています。" border="false":::

### <a name="navigation"></a>ナビゲーション

ナビゲーション層またはヘビーコンテンツがあるシナリオでは、ユーザーがセカンダリレイヤーに移動できるようにすることをお勧めします。 ユーザーは前のレイヤーに戻ることができる必要があります。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例は、会議中のナビゲーションを示しています。" border="false":::

## <a name="use-an-in-meeting-dialog"></a>会議中のダイアログを使用する

会議中のダイアログは Teams の会議のステージに表示されます。 ユーザーの注意、確認、または対話が必要ですが、それは微妙で、会議に割り込むことはありません。 これらは控えめで、タスク指向のシナリオでは使用してください。

### <a name="use-cases"></a>ユース ケース

会議中のダイアログは、参加者が必要になる可能性のあるユーザー (会議の開催者など) によってトリガーされます。

* 簡単なフィードバックを提供する
* 簡単なアンケートまたは投票を行う
* 承認の提出
* アラームを取得する

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議中のダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a>分析: 会議中のダイアログ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議中のダイアログの構造上の構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**ヘッダー**: アプリアイコン、名前、アクション文字列、および閉じるアイコンが含まれます。|
|2 |**iframe**: アプリのコンテンツを表示します。|

### <a name="anatomy-in-meeting-dialog-header"></a>分析: 会議中のダイアログヘッダー

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議中のダイアログヘッダーの構造上の構造を示しています。" border="false":::

2つのヘッダーバリエーションがあります。 可能であれば、アバターで variant を使用して、ダイアログがユーザーから送られてくることを強調します。

|カウンター|説明|
|----------|-----------|
|1|**アバター**: 会議中のダイアログを開始したユーザー。|
|2 |**アプリ アイコン**|
|3 |**アプリ名**|
|4 |**[閉じる] ボタン**: ダイアログを閉じます。|
|5 |**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。|

### <a name="responsive-behavior"></a>応答性の高い動作

会議中のダイアログのサイズは、シナリオによって異なる場合があります。 パディングとコンポーネントのサイズを維持するようにしてください。

* **幅**: iframe 幅は指定した範囲内の絶対的な値です。
* **高さ**: ダイアログの高さは、iframe のコンテンツによって決まります。 高さの最大値を超えるコンテンツに対して垂直スクロールが行われます。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを示しています。幅: 最小--280 ピクセル (248 ピクセルの iframe)。Max--460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="after-a-meeting"></a>会議の後

会議が終了した後、アプリのコンテンツを表示した後で、会議に戻ることができます。 この例では、会議の開催者は [ **Contoso** ] タブの [投票結果] を見ることができます。 (注: 設計上の観点からは、[事前に予定されている予定の投稿] および [ミーティング後] タブの動作に違いはありません)。

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例は、[ミーティング後] タブを示しています。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

### <a name="interactions"></a>関係

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Do: 操作の数を制限する

会議中のダイアログでは、ユーザーがすばやく作業を行うことができない不要なコンテンツを削除します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>いいえ: 不要な要素を紹介します。

複数の対話がある1つの会議中のダイアログでは、通話があいまいになることがあります。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-use-single-column-layouts"></a>手順: 単一列のレイアウトを使用する

ダイアログは会議ステージの中央にあります。タスクの完了は、ユーザーの不満を回避するために、迅速かつシンプルにする必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a>[しない: スペースを整頓する」

高密度または過度に構造化されたコンテンツは、特に会議中に煩雑で圧倒的なものになる可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-use-single-columns"></a>Do: 単一の列を使用する

[会議中] タブの絞り込みの性質を考えると、コンテンツを1列で表示することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-use-multiple-columns"></a>いいえ: 複数の列を使用します

[会議中] タブの容量に制限があるため、複数の列を持つレイアウトは推奨されません。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>コントロール

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do: 右揃えで主な操作を行います。

最も視覚的に大きい操作を、右端に positioining することをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>いいえ: 左揃えまたは中央揃えのアクション

これは、ダイアログでのコントロールの配置に関する標準 Teams パターンとは異なり、一番上にあるダイアログと競合する可能性があります。

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-scroll-vertically"></a>Do: 上下にスクロール

最も視覚的に大きなアクションは、右端の位置に配置することをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-scroll-horizontally"></a>いいえ: 横方向にスクロール

水平方向のスクロールは、Teams では予期された動作ではありません。 会議環境でのその他のキャンバスは、垂直方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>ワークフロー

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do: [会議中] タブで複雑なシナリオを表示する

アプリに複数のタスクが含まれている場合は、[会議中] タブで1列のレイアウトを使用することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a>[いいえ: 会議中] ダイアログで複雑なシナリオをパッケージ化する

会議中のダイアログは、簡単な相互作用を目的としています。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a>Do: Teams のカラートークンを使用する

Teams 会議は、ビジュアルおよび認知ノイズを軽減するために最適化されており、ユーザーがディスカッションと共有コンテンツに集中できるようにするために役立ちます。 カラートークンの使用について説明します <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(FLUENT UI)</a>。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>[いいえ: 他の消去ボタンを含める]

[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既にボタンが表示されているために、会議中のタブ自体が閉じられるという問題が発生することがあります。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-have-a-back-button"></a>Do: [戻る] ボタンを用意する

[会議中] タブでナビゲーションのレイヤーが複数ある場合、ユーザーは前のビューに戻ることができる必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>[いいえ: 他の消去ボタンを含める]

[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既にボタンが表示されているために、会議中のタブ自体が閉じられるという問題が発生することがあります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>注意: [会議中] タブでは modals を回避する

すでに制限のある [会議中] タブの modals (タスクモジュールとも呼ばれます) は、コンテンツを折り返したり不明瞭にしたりします。

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。

> [!div class="nextstepaction"]
> [設計検証ガイドラインの確認](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
