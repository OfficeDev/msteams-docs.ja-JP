---
title: タスクモジュールを設計する
author: heath-hamilton
description: Teams アプリのタスクモジュールを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606415"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのタスクモジュールを設計する

タスクモジュールを使用して、Teams アプリでモーダルポップアップエクスペリエンスを作成できます。 この機能を使用すると、リッチメディアと情報を表示したり、複雑なタスクを実行したりできます。

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="例は、タスクモジュールを示しています。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、包括的なタスクモジュールデザインガイドラインを見つけることができます。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>タスクモジュールを開く

タスクモジュールは、アプリのほとんどすべての場所から起動できます。

* **Tab**: タスクモジュールは、タブまたは iframe 内の任意のリンクから起動できます。 ユーザーが相互作用に集中するシナリオで使用します。
* **Bot**: タスクモジュールは、ボットメッセージ内のリンクから起動できます。
* **アダプティブカード**: タスクモジュールは、ユーザーがボタンを選択したときに、アダプティブカード (メッセージング内線または bot が送信) から起動できます。
* **メッセージング拡張機能 (アクションコマンド)**: メッセージング拡張機能を使用すると、メッセージのコンテンツに対して特定のアクションを実行できます。 アクションを選択すると、タスクモジュールが開きます。
* **メッセージング拡張機能 (新規作成ボックスコンテキスト)**: [新規作成] ボックスでは、標準のポップアップではなく、タスクモジュールを開くためのメッセージング拡張機能をデザインできます。 フォームの入力など、複雑な対話のためのタスクモジュールを予約します。

## <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="タスクモジュールの UI 構造を示す図" border="false":::

タスクモジュールは非常に柔軟なサーフェスです。 これらは、他の UI テンプレートを使用して、パートナーが作成したエクスペリエンスをホストするために、iframe を使用して構築できます。 これは、洗練された快適な作業に適しています。

また、 [アダプティブカード](../../task-modules-and-cards/cards/design-effective-cards.md) フレームワークを使用してビルドすることもできます。これは、一般的なシナリオ (フォームなど) をより簡単に実行する方法です。

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン**|
|2 |**アプリ名**: アプリの完全な名前。|
|3 |**ヘッダー**: ヘッダーをクリアで簡潔にします。 ユーザーが完了する必要のあるタスクについて説明します。
|4 |**[閉じる] ボタン**: 挿入するアプリコンテンツをユーザーが検索できるようにします。|
|5 |**iframe**: アプリコンテンツをホストする、応答性の高いスペース。|
|6 |**アクション (オプション)**: アプリコンテンツに関連するボタン。|

## <a name="designing-with-ui-templates"></a>UI テンプレートを使用して設計する

タスクモジュール内の一般的なレイアウトにテンプレートを使用することを検討してください。 それぞれが、自分のシナリオに合わせて、またはカスタマイズしたブランド化された優れたデザインを作成するために、小さなコンポーネントで構成されています。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。
* [Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。

## <a name="examples"></a>例

### <a name="list"></a>リスト

タスクモジュールでは、簡単にスキャンできるので、適切に作業できます。

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="タスクモジュール内のリストの例です。" border="false":::

### <a name="form"></a>フォーム

タスクモジュールは、連続したユーザー入力とインライン検証を含むフォームを表示するのに便利な場所です。 フォーム要素を埋め込む方法として、アダプティブカードを活用することができます。

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="タスクモジュールのフォームの例" border="false":::

### <a name="sign-in"></a>サインイン

一連のタスクモジュールを使用してフォーカスのあるサインインまたはサインアップフローを作成し、ユーザーが連続した手順を簡単に移動できるようにします。

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="タスクモジュールでのサインイン操作の例。" border="false":::

### <a name="media"></a>メディア

タスクモジュールにメディアコンテンツを埋め込んで、フォーカスのある表示環境を実現します。

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="タスクモジュール内のメディアコンテンツの例。" border="false":::

### <a name="empty-state"></a>空の状態

ウェルカムメッセージ、エラーメッセージ、および成功メッセージに使用します。

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="タスクモジュール内の空の状態の例です。" border="false":::

### <a name="image-gallery"></a>イメージ ギャラリー

Iframe 内にギャラリーカルーセルを埋め込みます。

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="タスクモジュール内のイメージギャラリーの例です。" border="false":::

### <a name="poll"></a>間隔

この例では、アダプティブカードから起動された投票結果を示します。

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="タスクモジュール内の投票の例" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

### <a name="usability"></a>使いやすさ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>Do: 一度に1つのタスクモジュールを使用する

目標は、すべてのタスクを完了した後にユーザーにフォーカスを移動することです。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>[いいえ: タスクモジュールの上にダイアログを表示する]

これにより、unfocused で混乱したユーザー環境が作成されます。

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>速い

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>実行: コンテンツが応答していることを確認する

タスクモジュールでホストされているアダプティブカードはモバイルデバイスで適切に表示されますが、iframe を使用してアプリコンテンツをホストする場合は、UI が応答可能であることと、デバイス間で適切に動作することを確認してください。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a>いいえ: 水平スクロールバーを使用します。

コンテンツを重視しすぎないようにすることをお勧めします。 スクロールが必要な場合は、水平方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>合理

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-keep-it-short"></a>実行: 短時間で保持する

マルチステップウィザードは簡単に作成できますが、これは必ずしも必要であるとは限りません。 複数画面タスクモジュールは、受信メッセージが煩雑で、tempt ユーザーが終了するため、問題を発生させる可能性があります。 タスクが実際に関係している場合は、タスクモジュールではなく、完全な web ページにポップアウトします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-do-long-interactions"></a>いいえ: 長時間の操作を実行する

相互作用を短くして、ポイントにするようにしてください。

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>エラー メッセージ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-use-inline-error-messages"></a>Do: インラインエラーメッセージを使用する

インラインエラー処理のガイドラインについては、「forms UI template」を参照してください。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>[いいえ: ダイアログにエラーメッセージを表示する。

タスクモジュールの上部にあるダイアログにエラーメッセージを表示しないようにします。 これにより、わかりやすいユーザー環境が作成されます。

   :::column-end:::
:::row-end:::
