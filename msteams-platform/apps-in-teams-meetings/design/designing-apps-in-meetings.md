---
title: 会議の内線情報の設計
author: heath-hamilton
description: Teams 会議でアプリを設計し、Microsoft Teams UI Kit を取得する方法について説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: c6e76356b698da4e32e279b0842ab2cc35254e99
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886759"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Microsoft Teams 会議の内線番号の設計

会議の生産性を向上させるアプリを作成できます。 たとえば、通話中にアンケートを完了したり、会議の流れを中断しないクイック リマインダーを送信したりします。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインについては、Microsoft Teams UI Kit をご覧ください。

> [!div class="nextstepaction"]
> [Microsoft Teams UI キットを取得する (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>会議の内線を追加する

会議の前と会議中に会議の内線を追加できます。 特定の会議用のアプリを Teams ストア (AppSource) から直接追加することもできます。

### <a name="add-before-a-meeting"></a>会議の前に追加する

会議の詳細で、タブの追加 **+** を選択してアプリのフライアウトを開き、会議用に最適化されたアプリを検索します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a>会議中に追加する

会議で、[その他の **アプリ** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **の追加] を選択し**、目的のアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a>会議の前に

会議の前に、タブにコンテンツを追加できます。次の例は、通話中に回答する下書きアンケート質問を示しています。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細にコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>構造: [会議] タブ (会議の前と後)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前と後の会議タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2 |**タブ オーバーフロー**: 名前の変更や削除などのタブアクションを開きます。|
|3|**iframe**: アプリのコンテンツを表示します。|

### <a name="designing-with-ui-templates"></a>UI テンプレートを使用した設計

会議タブを設計するには、次のいずれかの Teams UI テンプレートを使用します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスク ボードは、カンバボードまたはスレーンと呼ばれることもあるタスク ボードで、作業項目やチケットの状態を追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左側のナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。 一般に、タブ ナビゲーションは最小限に抑えます。

## <a name="use-an-in-meeting-tab"></a>会議内タブを使用する

[会議内] タブは、会議中のコラボレーションを拡張するキャンバスです。 参加者は、共有ビューまたはロール ベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示および操作できます。

### <a name="use-cases"></a>使用例

ユーザーは会議中タブを使用して次の場合があります。

* 詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)
* 会議参加者の投票、アンケート、またはタスク アイテムをすばやく作成する
* 会議に関連するメモを表示する (たとえば、営業リードに関する情報)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、会議内タブで投票コンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a>構造: [会議内] タブ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議内タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン (選択):** 16 ピクセルの透明なアプリ ロゴ。|
|2 |**アプリ名**|
|3|**ヘッダー**: アプリ名が含まれます。|
|4 |**[閉じる] ボタン**: タブを閉じます。フッターのアクションの代わりに、常に右上の閉じるアイコンを使用します。|
|5 |**通知バー**: エラー通知はヘッダーの直下に表示され、iframe コンテンツを 20 ピクセル下にプッシュします。|
|6 |**iframe**: アプリのコンテンツを表示します。|

### <a name="spacing"></a>Spacing

280 ピクセル幅の iframe 領域内に端から端まで収まる会議内タブを最適化します。 iframe の左右とタブ ヘッダーの間には 20 ピクセルのパディングがあります。 iframe はタブの下部にフル ブリードされます。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="会議中のタブ間隔のサイズの例を示します。" border="false":::

### <a name="scrolling"></a>スクロール

Iframe の内容は垂直方向にスクロールする必要があります。 スクロールしたコンテンツのみ表示できます (上または下に何も表示されません)。 スクロール バーは iframe コンテンツの一部です。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="会議中のタブのスクロール方法の例を示します。" border="false":::

### <a name="navigation"></a>ナビゲーション

ナビゲーション レイヤーやコンテンツの多いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。 ユーザーは前のレイヤーに戻れなければならない。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例は、会議内ナビゲーションを示しています。" border="false":::

## <a name="use-an-in-meeting-dialog"></a>会議中ダイアログを使用する

会議中のダイアログは Teams の会議ステージに表示されます。 ユーザーの注意、確認、またはやり取りが必要ですが、会議を中断することなく、微妙です。 これらは、淡色でタスク指向のシナリオに対して、念入りに使用する必要があります。

### <a name="use-cases"></a>使用例

会議内ダイアログは、参加者が次の操作を行うユーザー (会議の開催者など) によってトリガーされます。

* 簡単なフィードバックを提供する
* 短いアンケートまたは投票を行う
* 承認を送信する
* アラームを取得する

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議中のダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a>構造: 会議内ダイアログ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議中ダイアログの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**ヘッダー**: アプリ アイコン、名前、アクション文字列、閉じるアイコンが含まれます。|
|2 |**iframe**: アプリのコンテンツを表示します。|

### <a name="anatomy-in-meeting-dialog-header"></a>構造: 会議内ダイアログ ヘッダー

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議中ダイアログ ヘッダーの構造構造を示しています。" border="false":::

ヘッダーには 2 つのバリエーションがあります。 可能であれば、アバターと一緒にバリアントを使用して、ダイアログがユーザーから来ているのを強化します。

|カウンター|説明|
|----------|-----------|
|1|**アバター**: 会議中のダイアログを開始するユーザー。|
|2 |**アプリ アイコン**|
|3|**アプリ名**|
|4 |**[閉じる]** ボタン : ダイアログを閉じます。|
|5 |**操作文字列**: 通常、ダイアログを開始したユーザーを示します。|

### <a name="responsive-behavior"></a>応答性の高い動作

会議中のダイアログは、シナリオによってサイズが異なる場合があります。 パディングとコンポーネントのサイズは必ず維持してください。

* **Width**: iframe の幅は、指定した範囲内の絶対値です。
* **Height**: ダイアログの高さは、iframe 内のコンテンツによって決まります。 垂直方向のスクロールは、最大の高さを超えるコンテンツに引き継がされます。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例では、会議中のダイアログを表示します。幅: 最小 - 280 ピクセル (248 ピクセルの iframe)。最大 - 460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="after-a-meeting"></a>会議後

会議の終了後に会議に戻り、アプリのコンテンツを表示できます。 この例では、会議の開催者は **[Contoso]** タブで投票結果を確認できます (注: 設計上の観点から、会議前と会議後のタブエクスペリエンスの違いはありません)。

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

### <a name="interactions"></a>操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="操作の数を制限する方法を示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>操作の数を制限する

会議中のダイアログの場合は、ユーザーがすばやく何かを成し遂げるのに役立つ不要なコンテンツを削除します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="不要な要素を導入しない方法を示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>不要な要素を導入しない

複数の対話を含む 1 つの会議内ダイアログは、通話の邪魔になる可能性があります。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="単一列のダイアログ レイアウトの使い方を示す例。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>行う: 単一列のダイアログ レイアウトを使用する

ダイアログは会議ステージの中心にあるので、ユーザーの不満を避けるため、タスクの完了は迅速かつシンプルである必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議の内線のスペースを低優先にしてはいけないことを示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a>不要: スペースを整理する

密度の高いコンテンツや過剰に構造化されたコンテンツは、特に会議中に、気が散らされ、圧倒される可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="1 列のタブ レイアウトを表示する例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>行う: 単一列のタブ レイアウトを使用する

会議中タブの性質が狭い場合は、コンテンツを 1 つの列に表示することを強く推奨します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="複数の列を含むタブを表示する例。" border="false":::

#### <a name="dont-use-multiple-columns"></a>使用しない: 複数の列を使用する

会議内タブのスペースが限られているので、複数の列を含むレイアウトは推奨されません。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>コントロール

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="プライマリ コントロールを右揃えする方法を示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do: Right align the primary action

視覚的に最も大きなアクションは、最も右の位置に配置することをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="プライマリ コントロールを左揃えにしない方法を示す例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Don't: 左揃えまたは中央揃えアクション

これは、ダイアログでのコントロール配置の標準の Teams パターンとは異なり、上部のダイアログと競合する可能性があります。

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議中のタブでの垂直方向のスクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a>行う: 縦方向にスクロールする

ユーザーは、Teams (および他の場所) での垂直方向のスクロールを期待します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議中のタブで水平方向のスクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a>水平方向にスクロールしない

水平方向のスクロールは、Teams では想定される動作ではありません。 会議環境内の他のキャンバスは垂直方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>ワークフロー

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議内タブに複雑なシナリオを表示する例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>行う: 会議内タブで複雑なシナリオを表示する

アプリに複数のタスクが含まれる場合は、1 列のレイアウトで会議内タブを使用することを強く推奨します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議中のダイアログで複雑なシナリオを表示する例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>[しない]: 会議内ダイアログを複雑にする

会議中のダイアログは、簡単な対話を目的とします。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="濃色テーマの会議の拡張機能を表示する例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a>行う: Teams のカラー トークンを使用する

Teams 会議は、ユーザーがディスカッションと共有コンテンツに集中できるよう、視覚的および認知的な雑音を減らすために、濃色モード用に最適化されています。 カラー トークン <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI) の使用について学習します</a>。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="既定 (淡色) テーマの会議の内線を表示する例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a>[しない]: ハード コードの 16 進値

Teams のカラー トークンを使用しない場合、設計の拡張性が低く、管理に時間がかかる可能性があります。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="[戻る] ボタンを使用して会議の内線を表示する例。" border="false":::

#### <a name="do-have-a-back-button"></a>実行する: [戻る] ボタンがある

会議中のタブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻れなければならない。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="2 つの閉じボタンを持つ会議の内線を表示する例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>[しない]: 別の閉じボタンを含める

会議中のタブ コンテンツを閉じるオプションを指定すると、会議内タブ自体を閉じるボタンがヘッダーに既に存在する場合に問題が発生する可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議内タブ内にモーダル (またはタスク モジュール) を表示する例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>注意: [会議中] タブ内でモーダルを回避する

既に狭い会議内タブのモーダル (タスク モジュールとも呼ばれる) は、コンテンツを折り返してあいまいにしている可能性があります。

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に公開する予定の場合は、申請中にアプリが失敗する一般的な設計上の問題を理解する必要があります。

> [!div class="nextstepaction"]
> [設計検証のガイドラインを確認する](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
