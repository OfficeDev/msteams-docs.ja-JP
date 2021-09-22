---
title: 会議拡張機能の設計
author: heath-hamilton
description: 会議でアプリを設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 5597752ad8698e45c33ec7e116cd684f22ff98a3
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475700"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>会議の拡張機能Microsoft Teams設計する

アプリを作成して、会議の生産性を高めることができます。 たとえば、会議中にアンケートを完了したり、会議のフローを中断しない簡単なリマインダーを送信したりします。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>会議の拡張機能を追加する

ユーザーは、会議の前と会議中に会議拡張機能を追加できます。 また、特定の会議用のアプリを、その会議ストアから直接Teamsすることもできます。

### <a name="add-before-a-meeting"></a>会議の前に追加する

会議の詳細で、ユーザーは [タブの追加 **] +** を選択してアプリの飛び出しを開き、会議用に最適化されたアプリを検索できます。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線情報を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a>会議中に追加する

#### <a name="mobile"></a>モバイル

アプリが追加された後 (デスクトップなど)、ユーザーは [その他] を選択して会議でアプリに **アクセスできます** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 。

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="例は、モバイルでの会議中に会議の内線情報を追加する方法を示しています。" border="false":::

#### <a name="desktop"></a>Desktop

会議で、ユーザーは [アプリの **追加]** を選択 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **し**、必要なアプリを選択できます。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線情報を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a>会議の前

会議の前に、アプリはタブ内のユーザーが利用できます。次の例は、会議中にユーザーが回答するアンケートの下書き質問を示しています。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細でコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>解剖学: [会議] タブ (会議の前と後)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前と後の会議タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。|
|3|**iframe**: アプリのコンテンツを表示します。|

### <a name="design-with-ui-templates"></a>UI テンプレートを使用した設計

会議タブを設計するにはTeams UI テンプレートのいずれかを使用します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 左側のナビゲーション コンポーネントは、タブにナビゲーションが必要な場合に役立ちます。 一般に、ナビゲーションは最小限に抑えます。

## <a name="use-an-in-meeting-tab"></a>[会議内] タブを使用する

[会議内] タブは、会議中の共同作業を強化するキャンバスです。 出席者は、共有ビューまたは役割ベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示および操作できます。

### <a name="use-cases"></a>使用例

ユーザーは、[会議内] タブを使用して次の場合があります。

* 詳細なフィードバックを提供します。 たとえば、ジョブ候補を評価します。
* 会議参加者のポーリング、アンケート、またはタスク アイテムを作成します。
* 会議に関連するメモを表示します。 たとえば、販売リードに関する情報です。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="例は、モバイル上の会議内タブでポーリング コンテンツを表示する方法を示しています。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、会議内タブでポーリング コンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a>解剖学: [会議中] タブ

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議内タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン (選択)**: 16 ピクセルの透明なアプリ ロゴ。|
|2|**アプリ名**|
|3|**ヘッダー**: アプリ名が含まれます。|
|4 |**[閉じる]** ボタン: タブを閉じます。フッターのアクションではなく、常に右上の閉じるアイコンを使用します。|
|5|**通知バー**: エラー通知はヘッダーの直下に表示され、iframe コンテンツを 20 ピクセル下にプッシュします。|
|6 |**iframe**: アプリのコンテンツを表示します。|

### <a name="spacing"></a>Spacing

280 ピクセル幅の iframe 領域内にエッジからエッジに合わせて会議内タブを最適化します。 iframe の左側と右側、およびタブ ヘッダーの間には 20 ピクセルのパディングがあります。 iframe はタブの下部に完全にブリードされます。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例では、会議中のタブ間隔のディメンションを示します。" border="false":::

### <a name="scrolling"></a>スクロール

スクロールを許可する場合は、次のことを覚えておいてください。

* iframe コンテンツ内のコンテンツは垂直方向にのみスクロールする必要があります。
* ユーザーはスクロールしたコンテンツのみを表示する必要があります (上または下に何も表示されません)。 
* スクロール バーは、iframe コンテンツの一部です。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、会議内タブのスクロール方法を示しています。" border="false":::

### <a name="navigation"></a>ナビゲーション

ナビゲーション レイヤーやコンテンツが多いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。 ユーザーは前のレイヤーに戻る必要があります。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例では、会議内ナビゲーションを示します。" border="false":::

## <a name="use-an-in-meeting-dialog"></a>会議内ダイアログの使用

会議中のダイアログは、会議ステージTeams表示されます。 ユーザーの注意、確認、またはやり取りが必要ですが、微妙であり、会議を中断しません。 これらの使用は、軽くてタスク指向のシナリオに対して使用する必要があります。

### <a name="use-cases"></a>使用例

会議中のダイアログは、参加者が次の操作を行うユーザー (会議の開催者など) によってトリガーされます。

* 簡単なフィードバックを提供する
* 短いアンケートまたは投票を行う
* 承認を送信する
* アラームを取得する

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="例は、モバイルで会議内ダイアログを使用する方法を示しています。" border="false":::

### <a name="desktop"></a>Desktop

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
|4 |**[閉じる]** ボタン: ダイアログを閉じます。|
|5|**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。|

### <a name="responsive-behavior-in-meeting-dialogs"></a>応答性の高い動作: 会議中のダイアログ

会議内のダイアログは、さまざまなシナリオを考慮してサイズが異なる場合があります。 パディングとコンポーネントのサイズは必ず維持してください。

* **Width**: ダイアログの iframe の幅は、サポートされているサイズ範囲内の任意の場所で指定できます。
* **Height**: ダイアログの iframe の高さは、サポートされているサイズ範囲内の任意の場所で指定できます。 アプリのコンテンツが最大の高さを超えた場合は、ユーザーが垂直方向にスクロールすることもできます。

実装するには、キーを使用して幅と高さを指定 [`externalResourceUrl`](~/apps-in-teams-meetings/API-references.md#notificationsignal-api) します。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを表示します。幅: 最小--280 ピクセル (248 ピクセルの iframe)。Max---460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="use-the-shared-meeting-stage"></a>共有会議ステージの使用

共有会議ステージは、会議参加者がリアルタイムでアプリ コンテンツと対話し、共同作業を行うのに役立ちます。 たとえば、ユーザーは会議に集中して、ドキュメントの編集、ホワイトボードによるブレインストーミング、ダッシュボードの確認を行います。

会議ステージに共有されるアプリは、共有画面と同じ領域を占有します。 ステージは、すべての会議参加者の向きを変更します。

> [!NOTE]
> 現在、アプリがデスクトップ上のステージに共有されている場合は、モバイル会議のユーザーにのみ表示されます。
 
### <a name="use-cases"></a>使用例

共有会議のステージは、共同作業と参加に関するすべてです。 開始に役立つシナリオの例を次に示します。

:::row:::
   :::column span="1":::

**編集とレビュー**: 会議のすべてのユーザーと一緒にダッシュボードと計画に取り組む。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="例は、共有会議ステージでレビュー中のダッシュボードを示しています。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**ホワイトボード:** 共有キャンバスで一緒に描画してアイデアを作成します。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="例は、共有会議ステージのホワイトボードを示しています。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**クイズ**: 対話的な資料を使って知識をテストし、洞察を得る。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="例では、共有会議ステージでクイズを表示します。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a>解剖学: 共有会議ステージ

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="イメージは、共有会議ステージの設計構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン**: 強調表示されたアイコンは、アプリの会議中タブが開いている状態を示します。|
|2|**[会議ステージに共有] ボタン**: アプリを会議ステージに共有するエントリ ポイント。 共有会議ステージを使用するアプリを構成した場合に表示されます。|
|3|**iframe**: アプリのコンテンツを表示します。|
|4 |**[共有を停止する**] ボタン: 会議ステージへのアプリの共有を停止します。 共有を開始した参加者にのみ表示されます。|
|5|**発表者の属性**: アプリを共有した参加者の名前を表示します。|

### <a name="responsive-behavior-shared-meeting-stage"></a>応答性の高い動作: 共有会議ステージ

会議ステージに共有されるアプリのサイズは、会議の状態と、ユーザーがウィンドウのサイズを変更する方法によって異なります。 ブラウザーと同様に、ナビゲーションとコントロールのパディングと応答性の高いレイアウトを維持します。

* **サイド パネル**: ユーザーは、会議中にいつでもサイド パネルを開き、チャットしたり、名簿を表示したり、アプリ (つまり、会議内タブ) を使用することができます。 パネルが開いているときにステージが動的に再配置されます。
* **ビデオとオーディオ のグリッド**: ビデオとオーディオ のグリッドは常に表示され、会議の参加者を表示できます。 ユーザーが会議で他のユーザーにスポットライトを当てたりピンを固定したりすると、参加者グリッドの高さまたは幅は、向きに応じて増加します。

#### <a name="meeting-stage-without-side-panel"></a>会議ステージ (サイド パネルなし)

サイド パネルが開いていない場合、会議ステージは既定で 994x678 ピクセルで、最小 792x382 ピクセルを指定できます。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="サイド パネルを閉じた共有会議ステージの応答性を示す画像。" border="false":::

#### <a name="meeting-stage-with-side-panel"></a>会議ステージ (サイド パネル付き)

サイド パネルが開いている場合、会議ステージは既定で 918x540 ピクセルで、最小 472x382 ピクセルを指定できます。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="サイド パネルを開いた状態で共有された会議ステージの応答性を示す画像。" border="false":::

## <a name="after-a-meeting"></a>会議後

会議の終了後に会議に戻り、アプリのコンテンツを表示できます。 この例では、会議の開催者は **[Contoso]** タブで投票結果を確認できます(注: デザインの観点から、会議前と会議後のタブ エクスペリエンスの違いはありません)。

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例の図は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

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

複数の操作を含む 1 つの会議内ダイアログは、会議の邪魔になる可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="フォーカス環境を作成する方法を示す例。" border="false":::

#### <a name="do-create-a-focused-environment"></a>Do: フォーカス環境を作成する

アプリのエクスペリエンスを会議のステージに対してスコープを設定することをお勧めします。 サイド パネルの会議内タブを、特定のシナリオのセカンダリプライベート ビューとして使用できます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="会議中に競合するサーフェスを含めない方法を示す例。" border="false":::

#### <a name="dont-include-competing-surfaces"></a>[しない]: 競合するサーフェスを含める

アプリは、ステージでの共同作業や会議中のダイアログへの応答など、ユーザーに一度に 1 つのサーフェスにのみ集中を求める必要があります。 (注: アプリがステージ上にある間は、他のアプリによってダイアログがトリガーされた状態を維持できない)。 

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="1 列のダイアログ レイアウトを使用する方法を示す例。" border="false":::

#### <a name="do-use-a-one-column-dialog"></a>Do: 1 列のダイアログを使用する

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

#### <a name="do-use-a-one-column-tab"></a>Do: 1 列のタブを使用する

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

これは、ダイアログ内のコントロールTeamsの標準のパターンから離れ、上部のダイアログボックスと競合する可能性があります。

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>スクロール

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議内タブで垂直スクロールを表示する例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="共有会議ステージで垂直スクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a>Do: 垂直方向にスクロールする

ユーザーは、 (および他の場所) Teams垂直スクロールを期待します。 これは、ユーザーが x 軸と y 軸をパンできるホワイトボードなどのクリエイティブ なキャンバスがある場合は適用されません。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議内タブに水平スクロールを表示する例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="共有会議ステージで水平スクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a>[しない]: 水平方向にスクロールする

水平方向のスクロールは、(会議環境を含む) Teams予期される動作ではありません。

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

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="暗いテーマで会議の拡張機能を表示する別の例。" border="false":::

#### <a name="do-focus-on-dark-theme"></a>Do: 暗いテーマに焦点を当てる

Teams会議は暗いテーマに最適化され、視覚的および認知的なノイズを減らし、ユーザーがディスカッションと共有コンテンツに集中できます。 特定の種類のアプリ (ホワイトボードやドキュメント編集など) では、暗いキャンバスは必要ない場合があります。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="会議のテーマと一致しない色で会議の拡張機能を表示する例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="会議のテーマと一致しない色の会議拡張機能を示す別の例。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>[しない]: 見慣れない色を使用する

会議環境と衝突する色が気を散らし、ユーザーのネイティブな表示が少Teams。 通話テーマのニュートラルTeams[含む、](https://developer.microsoft.com/fluentui#/styles/web/colors/products)カラー ランプの詳細について学習します。

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

### <a name="responsive-behavior"></a>応答性の高い動作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="会議拡張機能のサイズを適切に変更する方法を示す例。" border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>Do: アプリのサイズ変更とスケーリングを迅速に行う

アプリのコンテンツは、小さいウィンドウで動的にサイズを変更して凝縮する必要があります。 アプリのメイン ナビゲーションとフローティング コントロールを表示します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="会議拡張機能のサイズを適切に変更しない方法を示す例。" border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>[しない]: プライマリ UI コンポーネントをトリミングまたはクリップする

画面外のナビゲーションとコントロールをフローティングし、スクロールして検索する必要がある場合、ユーザーにとって混乱を招く可能性があります。 アプリコンテンツが iframe に収まらない場合は、アプリのコンテンツを水平方向にスクロールしてはならない。

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会議用にアプリを構成する](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
