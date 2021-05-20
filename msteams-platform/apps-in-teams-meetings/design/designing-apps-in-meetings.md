---
title: 会議の拡張機能の設計
author: heath-hamilton
description: Teams会議でアプリをデザインする方法と、Microsoft Teams UI キットを入手する方法について説明します。
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 0a888c333305e9caafcd0bac0e5549bf08ead424
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566027"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>会議の拡張機能Microsoft Teams設計する

会議の生産性を高めるアプリを作成できます。 たとえば、通話中にアンケートを完了してもらうか、会議のフローを中断しない簡単なアラームを送信するように依頼します。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、より包括的なデザイン ガイドラインについては、Microsoft Teams UI キットを参照してください。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>会議の内線番号を追加する

会議の前と中に会議の内線番号を追加できます。 また、特定の会議のアプリをTeams ストア (AppSource) から直接追加することもできます。

### <a name="add-before-a-meeting"></a>会議の前に追加する

会議の詳細で、[ **タブを追加する +** ] を選択してアプリのポップアップを開き、会議に最適化されたアプリを検索します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線番号を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a>会議中に追加する

会議で、[**アプリを追加** する] を選択 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  し、目的のアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線番号を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a>会議の前に

会議の前に、タブにコンテンツを追加できます。次の例は、通話中に回答する調査質問の下書きを示しています。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細のコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>解剖学: [会議] タブ (会議の前後)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前後の会議タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブオーバーフロー**: 名前の変更や削除などのタブアクションを開きます。|
|3|**iframe**: アプリのコンテンツを表示します。|

### <a name="designing-with-ui-templates"></a>UI テンプレートを使用したデザイン

次の Teams UI テンプレートのいずれかを使用して、会議タブの設計に役立ちます。

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々の項目に対してアクションを実行できるようにします。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスク ボードは、かんばんボードまたはスイム レーンとも呼ばれ、作業項目やチケットの状態を追跡するためによく使用されるカードの集まりです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および送信するためのものです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左のナビゲーション テンプレートは、タブが何らかのナビゲーションを必要とする場合に役立ちます。 通常、タブ ナビゲーションは最小限に抑える必要があります。

## <a name="use-an-in-meeting-tab"></a>[会議中] タブを使用する

[ミーティング中] タブは、会議中のコラボレーションを強化するためのキャンバスです。 参加者は、共有ビューまたはロールベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示したり、操作したりできます。

### <a name="use-cases"></a>使用例

[会議中] タブを使用して、次の場合があります。

* 詳細なフィードバックを提供します。 たとえば、求職者を評価します。
* ミーティング参加者の投票、アンケート、またはタスク アイテムを作成します。
* 会議に関連するメモを表示します。 たとえば、販売リードに関する情報などです。

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、ミーティング中のタブで投票コンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a>解剖学: [会議中] タブ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議中のタブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリアイコン(選択済み)**: 16ピクセル透明アプリのロゴ。|
|2|**アプリ名**|
|3|**ヘッダー**: アプリ名を含めます。|
|4|**閉じるボタン**: タブを閉じます。フッターのアクションではなく、常に右上の閉じるアイコンを使用します。|
|5|**通知バー**: エラーアラートはヘッダーの真下に表示され、iframeのコンテンツを20ピクセル下に押し下げます。|
|6|**iframe**: アプリのコンテンツを表示します。|

### <a name="spacing"></a>Spacing

280 ピクセル幅の iframe 領域内にエッジツーエッジに収まるように、会議中のタブを最適化します。 iframe の左右とタブ ヘッダーの間には、20 ピクセルのパディングがあります。 iframe は、タブの下部にフルブリードされます。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例は、会議内のタブ間隔の寸法を示しています。" border="false":::

### <a name="scrolling"></a>スクロール

Iframe の内容は垂直方向にスクロールする必要があります。 スクロールしたコンテンツのみが表示されます (上または下には何もありません)。 スクロールバーは iframe コンテンツの一部です。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、会議内のタブがスクロールする方法を示しています。" border="false":::

### <a name="navigation"></a>ナビゲーション

ナビゲーション レイヤーまたはコンテンツの負荷が高いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。 ユーザーは前のレイヤーに戻ることができる必要があります。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例は、会議内のナビゲーションを示しています。" border="false":::

## <a name="use-an-in-meeting-dialog"></a>会議内ダイアログを使用する

ミーティング内のダイアログは、ミーティングのTeamsステージに表示されます。 ユーザーの注意、確認、または操作が必要ですが、微妙であり、会議を中断しません。 軽くてタスク指向のシナリオでは、これらを慎重に使用する必要があります。

### <a name="use-cases"></a>使用例

会議中のダイアログは、参加者に次の操作を行うユーザー (会議の開催者など) によってトリガーされます。

* 簡単なフィードバックを提供する
* 短いアンケートまたはアンケートを実施する
* 承認の送信
* アラームを取得する

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議内のダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a>解剖学: 会議中ダイアログ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議内のダイアログの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**ヘッダー**: アプリアイコン、名前、アクション文字列、および閉じるアイコンが含まれます。|
|2|**iframe**: アプリのコンテンツを表示します。|

### <a name="anatomy-in-meeting-dialog-header"></a>解剖学: 会議内ダイアログヘッダー

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議内のダイアログ ヘッダーの構造構造を示しています。" border="false":::

2 つのヘッダバリアントがあります。 可能であれば、アバターと共にバリアントを使用して、ダイアログが人から来ることを補強します。

|カウンター|説明|
|----------|-----------|
|1|**アバター**: 会議中のダイアログを開始した人。|
|2|**アプリ アイコン**|
|3|**アプリ名**|
|4|**閉じるボタン**: ダイアログを閉じます。|
|5|**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。|

### <a name="responsive-behavior"></a>応答性の高い動作

会議中のダイアログ ボックスは、さまざまなシナリオを考慮してサイズが異なる場合があります。 パディングとコンポーネントサイズを維持してください。

* **幅**: サポートされているサイズ範囲内の任意の場所で、ダイアログの iframe の幅を指定できます。
* **高さ**: サポートされているサイズ範囲内の任意の場所で、ダイアログの iframe の高さを指定できます。 アプリのコンテンツが最大の高さを超えた場合、ユーザーが垂直方向にスクロールできるようにすることもできます。

実装するには、キーを使用して幅と高さを指定 [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) します。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを示しています。幅: 最小-280ピクセル(248ピクセルのiframe)。最大 --460 ピクセル(428 ピクセルの iframe)高さ:300ピクセル(iframe)。" border="false":::

## <a name="after-a-meeting"></a>会議の後

終了後に会議に戻ってアプリのコンテンツを表示できます。 この例では、会議の開催者は **[Contoso]** タブで投票結果を確認できます (注: 設計の観点から見ると、会議前と会議後のタブ エクスペリエンスの間に違いはありません)。

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例の図は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="interactions"></a>相互 作用

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="インタラクションの数を制限する方法を示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>実行: インタラクションの数を制限する

会議中のダイアログでは、ユーザーがすぐに何かを達成するのに役立たない不要なコンテンツを削除します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="不要な要素を導入しない方法を示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>しない: 不要な要素を導入する

複数の対話を行う単一の会議内のダイアログは、通話から気をそらす可能性があります。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="単一列のダイアログ レイアウトの使用方法を示す例を示します。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>行う: 単一列のダイアログ レイアウトを使用する

ダイアログは会議の中心にあるため、ユーザーの不満を避けるために、タスクの完了は迅速かつ簡単に行う必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議内線のスペースを乱雑にする必要はありません示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a>しない:スペースを乱雑にする

密または過度に構造化されたコンテンツは、特に会議中に、気が散り、圧倒的になる可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="単一列のタブ レイアウトを示す例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>実行: 単一列のタブ レイアウトを使用する

会議内のタブの狭い性質を考えると、1 つの列に内容を表示することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="複数の列を含むタブを表示する例。" border="false":::

#### <a name="dont-use-multiple-columns"></a>しない: 複数の列を使用する

会議内タブのスペースが限られているため、複数の列を含むレイアウトは推奨されません。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>コントロール

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="主コントロールを右揃えにする方法を示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a>実行: プライマリアクションを右揃えにします

最も視覚的に重いアクションを右端に配置することをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="主コントロールを左揃えにしない方法を示す例を示します。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>しない: 左または中央揃えアクション

これは、ダイアログ内のコントロール配置の標準Teamsパターンから外れ、上位のダイアログボックスと競合する可能性があります。

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議内のタブで垂直スクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a>行う: 垂直方向にスクロール

ユーザーは、Teams(および他の場所)で垂直スクロールを期待しています。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議内のタブで水平スクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a>しない: 水平方向にスクロールする

水平スクロールは、Teamsで予期される動作ではありません。 会議環境の他のキャンバスは、垂直方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>ワークフロー

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議中のタブでの複雑なシナリオの例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>行う: [ミーティング中] タブの複雑なシナリオを表示します。

アプリに複数のタスクが含まれている場合は、単一列レイアウトの [ミーティング中] タブを使用することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議内のダイアログで複雑なシナリオを示す例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>しない: 会議中のダイアログを複雑にする

会議中のダイアログは、簡単な対話を目的としています。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="暗いテーマを持つ会議の内線番号を示す例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a>行う: Teams色のトークンを使用する

Teams会議は、ユーザーがディスカッションや共有コンテンツに集中できるように、視覚や認知ノイズを低減するために、ダーク モード用に最適化されています。 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">カラー トークン (Fluent UI) の</a>使用について学習します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="既定の (明るい) テーマを持つ会議内線番号を示す例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a>しない: ハードコードの16進値

Teams色のトークンを使用しない場合、デザインの拡張性が低下し、管理に時間がかかります。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="会議内線番号を [戻る] ボタンで表示する例。" border="false":::

#### <a name="do-have-a-back-button"></a>行う:戻るボタンを持っている

会議内のタブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻ることができる必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="2 つの消し込みボタンを持つ会議内線番号を示す例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>しない: 別の却下ボタンを含める

[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既に [会議中] タブ自体を閉じるボタンが存在するため、問題が発生する可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議中のタブ内にモーダル (またはタスク モジュール) を表示する例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>注意: [会議中] タブ内でモーダルを避ける

既に狭い会議内タブのモーダル (タスク モジュールとも呼ばれます) は、コンテンツをラップして隠す可能性があります。

   :::column-end:::
:::row-end:::
