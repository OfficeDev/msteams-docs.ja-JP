---
title: Microsoft Teams を会議のタブで設計する
author: heath-hamilton
description: Microsoft Teams の [会議中] タブを設計するためのガイダンスとベストプラクティスについて説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 91981ab79c8e50483568dd0dc750b4e9b3fdef24
ms.sourcegitcommit: b01986739a05c65094618fbe76aeb53d038b1c74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48178324"
---
# <a name="design-an-in-meeting-tab"></a>[会議中] タブを設計する

[会議中] タブは、会議中に共同作業を補強するためのキャンバスです。 [チーム] タブの機能に基づいて、参加者は共有ビューまたはロールベースのビューを使用して、会議ステージ外の専用の領域でアプリコンテンツを表示したり操作したりできます。

## <a name="use-cases"></a>ユース ケース

[会議中] タブを使用して、次のことを行うことができます。

* 詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)
* 会議の参加者用に投票、調査、または仕事アイテムをすばやく作成する
* 会議に関連するメモを表示する (たとえば、販売リードに関する情報)

## <a name="example"></a>例

次の例は、アンケートのアプリコンテンツを表示する [会議中] タブを示しています。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="例では、会議の開催者からの会議タブは、会議の開催者の視点から見ることができるようになります。":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">完全なシナリオを参照してください (Figma)</a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">その他の使用例 (Figma) を参照してください。</a>

## <a name="anatomy"></a>構造

[会議中] タブには、次のディメンションを使用してアプリのコンテンツが表示されます。

* **幅**: webview エリアの場合は280ピクセル。 Webview の左側と右側には、20ピクセルのパディングがあります。
* **高さ**: タブの下端までの裁ち落とし。Webview エリアと tab ヘッダーの間には、20ピクセルのパディングがあります。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="会議の拡張機能の UI を [会議] タブに示す図" border="false":::

1. **アプリアイコン**: [会議中] タブへのエントリポイントです。
1. **ヘッダー**: タブ名を含みます。
1. **Name**: tab インスタンスの名前。
1. [**閉じる**]: タブを閉じます。フッター内のアクションではなく、右上にある閉じるアイコンを常に使用します。
1. **Webview**: サードパーティアプリのすべてのコンテンツを表示します。

## <a name="behavior"></a>動作

### <a name="scale"></a>倍率

現在、[会議中] タブの幅は固定されています。

### <a name="scrolling"></a>量

[会議中] タブでスクロールすることについては、次の項目を参照してください。

* 垂直方向にスクロールできるようにする必要があります。
* スクロールした内容のみが表示されます (何も上または下にありません)。
* Scrollbar は、webview コンテンツの一部です。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="[会議中] タブでの webview コンテンツのスクロール方法を示す図。" border="false":::

### <a name="navigation"></a>ナビゲーション

ナビゲーション層またはヘビーコンテンツがあるシナリオでは、ユーザーがセカンダリレイヤーに移動できるようにすることをお勧めします。 ユーザーは前のレイヤーに戻ることができる必要があります。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="[会議中] タブでのセカンダリレイヤーへの移動方法を示す図" border="false":::

## <a name="components"></a>コンポーネント

会議中のタブは、主に、 <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent デザインシステム</a>を基にした次の<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI コンポーネント (figma)</a>で構築されています。

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

### <a name="responsiveness"></a>性

会議中のタブレイアウトは、さまざまなサイズに拡張できる必要があります。 会議の後、実行中、および後に、タブの拡大/縮小と実行の方法を検討します。

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="会議の前と後に、会議内のタブのコンテンツが全画面のタブのように表示されることを示す図。" border="false":::

#### <a name="before-the-meeting"></a>会議の前

タブレイアウトが異なる言語の右または左のレイアウトに適応し、コントロールが正しい位置に移動することを確認してください。 (会議前レイアウトは、会議後のレイアウトにも適用されます)。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="会議中に [会議前] タブの内容が [会議中] タブにどのように縮小されるかを示す図。" border="false":::

#### <a name="during-the-meeting"></a>会議中

タブのコンテンツは、[会議中] タブのレイアウトと場所に調整されます。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="Teams 会議で使用される暗いテーマの [会議中] タブの設計方法を示す図。" border="false":::

#### <a name="do-design-for-a-dark-theme"></a>Do: 暗いテーマのデザイン

Teams 会議は、ビジュアルおよび認知ノイズを軽減するために最適化されており、ユーザーがディスカッションと共有コンテンツに集中できるようにするために役立ちます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="この図は、Teams の暗いテーマに向いていない色を使用しないことを示しています。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>いいえ: 見慣れない色を使用する

会議環境と競合している色は、煩雑で、Teams に対してネイティブに表示されないことがあります。

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>量

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="[会議中] タブで垂直方向にスクロールできることを示す図" border="false":::

#### <a name="do-scroll-vertically"></a>Do: 上下にスクロール

ユーザーは、Teams (およびその他の場所) で縦方向にスクロールすることが予想されます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="[会議中] タブで水平スクロールを許可しないことを示す図" border="false":::

#### <a name="dont-scroll-horizontally"></a>いいえ: 横方向にスクロール

水平方向のスクロールは、Teams では予期された動作ではありません。 会議環境でのその他のキャンバスは、垂直方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>レイアウト

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="[会議中] タブで推奨される単一列のレイアウトを示す図" border="false":::

#### <a name="do-single-columns"></a>Do: 単一列

[会議中] タブの絞り込みの性質を考えると、コンテンツを1列で表示することを強くお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="[会議中] タブの2列のレイアウトが最適でないことを示す図" border="false":::

#### <a name="dont-multiple-columns"></a>いいえ: 複数列

[会議中] タブの容量に制限があるため、複数の列を持つレイアウトは推奨されません。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="会議中のタブアプリに複数のナビゲーション層がある場合は、常に [戻る] ボタンを表示する図を示します。" border="false":::

#### <a name="do-have-a-back-button"></a>Do: [戻る] ボタンを用意する

複数のナビゲーション層がある場合は、ユーザーが前のビューに戻ることができる必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="ナビゲーション用に [会議中] タブにもう1つの [閉じる] ボタンを追加することによって、問題が発生する可能性があることを示す図。" border="false":::

#### <a name="dont-include-another-close-button"></a>[しない]: 別の [閉じる] ボタンを含める

[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既に [閉じる] ボタンがあるために問題が発生し、会議中のタブ自体が閉じられることがあります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="制限されたスペースがある場合に、[会議中] タブで modals (つまり、タスクモジュール) を使用するときに注意が必要なことを示す図" border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a>注意: 狭いスペースでのダイアログの使用

すでに絞り込みが行われているタブの [タスクモジュール] などのダイアログは、コンテンツの折り返しや不明瞭になることがあります。

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>アクセシビリティ

アクセシビリティの詳細については、「 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>」を参照してください。

## <a name="resources"></a>リソース

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams の会議拡張機能 Figma ファイル</a>
* [タブデザインガイドライン](../tabs/design/tabs.md)
* [タブモバイルのデザインガイドライン](../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。

> [!div class="nextstepaction"]
> [設計検証ガイドラインの確認](../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
