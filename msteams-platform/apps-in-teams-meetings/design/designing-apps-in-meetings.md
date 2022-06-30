---
title: 会議拡張機能の設計
author: heath-hamilton
description: Teams 会議でアプリの会議拡張機能を設計する方法について説明します。 Microsoft Teams UI Kit の UI テンプレートを使用して、会議タブの設計に役立ちます。
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 7df89357f5c052fec5ff2a82cd721b9b7c06da94
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558087"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Microsoft Teams 会議拡張機能の設計

会議の生産性を高めるようアプリを作成できます。 たとえば、通話中にアンケートを記入するよう依頼したり、会議のフローを中断しない簡単なリマインダーを送信したりします。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit には、必要に応じて変更できる要素を含む、より包括的なボット デザインのガイドラインが掲載されています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>会議拡張機能の追加

ユーザーは、会議の前後に会議の延長を追加できます。 また、Teams ストアから特定の会議用のアプリを直接追加することもできます。

### <a name="add-before-a-meeting"></a>会議の前

会議の詳細で、ユーザーは **タブ +** を追加してアプリのポップアップを開き、会議用に最適化されたアプリを見つけることができます。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例では、会議の前に会議の延長を追加する方法を示します":::

### <a name="add-during-a-meeting"></a>会議中に追加

#### <a name="mobile"></a>Mobile

アプリが追加されると (デスクトップなど)、ユーザーは会議で [**その他**:::image type="icon" source="../../assets/icons/teams-client-more.png":::] を選択してアプリにアクセスできます。

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="例では、モバイルでの会議中に会議の延長を追加する方法を示します":::

#### <a name="desktop"></a>Desktop

会議では、ユーザーは **[その他]** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: > **[アプリの追加** を選択し、目的のアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例では、会議中に会議の延長を追加する方法を示します。":::

## <a name="before-a-meeting"></a>会議の前

会議の前に、アプリはタブでユーザーが利用できます。次の例は、会議中に回答するアンケートの質問の下書きを示しています。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例では、通話の前に会議の詳細のコンテンツをアプリする方法を示します":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>構造: [会議] タブ (会議の前後)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例では、会議の前後の会議タブの構造解剖を示します。":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。|
|3|**iframe**: アプリのコンテンツを表示します。|

### <a name="design-with-ui-templates"></a>UI テンプレートを使用したデザイン

次の Teams UI テンプレートのいずれかを使用して、タブを設計します:

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): かんばんボードまたはスイム レーンと呼ばれることもあるタスク ボードは、作業項目またはチケットのステータスを追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): タブにナビゲーションが必要な場合は、左側のナビゲーション コンポーネントが役立ちます。 一般に、タブ ナビゲーションは最小限に抑える必要があります。

## <a name="use-an-in-meeting-tab"></a>会議中のタブを設計する

会議中タブは、会議中の共同作業を強化するためのキャンバスです。 出席者は、共有ビューまたはロールベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示および操作できます。

### <a name="use-cases"></a>使用例

ユーザーは会議中タブを使用して、次の場合に使用できます:

* 詳細なフィードバックを提供してください。 たとえば、ジョブ候補を評価します。
* 会議の参加者の投票、アンケート、またはタスク アイテムを作成します。
* 会議に関連するメモを表示します。 たとえば、潜在顧客に関する情報などです。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="例では、モバイルの会議中タブに投票コンテンツを表示する方法を示します。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例では、会議中タブで投票コンテンツを表示する方法を示します。":::

### <a name="anatomy-in-meeting-tab"></a>構造: 会議中タブ

:::image type="content" source="../../assets/in-meeting-tab-anatomy.png" alt-text="例では、会議中タブの構造構造を示します。":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン (選択済み)**: 16 ピクセルの透明なアプリ ロゴ。|
|2|**アプリ名**|
|3|**ヘッダー**: アプリ名が含まれます。|
|4|**[閉じる] ボタン**: タブを閉じます。フッターのアクションではなく、常に右上の閉じるアイコンを使用します。|
|5|**[通知] バー**: エラー アラートがヘッダーのすぐ下に表示され、残りの iframe コンテンツが 20 ピクセル下にプッシュされます。|
|6 |**iframe**: アプリのコンテンツを表示します。|

### <a name="spacing"></a>Spacing

280 ピクセル幅の iframe 領域内でエッジ ツー エッジに合わせて会議中タブを最適化します。 iframe の左側と右側、およびタブ ヘッダーの間に 20 ピクセルのパディングがあります。 iframe はタブの下部まで完全に裁ち落としとなります。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例では、会議中タブの間隔の大きさが表示されます。":::

### <a name="scrolling"></a>スクロール

スクロールを許可する場合は、次の点に注意してください:

* iframe コンテンツ内のコンテンツは、垂直方向にのみスクロールできます。
* ユーザーには、スクロールしたコンテンツのみが表示されます (上または下に何も表示されません)。
* スクロール バーは iframe コンテンツの一部です。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例では、会議中タブのスクロール方法を示します。":::

### <a name="navigation"></a>ナビゲーション

ナビゲーション レイヤーやコンテンツが多いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。 ユーザーは前のレイヤーに戻ることができる必要があります。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例では、会議中のナビゲーションが表示されます。":::

## <a name="use-an-in-meeting-dialog"></a>会議中のダイアログを設計する

Teams 会議ステージに会議中ダイアログが表示されます。 ユーザーの注意、確認、または対話が必要ですが、微妙であり、会議を中断しません。 軽くてタスク指向のシナリオには、頻繁に使用しないようにする必要があります。

### <a name="use-cases"></a>使用例

会議中ダイアログは、参加者が次の操作を行うユーザー (会議の開催者など) によってトリガーされます。

* 簡単なフィードバックを提供します。
* 短いアンケートまたは投票を行います。
* 承認を送信します。
* リマインダーを取得します。

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="例では、会議中ダイアログを使用する方法を示しています。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="会議中ダイアログを使用する方法を示す例。":::

### <a name="anatomy-in-meeting-dialog"></a>構造: 会議中ダイアログ

:::image type="content" source="../../assets/in-meeting-dialog-anatomy.png" alt-text="例では、会議中ダイアログの構造解剖を示しています。":::

|カウンター|説明|
|----------|-----------|
|1|**ヘッダー**: アプリ アイコン、名前、アクション文字列、閉じるアイコンが含まれます。|
|2|**iframe**: アプリのコンテンツを表示します。|

### <a name="anatomy-in-meeting-dialog-header"></a>構造: 会議中ダイアログ ヘッダー

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例では、会議中のダイアログ ヘッダーの構造構造を示します。":::

ヘッダーには 2 つのバリアントがあります。 可能であれば、バリアントをアバターと共に使用して、ダイアログが人物から送信されていることを強調します。

|カウンター|説明|
|----------|-----------|
|1|**アバター**: 会議中ダイアログを開始するユーザー。|
|2|**アプリ アイコン**|
|3|**アプリ名**|
|4|**[閉じる] ボタン**: ダイアログを閉じます。|
|5|**操作文字列**: 通常、ダイアログを開始したユーザーを示します。|

### <a name="responsive-behavior-in-meeting-dialogs"></a>応答性の高い動作: 会議中ダイアログ

会議中のダイアログのサイズは、シナリオによって異なる場合があります。 パディングとコンポーネントのサイズは必ず維持してください。

* **幅**: サポートされているサイズ範囲内の任意の場所でダイアログの iframe の幅を指定できます。
* **高さ**: サポートされているサイズ範囲内の任意の場所で、ダイアログの iframe の高さを指定できます。 アプリのコンテンツが最大の高さを超えた場合に、ユーザーが垂直方向にスクロールできるようにすることもできます。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例では、会議中のダイアログが表示されます。幅: 最小 - 280 ピクセル (248 ピクセル iframe)。最大 460 ピクセル (428 ピクセル iframe)。高さ: 300 ピクセル (iframe).":::

## <a name="use-the-shared-meeting-stage"></a>共有会議ステージを使用する

ユーザーが会議ステージでアプリ コンテンツの一部またはすべてを共有および操作することを許可できます。 会議中にユーザーがこの機能を使用する方法の例を次に示します。

* ドキュメントを編集する。
* ホワイト ボード
* ダッシュボードを確認する。
* ビデオを見る。
* ゲームをプレイしています。

会議ステージで共有されるアプリは、共有画面と同じ領域を占有します。 また、ステージはすべての会議参加者の向きを同じように方向にさせます。

> [!NOTE]
> 現在、モバイル ユーザーは会議ステージでアプリのコンテンツを共有できません。 ただし、デスクトップから共有されているコンテンツを表示できます。

### <a name="use-cases"></a>使用例

共有会議ステージは、コラボレーションと参加に関わるものです。 作業を開始するのに役立つシナリオの例を次に示します。

:::row:::
   :::column span="1":::

**編集とレビュー**: ダッシュボードの詳細と会議の全員との計画。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="例では、共有会議ステージでレビューされているダッシュボードが表示されます。":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="例では、共有会議ステージでレビューされているダッシュボード コンポーネントを示しています。":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**ホワイトボード**: 共有キャンバスで一緒に描画してアイデアを作成します。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="例では、共有会議ステージ上のホワイトボードを示しています。":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**テスト**: 知識をテストし、対話型の資料で分析情報を得る。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="例では、共有会議ステージでクイズを示しています。":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-share-all-app-content-to-a-meeting"></a>構造: すべてのアプリ コンテンツを会議に共有する

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="画像は、すべてのアプリ コンテンツが共有されている場合の共有会議ステージの設計構造を示しています。":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン**: 強調表示されたアイコンは、アプリの会議中タブが開かれていることを示します。|
|2|**[会議に共有] ボタン**: アプリを会議と共有するエントリ ポイント。 共有会議ステージを使用するようにアプリを構成した場合に表示されます。|
|3|**発表者の属性**: アプリを共有した参加者の名前を表示します。|
|4|**iframe**: アプリのコンテンツを表示します。|
|5|**[共有の停止] ボタン**: 会議ステージへのアプリの共有を停止します。 共有を開始した参加者に対してのみ表示されます。|

### <a name="anatomy-share-specific-app-content-to-a-meeting"></a>構造: 特定のアプリ コンテンツを会議に共有する

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy-component.png" alt-text="画像は、特定のアプリ コンテンツのみが共有されている場合に、共有会議ステージの設計構造を示しています。":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン**: 強調表示されたアイコンは、アプリの会議中タブが開かれていることを示します。|
|2|**[会議に共有] ボタン**: アプリを会議と共有するエントリ ポイント。 一貫したエクスペリエンスを実現するには、常に標準の Teams 共有アイコンを使用します。 "**会議に共有**" が推奨される既定のテキストですが、ユース ケースに合わせてカスタマイズすることもできます。 たとえば、ゲーム アプリの場合は "**一緒にプレイしよう**"、ビデオ アプリの場合は "**一緒に見よう**" などです。 いずれの方法でも、操作により、会議の全員と共有の対話型エクスペリエンスが作成されることを明確にします。|
|3|**発表者の属性**: アプリを共有した参加者の名前を表示します。|
|4|**iframe**: アプリのコンテンツを表示します。|
|5|**[共有の停止] ボタン**: 会議ステージへのアプリの共有を停止します。 共有を開始した参加者に対してのみ表示されます。|

### <a name="responsive-behavior-shared-meeting-stage"></a>応答性の高い動作: 共有会議ステージ

会議ステージで共有されるアプリのサイズは、会議の状態と、ユーザーによるウィンドウのサイズを変更方法によって異なります。 ブラウザーと同様に、ナビゲーションとコントロールのパディングと応答性の高いレイアウトを維持します。

* **サイド パネル**: ユーザーは、会議中にいつでもサイド パネルを開いてチャットしたり、名簿を表示したり、アプリ (つまり、会議中タブ) を使用したりできます。 ステージは、パネルが開いているときに動的に再配置されます。
* **ビデオとオーディオ グリッド**: ビデオグリッドとオーディオ グリッドは、会議の参加者を表示するために常に表示されます。 ユーザーが会議の参加者にスポットライトを当てたりピン留めしたりすると、印刷の向きに応じて参加者グリッドの高さや幅が増えます。

#### <a name="meeting-stage-without-side-panel"></a>会議ステージ (サイド パネルなし)

サイド パネルが開いていない場合、会議ステージは既定で 994 x 678 ピクセルで、最小 792 x 382 ピクセルにすることができます。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="サイド パネルを閉じた共有会議ステージの応答性を示す画像。":::

#### <a name="meeting-stage-with-side-panel"></a>会議ステージ (サイド パネル付き)

サイド パネルが開いている場合、会議ステージは既定で 918 x 540 ピクセルで、最小 472 x 382 ピクセルにすることができます。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="サイド パネルを開いた共有会議ステージの応答性を示す画像。":::

## <a name="after-a-meeting"></a>会議後

会議が終了した後に会議に戻り、アプリのコンテンツを表示できます。 この例では、会議の開催者は、**Contoso** タブで投票結果を確認できます (注: デザインの観点から見ると、会議前タブと会議後タブのエクスペリエンスに違いはありません)。

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例の図は、会議後のタブを示しています。":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="interactions"></a>相互作用

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="例では、相互作用の数を制限する方法を示しています。":::

#### <a name="do-limit-the-number-of-interactions"></a>実行: 操作の数を制限する

会議中ダイアログの場合は、ユーザーが何かを迅速にやり遂げるのに不要なコンテンツを削除します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="例では、不要な要素を導入しない方法を示しています。":::

#### <a name="dont-introduce-unnecessary-elements"></a>禁止: 不要な要素の導入

1 つの会議中ダイアログに複数の相互作用があると、会議から注意散漫になってしまう可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="例では、優先環境を作成する方法を示しています。":::

#### <a name="do-create-a-focused-environment"></a>実行: 優先環境の作成

アプリのエクスペリエンスは、会議ステージのみに限定することをお勧めします。 特定のシナリオでは、サイド パネルの 会議中タブをセカンダリのプライベート ビューとして使用できます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="例では、会議中に競合するサーフェイスを含めないようにする方法を示しています。":::

#### <a name="dont-include-competing-surfaces"></a>禁止: 競合するサーフェイスを含める

アプリは、ステージで共同作業を行う場合でも、会議中のダイアログに応答する場合でも、一度に 1 つのサーフェイスにフォーカスするようにユーザーに求める必要があります。 (注: アプリがステージ上にある間は、他のアプリによってトリガーされるダイアログを保持することはできません)。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="例では、単一列のダイアログ レイアウトの使用方法を示しています。":::

#### <a name="do-use-a-one-column-dialog"></a>実行: 1 列のダイアログを使用

ダイアログは会議ステージの中心にあるため、ユーザーの不満を避けるために、タスクの完了を迅速かつ簡単にする必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="例では、会議拡張機能のスペースを取り散らかさないようにする必要があることを示しています。":::

#### <a name="dont-clutter-the-space"></a>禁止: スペースを取り散らかす

密度の高いコンテンツや過度に構造化されたコンテンツは、特に会議中に、気が散り、圧倒されてしまうことがあります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="例では、単一列のタブ レイアウトを示しています。":::

#### <a name="do-use-a-one-column-tab"></a>実行: 1 列のタブを使用する

会議中タブは狭いという性質があるので、内容を 1 つの列に表示することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="例では、複数の列を含むタブを示しています。":::

#### <a name="dont-use-multiple-columns"></a>禁止: 複数の列の使用

会議中タブのスペースが限られているため、複数の列を含むレイアウトはお勧めしません。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>コントロール

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="例では、プライマリ コントロールを右揃えする方法を示しています。":::

#### <a name="do-right-align-the-primary-action"></a>実行: 主要操作を右揃えにする

最も視覚的に最も重い操作をいちばん右側の位置に置くことをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="例では、主要操作を左揃えにしない方法を示しています。":::

#### <a name="dont-left-or-center-align-actions"></a>禁止: 操作を左揃えまたは中央揃えにする

そうした配置は、ダイアログでのコントロールの配置に関する標準的な Teams パターンから逸脱しており、上位のダイアログと競合する可能性があります。

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>スクロール

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="例では、会議中タブで垂直スクロールを示しています。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="例では、共有会議ステージで垂直スクロールを示しています。":::

#### <a name="do-scroll-vertically"></a>実行: 垂直方向にスクロールする

ユーザーは、Teams (およびその他の場所) での垂直スクロールを想定してます。 これは、ユーザーが x 軸と y 軸をパンできるホワイトボードなどのクリエイティブ キャンバスがある場合は適用されない場合があります。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="例では、会議中タブで水平スクロールを示しています。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="例では、共有会議ステージで水平スクロールを示しています。":::

#### <a name="dont-scroll-horizontally"></a>禁止: 横方向にスクロール

横方向のスクロールは、Teams (会議環境を含む) で想定される動作ではありません。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>ワークフロー

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="例では、会議中タブで複雑なシナリオを示しています。":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>実行: 会議中タブでのサーフェイスの複雑なシナリオ

アプリに複数のタスクが含まれている場合は、単一列レイアウトの会議中タブを使用することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="例では、会議中ダイアログで複雑なシナリオを示しています。":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>禁止: 会議中のダイアログを複雑にする

会議中のダイアログは、短時間のやり取りを目的としています。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="例では、ダーク テーマの会議拡張機能を示しています。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="もう一例でも、ダーク テーマの会議拡張機能を示しています。":::

#### <a name="do-focus-on-dark-theme"></a>実行: ダーク テーマにフォーカスする

Teams 会議は、ユーザーがディスカッションや共有コンテンツに集中できるように、視覚的および認知的なノイズを減らすのに役立つダーク テーマ用に最適化されています。 特定の種類のアプリ (ホワイトボードやドキュメントの編集など) では、暗いキャンバスは必要ありません。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="例では、会議テーマと一致しない色の会議拡張機能を示しています。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="もう 1 つの例でも会議テーマと一致しない色の会議拡張機能を示しています。":::

#### <a name="dont-use-unfamiliar-colors"></a>禁止: 使い慣れていない色を使用する

会議環境と競合する色を使うと注意散漫になり、Teams に対してあまりネイティブに見えなくなる可能性があります。 通話テーマのニュートラルを含む Teams の [色傾斜](https://developer.microsoft.com/fluentui#/styles/web/colors/products) について説明します。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="例では、[戻る] ボタンを含む会議拡張機能を示しています。":::

#### <a name="do-have-a-back-button"></a>実行: [戻る] ボタンを付ける

会議中タブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻ることができる必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="例では、2 つの [閉じる] ボタンを含む会議の延長を示しています。":::

#### <a name="dont-include-another-dismiss-button"></a>禁止: 別の [閉じる] ボタンを含める

会議中タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既に会議中タブ自体を閉じるボタンがあるため、問題が発生する可能性があります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="例では、会議中タブ内のモーダルを示しています。":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>注意: 会議中タブ内でモーダルの使用は避けてください。

既に狭くなっている会議中タブにモーダル (タスク モジュールとも呼ばれます) を使用すると、コンテンツが折り返し表示になり、不明瞭になってしまいます。

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a>応答性の高い動作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="例では、会議の内線番号を適切に変更する方法を示しています。":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>実行: アプリのサイズを変更し、スケーリングし、応答性を高める

アプリ コンテンツのサイズを動的に変更し、より小さいウィンドウで簡素化する必要があります。 アプリのメイン ナビゲーションとフローティング コントロールを表示したままにします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="例では、会議拡張機能が適正にサイズ変更されていない例を示しています。":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>禁止: 主要 UI コンポーネントをトリミングまたはクリップする

移動ウィンドウナビゲーションとコントロールを画面外にし、表示するのにスクロールが必要になってしまうと、ユーザーにとって混乱を招く可能性があります。 アプリのコンテンツは、iframe に収まらないときに水平方向にスクロールしないでください。

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会議用にアプリを構成する](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
