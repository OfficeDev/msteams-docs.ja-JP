---
title: Microsoft Teams での会議ダイアログの設計
author: heath-hamilton
description: Microsoft Teams の会議中のダイアログを設計するためのガイダンスとベストプラクティス。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 89e532e6dbd83e54269606f6e051fa377de68f62
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "48243334"
---
# <a name="design-an-in-meeting-dialog"></a>会議中のダイアログを設計する

会議中のダイアログは Teams の会議のステージに表示されます。 ユーザーの注意、確認、または対話が必要ですが、それは微妙で、会議に割り込むことはありません。

## <a name="use-cases"></a>使用例

会議中のダイアログは、参加者が必要になる可能性のあるユーザー (会議の開催者など) によってトリガーされます。

* 簡単なフィードバックを提供する
* 簡単なアンケートまたは投票を行う
* 承認の提出
* アラームを取得する

## <a name="example"></a>例

次の例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。 ご覧のように、コンテンツとタスクは軽量です。

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">完全なシナリオを参照してください (Figma)</a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">その他の使用例 (Figma) を参照してください。</a>

## <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="会議中のダイアログビューの UI の構造" border="false":::

1. **アプリ アイコン**
1. **アプリ名**
1. **アクション文字列**
1. **消しアイコン:** 1つのダイアログを閉じます。 フッター内のアクションではなく、右上にある閉じるアイコンを常に使用します。
1. **Webview**: サードパーティのアプリのコンテンツとボタンをすべて表示します ([Teams の標準] ボタンを推奨)。

### <a name="sizing"></a>決定

会議中のダイアログのサイズはさまざまなユースケースに応じて異なる可能性がありますが、常にパディングとコンポーネントのサイズを維持する必要があります。

* **高さ**: ダイアログの高さは、webview の内容によって決まります。 指定した最大の高さを超えているコンテンツに対して垂直方向のスクロールが行われます。
* **幅**: webview の幅は、指定した範囲内の絶対的な値です。

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="会議中のダイアログの可能な大きさを示す図高さ: ダイアログの高さは、webview の内容によって決まります。高さの最大値 (ユーザーが定義した値) を超える縦方向のスクロールが行われます。Min: なし。最大値: 400 ピクセル (320 ピクセル webview)。幅: webview の幅は、指定した範囲内の絶対的な値です。最小値: 288 ピクセル (256 ピクセル webview)。最大値: 468 ピクセル (436 ピクセル webview)。" border="false":::

## <a name="behavior"></a>動作

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>では、rest、読み込みなど、会議中の一般的なダイアログの動作を参照してください。

### <a name="position"></a>Position

会議中のダイアログは、会議のステージの中央に配置されます。 チームのシステムレベル通知のフレームワーク内でドラッグして作業することはできません。

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="会議中のダイアログの UI 構造を示す図" border="false":::

### <a name="aggregation"></a>Aggregation

一度に表示されるのは1つのダイアログのみで、最下部に最後に送信された時点からのスタックランキング。 ダイアログが解決または消去されると、次のダイアログボックスに移動します。

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">例 (Figma) を参照してください。</a>

### <a name="scrolling"></a>量

スクロールは、会議中のダイアログの webview 部分で行われます。 スクロールについて次の点に注意してください。

* 垂直方向にスクロールできるようにする必要があります。
* スクロールした内容のみが表示されます (何も上または下にありません)。

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="会議中のダイアログでの webview コンテンツのスクロール方法を示す図。" border="false":::

### <a name="buttons"></a>ボタン

[会議中] ダイアログボタンは、webview の一部です ([いくつかの例を参照してください](#best-practices))。

類似のコンポーネントとは異なり、ユーザーがボタンを選択すると、会議中のダイアログは閉じられます。

## <a name="components"></a>コンポーネント

会議中のダイアログは、主に、 <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent デザインシステム</a>を基にした次の<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI コンポーネント (figma)</a>で構築されています。

コンポーネント | ガイドライン | 例
 - | - | -
ボタン | プライマリボタンとセカンダリボタンは、中または small にすることができます。 | 応答を送信する
Input | 簡単なユーザー入力のフィールド。 ラベルのテキストにアイコンを含めることができます。  | フィードバックの入力
Dropdown | リストから1つ以上のオプションを選択します。 検索機能と複数選択機能を含めることができます。 | 言語を選択する
選択コントロール | 複数の選択肢またはラジオボタンのチェックボックスを使用して、1つの選択肢に対してトグルを行います。 選択の詳細については、スライダーを使用します。 | 投票の投票
アラート | 緊急メッセージ、エラー状態、または警告を表示するかどうかにかかわらず、メッセージは短くなければならず、ユーザーの現在のタスクが中断されることはありません。 | 応答を送信するときの表示の問題

## <a name="theming"></a>テーマ

### <a name="colors"></a>色

背景、foregrounds、および伝達の状態に推奨される <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">配色 (Figma)</a> を使用します。

### <a name="typography"></a>文字体裁

タイトル、本文テキスト、およびメタデータテキストに推奨される <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">フォントサイズと太さ (Figma)</a> を使用します。

## <a name="best-practices"></a>ベスト プラクティス

会議中のダイアログを使用すると通話がより効果的になることがありますが、obtrusive 過ぎると、着信呼び出しをすることもできます。 一般的に、ダイアログは控えめに使用し、次のベストプラクティスに従ってください。

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="ユーザーが会議に集中できるように、会議中のダイアログコンテンツを単一の画面に制限する方法を示す図。" border="false":::

#### <a name="do-keep-it-contained"></a>Do: 格納されたまま保持する

ユーザーが会議に集中できるように、会議ダイアログのコンテンツを1つの画面に制限します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="会議中のダイアログで、ユーザーがコンテンツ間を移動する必要がないことを示す図" border="false":::

#### <a name="dont-include-multiple-steps"></a>いいえ: 複数の手順を含めます

会議中のダイアログでは、ユーザーがコンテンツを移動する必要はありません。

   :::column-end:::
:::row-end:::

### <a name="interactions"></a>関係

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="ユーザーが迅速に作業を行うことができないような、不要なコンテンツを削除する理由を示す図。" border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="不要なコンテンツを削除する理由を示す別の図は、ユーザーにとってすぐには解決できないものです。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="複雑な対話が必要な場合、代わりに会議の右ウィンドウで1つの列を使用することを示す図" border="false":::

#### <a name="do-limit-number-of-interactions"></a>Do: 操作の数を制限する

不要なコンテンツを削除して、ユーザーがすばやく作業できないようにします。 複雑な対話が必要な場合は、代わりに [会議中] タブで単一の列を使用してコンテンツを表示することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="会議の中で会議中のダイアログ distracts の相互作用が多すぎることを示す図。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>いいえ: 不要な要素を紹介します。

複数の対話を含む1つの会議中のダイアログを設計することもできますが、会議の参加者が多くなることがあります。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="会議中のダイアログの理想的なレイアウトを示す図" border="false":::

#### <a name="do-use-single-column-layouts"></a>手順: 単一列のレイアウトを使用する

ダイアログは会議ステージの中央にあります。タスクの完了は、ユーザーの不満を回避するために、迅速かつシンプルにする必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="推奨されていない会議中のダイアログのレイアウトを示す図" border="false":::

#### <a name="dont-clutter-the-space"></a>[しない: スペースを整頓する」

高密度または過度に構造化されたコンテンツは、特に会議中に煩雑で圧倒的なものになる可能性があります。

   :::column-end:::
:::row-end:::

### <a name="size"></a>Size

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="会議中のダイアログのサイズを常に同じにする方法を示す図。" border="false":::

#### <a name="do-keep-it-consistent"></a>実行: 一貫性を保つ

会議ダイアログボックスは常に同じ場所に表示されるため、これは重要です。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="異なるダイアログサイズを使用する方法を示す図" border="false":::

#### <a name="dont-always-fit-to-the-content"></a>いいえ: 常にコンテンツに合わせる

水平方向のスクロールを避けようとしていますが、同じアプリ内の複数の会議中のダイアログのサイズが一貫していない場合があります。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>コントロール

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="会議中のダイアログにボタンを配置する場所を示す図" border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do: 右揃えで主な操作を行います。

最も視覚的に大きなアクションは、右端の位置に配置することをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="会議中のダイアログにボタンを配置しない場所を示す図。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>いいえ: 左揃えまたは中央揃えのアクション

これは、ダイアログでのコントロールの配置に関する標準 Teams パターンとは異なり、一番上にあるダイアログと競合する可能性があります。

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>アクセシビリティ

アクセシビリティの詳細については、「 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>」を参照してください。

## <a name="resources"></a>リソース

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams の会議拡張機能 Figma ファイル</a>

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。

> [!div class="nextstepaction"]
> [設計検証ガイドラインの確認](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
