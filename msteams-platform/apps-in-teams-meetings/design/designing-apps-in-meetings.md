---
title: 会議拡張機能の設計
author: heath-hamilton
description: Teams 会議でアプリを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 022ffdd7341f60a9c6732948a0914383ddb248a8
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018475"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Microsoft Teams 会議拡張機能の設計

アプリを作成して、会議の生産性を高めることができます。 たとえば、通話中にアンケートを完了したり、会議のフローを中断しない簡単なリマインダーを送信したりします。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインについては、Microsoft Teams UI Kit を参照してください。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>会議の拡張機能を追加する

会議の前と会議中に会議拡張機能を追加できます。 特定の会議のアプリを Teams ストア (AppSource) から直接追加することもできます。

### <a name="add-before-a-meeting"></a>会議の前に追加する

会議の詳細で、[タブの追加 **] +** を選択してアプリの飛び出しを開き、会議に最適化されたアプリを検索します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線情報を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a>会議中に追加する

会議で、[その他の :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **アプリの追加] を選択し**、目的のアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線情報を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a>会議の前に

会議の前に、タブにコンテンツを追加できます。次の例は、通話中に回答するアンケートの下書き質問を示しています。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細でコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>解剖学: [会議] タブ (会議の前と後)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前と後の会議タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。|
|3|**iframe**: アプリのコンテンツを表示します。|

### <a name="designing-with-ui-templates"></a>UI テンプレートを使用した設計

会議タブを設計するには、次のいずれかの Teams UI テンプレートを使用します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。 一般に、タブ ナビゲーションは最小限に抑えます。

## <a name="use-an-in-meeting-tab"></a>[会議内] タブを使用する

[会議内] タブは、会議中の共同作業を強化するキャンバスです。 出席者は、共有ビューまたは役割ベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示および操作できます。

### <a name="use-cases"></a>使用例

ユーザーは、[会議内] タブを使用して次の場合があります。

* 詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)
* 会議参加者のポーリング、アンケート、またはタスク アイテムをすばやく作成する
* 会議に関連するメモを表示する (たとえば、営業担当に関する情報)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、会議内タブでポーリング コンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a>解剖学: [会議中] タブ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議内タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン (選択):** 16 ピクセルの透明なアプリ ロゴ。|
|2|**アプリ名**|
|3|**ヘッダー**: アプリ名が含まれます。|
|4|**[閉じる]** ボタン: タブを閉じます。フッターのアクションではなく、常に右上の閉じるアイコンを使用します。|
|5|**通知バー**: エラー通知はヘッダーの直下に表示され、iframe コンテンツを 20 ピクセル下にプッシュします。|
|6|**iframe**: アプリのコンテンツを表示します。|

### <a name="spacing"></a>Spacing

280 ピクセル幅の iframe 領域内にエッジからエッジに合わせて会議内タブを最適化します。 iframe の左側と右側、およびタブ ヘッダーの間には 20 ピクセルのパディングがあります。 iframe はタブの下部に完全にブリードされます。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例では、会議中のタブ間隔のディメンションを示します。" border="false":::

### <a name="scrolling"></a>スクロール

Iframe のコンテンツは垂直方向にスクロールする必要があります。 スクロールしたコンテンツのみを表示できます (上または下に何も表示されません)。 スクロール バーは、iframe コンテンツの一部です。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、会議内タブのスクロール方法を示しています。" border="false":::

### <a name="navigation"></a>ナビゲーション

ナビゲーション レイヤーやコンテンツが多いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。 ユーザーは前のレイヤーに戻る必要があります。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例では、会議内ナビゲーションを示します。" border="false":::

## <a name="use-an-in-meeting-dialog"></a>会議内ダイアログの使用

会議中のダイアログが Teams 会議ステージに表示されます。 ユーザーの注意、確認、またはやり取りが必要ですが、微妙であり、会議を中断しません。 これらの使用は、軽くてタスク指向のシナリオに対して使用する必要があります。

### <a name="use-cases"></a>使用例

会議中のダイアログは、参加者が次の操作を行うユーザー (会議の開催者など) によってトリガーされます。

* 簡単なフィードバックを提供する
* 短いアンケートまたは投票を行う
* 承認を送信する
* アラームを取得する

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議内ダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a>解剖学: 会議中のダイアログ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議内ダイアログの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**ヘッダー**: アプリ アイコン、名前、アクション文字列、閉じるアイコンが含まれます。|
|2|**iframe**: アプリのコンテンツを表示します。|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomy: 会議内ダイアログ ヘッダー

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議中のダイアログ ヘッダーの構造構造を示しています。" border="false":::

2 つのヘッダーバリアントがあります。 可能であれば、アバターと一緒にバリアントを使用して、ダイアログが人から来ているのを強化します。

|カウンター|説明|
|----------|-----------|
|1|**アバター**: 会議内ダイアログを開始するユーザー。|
|2|**アプリ アイコン**|
|3|**アプリ名**|
|4|**[閉じる]** ボタン: ダイアログを閉じます。|
|5|**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。|

### <a name="responsive-behavior"></a>応答性の高い動作

会議内のダイアログは、さまざまなシナリオを考慮してサイズが異なる場合があります。 パディングとコンポーネントのサイズは必ず維持してください。

* **Width**: ダイアログの iframe の幅は、サポートされているサイズ範囲内の任意の場所で指定できます。
* **Height**: ダイアログの iframe の高さは、サポートされているサイズ範囲内の任意の場所で指定できます。 アプリのコンテンツが最大の高さを超えた場合は、ユーザーが垂直方向にスクロールすることもできます。

実装するには、キーを使用して幅と高さを指定 [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) します。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを表示します。幅: 最小--280 ピクセル (248 ピクセルの iframe)。Max---460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="after-a-meeting"></a>会議の後

会議の終了後に会議に戻り、アプリのコンテンツを表示できます。 この例では、会議開催者は **[Contoso]** タブで投票結果を確認できます (注: デザインの観点から、会議前と会議後のタブ エクスペリエンスの違いはありません)。

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例の図は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

### <a name="interactions"></a>対話

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="操作の数を制限する方法を示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Do: 操作の数を制限する

会議中のダイアログでは、ユーザーが何かを迅速に実行するのに役立つ不要なコンテンツを削除します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="不要な要素を導入しない方法を示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>[しない]: 不要な要素を導入する

複数の操作を含む単一の会議内ダイアログは、通話の邪魔になる可能性があります。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="1 列のダイアログ レイアウトを使用する方法を示す例。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>Do: 1 列のダイアログ レイアウトを使用する

ダイアログは会議ステージの中心にあるので、タスクの完了はユーザーの不満を避けるために迅速かつ簡単に行う必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議内線のスペースを煩雑にしてはいけないことを示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a>T't: スペースを乱雑にする

密なコンテンツや過剰に構造化されたコンテンツは、特に会議中に気が散り、圧倒的になる可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="1 列のタブ レイアウトを表示する例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>Do: 1 列のタブ レイアウトを使用する

会議内タブの狭い性質を考えると、コンテンツを 1 つの列に表示することを強く推奨します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="複数の列を持つタブを表示する例。" border="false":::

#### <a name="dont-use-multiple-columns"></a>[しない]: 複数の列を使用する

会議内タブのスペースが限られているので、複数の列を含むレイアウトは推奨されません。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>コントロール

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="プライマリ コントロールを右揃えする方法を示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do: プライマリ アクションを右揃えする

最も視覚的に重いアクションを最も右の位置に配置することをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="プライマリ コントロールを左揃えにしない方法を示す例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>[しない]: 左揃えまたは中央揃えアクション

これは、ダイアログ内のコントロールの配置に関する標準的な Teams パターンから離れ、上部のダイアログボックスと競合する可能性があります。

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議内タブで垂直スクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a>Do: 垂直方向にスクロールする

ユーザーは Teams (および他の場所) での垂直スクロールを期待します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議内タブに水平スクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a>[しない]: 水平方向にスクロールする

Teams での水平方向のスクロールは予期しない動作です。 会議環境内の他のキャンバスは垂直方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>ワークフロー

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議内タブに複雑なシナリオを表示する例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do: [会議内] タブの複雑なシナリオを表示する

アプリに複数のタスクが含まれる場合は、1 列のレイアウトで会議内タブを使用することを強く推奨します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議内ダイアログで複雑なシナリオを表示する例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>[しない]: 会議内のダイアログを複雑にする

会議中のダイアログは、簡単な操作を目的とします。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="暗いテーマで会議の拡張機能を表示する例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a>Do: Teams カラー トークンを使用する

Teams の会議は、ユーザーがディスカッションと共有コンテンツに集中できるよう、視覚的および認知的なノイズを減らすのに役立つダーク モード用に最適化されています。 カラー トークン <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI) の使用について学習します</a>。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="既定の (明るい) テーマを持つ会議拡張機能を表示する例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a>Don't: ハード コードの 16 進値

Teams カラー トークンを使用しない場合、デザインの拡張性が低く、管理に時間がかかっています。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="戻るボタンを使用して会議の拡張機能を表示する例。" border="false":::

#### <a name="do-have-a-back-button"></a>Do: [戻る] ボタンを持つ

会議内タブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻る必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="2 つの閉じボタンを使用して会議の内線表示オプションを表示する例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>[しない] : 別の [閉じ] ボタンを含める

会議中のタブ コンテンツを閉じるオプションを指定すると、ヘッダーに既に会議中のタブ自体を閉じるボタンが存在するために問題が発生する可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議内タブ内にモーダル (またはタスク モジュール) を表示する例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>注意: [会議内] タブ内のモーダルを回避する

既に狭い会議内タブのモーダル (タスク モジュールとも呼ばれる) は、コンテンツをラップしてあいまいにしている可能性があります。

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>デザインを検証する

AppSource にアプリを公開する予定がある場合、アプリの提出時に失敗する原因となるデザイン上の問題を理解しておく必要があります。

> [!div class="nextstepaction"]
> [デザイン検証ガイドラインをチェックする](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
