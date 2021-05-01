---
title: タスク モジュールをデザインする
author: heath-hamilton
description: アプリのタスク モジュールを設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 347ce42c41706f698e2f8897a0518aae0850a275
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101731"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>アプリ用のタスク モジュールMicrosoft Teamsする

タスク モジュールを使用して、Teamsポップアップ エクスペリエンスを作成できます。 リッチ メディアと情報を表示したり、複雑なタスクを完了したりするには、この機能を使用します。

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="タスク モジュールの例を示します。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、より包括的なタスク モジュール設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>タスク モジュールを開く

タスク モジュールは、アプリのほぼすべての場所から起動できます。

* **Tab**: タブ内の任意のリンクからタスク モジュールを起動できます。ユーザーが対話に集中するシナリオで使用します。
* **ボット**: ボット メッセージ内のリンクからタスク モジュールを起動できます。
* **アダプティブ カード**: ユーザーがボタンを選択すると、アダプティブ カード (メッセージング拡張機能またはボットによって送信される) からタスク モジュールを起動できます。
* **メッセージング拡張機能 (アクション コマンド)**: メッセージング拡張機能を使用すると、メッセージ コンテンツに対して特定のアクションを実行できます。 アクションを選択すると、タスク モジュールが開きます。
* **メッセージング拡張機能 (作成ボックス** コンテキスト) : 作成ボックスで、メッセージング拡張機能を設計して、一般的なフライアウトではなくタスク モジュールを開くことができます。 フォームの入力など、複雑な操作のためにタスク モジュールを予約します。

## <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="タスク モジュールの UI 構造を示す図。" border="false":::

タスク モジュールは非常に柔軟なサーフェスです。 iframes を使用して構築し、他の UI テンプレートを引き込み、パートナーが構築したエクスペリエンスをホストできます。 これは、最も洗練されたエクスペリエンスに優先されます。

また、アダプティブ カード フレームワーク[](../../task-modules-and-cards/cards/design-effective-cards.md)を使用して構築することもできます。これは、一般的なシナリオ (フォームなど) をより簡単かつ迅速に実行できます。

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン**|
|2|**アプリ名**: アプリの完全な名前。|
|3|**ヘッダー**: ヘッダーを明確かつ簡潔にします。 ユーザーが完了するタスクについて説明します。
|4|**[閉じる**] ボタン: ユーザーが挿入するアプリ コンテンツを検索できます。|
|5|**iframe**: アプリ コンテンツをホストするレスポンシブ スペース。|
|6|**アクション (省略可能)**: アプリコンテンツに関連するボタン。|

## <a name="designing-with-ui-templates"></a>UI テンプレートを使用した設計

タスク モジュール内の一般的なレイアウトにテンプレートを使用する方法を検討してください。 各コンポーネントは、小規模なコンポーネントで構成され、使い慣れた、またはシナリオやブランドの外観に合わせてカスタマイズできる、エレガントで応答性の高いデザインを作成します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。

## <a name="examples"></a>例

### <a name="list"></a>一覧表示

リストはスキャンが簡単なので、タスク モジュールでうまく機能します。

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="タスク モジュールのリストの例。" border="false":::

### <a name="form"></a>フォーム

タスク モジュールは、シーケンシャル ユーザー入力とインライン検証を備え、フォームを表面化する最適な場所です。 フォーム要素を埋め込む方法としてアダプティブ カードを活用できます。

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="タスク モジュール内のフォームの例。" border="false":::

### <a name="sign-in"></a>サインインする

一連のタスク モジュールを使用して、フォーカスのあるサインインフローまたはサインアップ フローを作成し、ユーザーが順次ステップを簡単に移動できます。

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="タスク モジュールでのサインイン エクスペリエンスの例。" border="false":::

### <a name="media"></a>メディア

フォーカスされた表示エクスペリエンスのために、タスク モジュールにメディア コンテンツを埋め込む。

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="タスク モジュールのメディア コンテンツの例。" border="false":::

### <a name="empty-state"></a>空の状態

ウェルカム メッセージ、エラー メッセージ、成功メッセージに使用します。

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="タスク モジュールの空の状態の例。" border="false":::

### <a name="image-gallery"></a>イメージ ギャラリー

ギャラリーカルーセルを iframe に埋め込む。

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="タスク モジュールのイメージ ギャラリーの例。" border="false":::

### <a name="poll"></a>Poll

次の使用例は、アダプティブ カードから起動されたポーリング結果を示しています。 ポーリングは、タスク モジュール内に配置できます。

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="タスク モジュールのポーリングの例。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="usability"></a>使いやすさ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="タスク モジュールのベスト プラクティス (一度に 1 つのタスク モジュール) を表示する例。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>Do: 一度に 1 つのタスク モジュールを使用する

目標は、ユーザーが結局タスクを完了する作業に集中する方法です。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="タスク モジュールのベスト プラクティスを表示する例 (タスク モジュールの上にダイアログを表示する)。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>[しない] タスク モジュールの上にダイアログを表示する

これにより、焦点が合わされ、わかりにくいユーザー エクスペリエンスが作成されます。

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>速い

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (コンテンツが応答可能な状態を確認してください)。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>Do: コンテンツの応答性を確認する

タスク モジュールでホストされているアダプティブ カードはモバイル デバイスで適切にレンダリングされます。iframe を使用してアプリ コンテンツをホストする場合は、UI が応答性に優れた、デバイス間で適切に動作する必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (水平方向のスクロール バーを使用しない)。" border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a>[しない]: 水平方向のスクロール バーを使用する

コンテンツに焦点を当て、長すぎずに維持するベスト プラクティスです。 スクロールが必要な場合は、水平方向ではなく垂直方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>シンプルさ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (短くする)。" border="false":::

#### <a name="do-keep-it-short"></a>Do: 短くする

マルチステップ ウィザードは簡単に作成できますが、必ずしも必要とは限りません。 複数画面のタスク モジュールは、受信メッセージが気を散らし、ユーザーが終了を思い出すので、問題になる可能性があります。 タスクが実際に関係している場合は、タスク モジュールの代わりに完全な Web ページにポップアウトします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (長い対話を行う必要があります)。" border="false":::

#### <a name="dont-have-long-interactions"></a>Don't: 長い対話を行う

やり取りを短くしてポイントにしてください。

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>エラー メッセージ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (インライン エラー メッセージを使用)。" border="false":::

#### <a name="do-use-inline-error-messages"></a>Do: インライン エラー メッセージを使用する

インライン エラー処理のガイドラインについては、フォーム UI テンプレートを参照してください。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (ダイアログにエラー メッセージを表示する)。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>[しない] ダイアログにエラー メッセージを表示する

タスク モジュールの上のダイアログにエラー メッセージを表示しません。 わかりにくいユーザー エクスペリエンスを作成します。

   :::column-end:::
:::row-end:::
