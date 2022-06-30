---
title: タスク モジュールをデザインする
author: heath-hamilton
description: このモジュールでは、Teams アプリのタスク モジュールをデザインして、Microsoft Teams UI Kit を取得するする方法を説明します。
ms.localizationpriority: high
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 95d0d43e72a72220111c0afa81970a4fab986fc8
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558115"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Microsoft Teams のアプリのタスク モジュールの設計

Teams アプリでタスク モジュールを使用して、モーダル ポップアップ エクスペリエンスを作成することができます。 この機能を使用して豊富なメディアと情報を表示し、複雑なタスクを完了します。

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="タスク モジュールを示す例。":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit には、必要に応じて変更できる要素を含む、より包括的なタスク モジュール デザインのガイドラインが掲載されています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>タスク モジュールを開く

タスク モジュールは、アプリのほぼすべての場所で起動できます。

* **タブ**: タスク モジュールは、タブ内のあらゆるリンクから起動できます。ユーザーを対話に集中させたいシナリオで使用します。
* **ボット**: タスク モジュールは、ボット メッセージ内のリンクから起動できます。
* **アダプティブ カード**: タスク モジュールは、ユーザーがボタンを選択した場合にアダプティブ カード (メッセージ拡張機能またはボットによる送信) から起動できます。
* **メッセージ拡張機能 (アクション コマンド)**: メッセージ拡張機能を使用すると、メッセージ コンテンツで特定のアクションを実行できます。アクションを選択すると、タスク モジュールが開きます。
* **メッセージ拡張機能 (作成ボックスコンテキスト)**: 作成ボックスで、メッセージ拡張機能を設計して、一般的なポップアップの代わりにタスク モジュールを開くことができます。フォームの入力など、複雑な操作のためにタスク モジュールを予約します。

## <a name="anatomy"></a>構造

タスク モジュールでは、ホストされたアプリ エクスペリエンスに柔軟なサーフェスを提供します。これらは IFRAME​​ (デスクトップ) または Web ビュー (モバイル) を使用して構築されています。そのため、UI テンプレート (推奨) を使用するか、またはゼロからタスク モジュールを設計できます。

また、[アダプティブ カード](../../task-modules-and-cards/cards/design-effective-cards.md) フレームワークを使用して構築することもできます。これは、一般的なシナリオ (フォームなど) を促進する、より簡単で迅速な方法です。

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-task-module-anatomy.png" alt-text="モバイルでのタスク モジュールの UI 構造を示す図。":::

|カウンター|説明|
|----------|-----------|
|1|**ヘッダー**: ヘッダーを明確かつ簡潔にします。 ユーザーに完了させたいタスクについて説明します。
|2|**アプリ名**: アプリのフル ネーム|
|3|**閉じるボタン**: タスク モジュールを閉じます。 アプリ コンテンツに保存されていない変更は適用されません。|
|4|**Web ビュー**: アプリ コンテンツをホストする応答性の高いスペース。|
|5|**アクション (省略可能)**: アプリ コンテンツに関連するボタン。|

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="タスク モジュールの UI 構造を示す図。":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ アイコン**|
|2|**アプリ名**: アプリのフル ネーム|
|3|**ヘッダー**: ヘッダーを明確かつ簡潔にします。 ユーザーに完了させたいタスクについて説明します。
|4|**閉じるボタン**: タスク モジュールを閉じます。 アプリ コンテンツに保存されていない変更は適用されません。|
|5|**IFRAME​​**: アプリ コンテンツをホストする応答性の高いスペース。|
|6 |**アクション (省略可能)**: アプリ コンテンツに関連するボタン。|

## <a name="designing-with-ui-templates"></a>UI テンプレートを使用して設計する

タスク モジュール内の一般的なレイアウトにテンプレートを使用することを検討してください。各コンポーネントは、より小規模なコンポーネントで構成され、使い慣れた、またはシナリオやブランドの外観に合わせてカスタマイズできる、優雅で応答性の高いデザインを作成します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、最初の実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。

## <a name="examples"></a>例

### <a name="list"></a>リスト

スキャンが簡単なので、リストはタスク モジュールでうまく機能します。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-list.png" alt-text="モバイルでのタスク モジュールのリストの例。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="タスク モジュールのリストの例。":::

### <a name="form"></a>フォーム

タスク モジュールは、シーケンシャル ユーザー入力とインライン検証を備え、フォームを表面化するのに最適な場所です。 フォーム要素を埋め込む方法としてアダプティブ カードを活用できます。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-form.png" alt-text="モバイルでのタスク モジュールのフォームの例。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/form.png" alt-text="タスク モジュールのフォームの例。":::

### <a name="sign-in"></a>サインイン

一連のタスク モジュールを使用して、フォーカスしたサインイン フローやサインアップ フローを作成し、ユーザーがシーケンシャルな段階を簡単に移動できるようにします。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-sign-in.png" alt-text="モバイルのタスク モジュールでのサインイン エクスペリエンスの例。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="タスク モジュールでのサインイン エクスペリエンスの例。":::

### <a name="media"></a>メディア

フォーカスされた表示エクスペリエンスのために、タスク モジュールにメディア コンテンツを埋め込みます。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-media.png" alt-text="モバイルのタスク モジュールでのメディア コンテンツの例。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="タスク モジュールのメディア コンテンツの例。":::

### <a name="empty-state"></a>空の状態

ウェルカム メッセージ、エラー メッセージ、成功メッセージに使用します。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-empty-state.png" alt-text="モバイルでのタスク モジュールの空の状態の例。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="タスク モジュールの空の状態の例。":::

### <a name="image-gallery"></a>画像ギャラリー

ギャラリー カルーセルを IFRAME (デスクトップ) や Web ビュー (モバイル) に埋め込みます。

##### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-image-gallery.png" alt-text="モバイルのタスク モジュールの画像ギャラリーの例。":::

##### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="タスク モジュールの画像ギャラリーの例。":::

### <a name="poll"></a>投票

この例では、アダプティブ カードで起動した投票結果を示しています。 投票は、タスク モジュール内に配置できます。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/task-module/mobile-poll.png" alt-text="モバイルのタスク モジュールでの投票の例。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="タスク モジュールでの投票の例。":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="usability"></a>ユーザビリティ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (一度に 1 つのタスク モジュール)。":::

#### <a name="do-use-one-task-module-at-a-time"></a>やるべきこと: 一度に 1 つのタスク モジュールを使用する

この目標は、ユーザーが最終的にタスクを完了する作業に集中させることです。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (タスク モジュールの上にダイアログを表示する)。":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>してはいけないこと: タスク モジュールの上にダイアログを表示する

これによりフォーカスされなくなり、わかりづらいユーザー エクスペリエンスが作成されます。

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>応答性が高い

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (コンテンツの応答性が高いことを確認する)。":::

#### <a name="do-make-sure-the-content-is-responsive"></a>やるべきこと: コンテンツの応答性を確認する

タスク モジュールでホストされているアダプティブ カードはモバイル デバイスで適切にレンダリングされますが、IFRAME を使用してアプリ コンテンツをホストする場合は、UI の応答性が高く、デバイス間で適切に動作していることを確認してください。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (水平方向のスクロール バーを使用しない)。":::

#### <a name="dont-use-horizontal-scroll-bars"></a>してはいけないこと: 水平方向のスクロール バーを使用する

これは、コンテンツにフォーカスし、時間がかかりすぎないように維持するベスト プラクティスです。 スクロールが必要な場合は、水平方向ではなく垂直方向にスクロールします。

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>簡易性

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (簡潔にまとめる)。":::

#### <a name="do-keep-it-short"></a>やるべきこと: 簡潔にまとめる

複数ステップ ウィザードは簡単に作成できますが、それが必ずしも必要とはいえません。 複数画面のタスク モジュールは、受信メッセージでユーザーが集中力を切らし、終了しようとしてしまうため問題があります。 実際に関係のあるタスクの場合は、タスク モジュールの代わりに完全な Web ページにポップアウトします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (長い対話がない)。":::

#### <a name="dont-have-long-interactions"></a>してはいけないこと: 長い対話を行う

対話を短くしてワンポイントになるようにします。

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>エラー メッセージ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (インライン エラー メッセージを使用する)。":::

#### <a name="do-use-inline-error-messages"></a>するべきこと: インライン エラー メッセージを使用する

インライン エラー処理のガイドラインについては、UI テンプレートのフォームを参照してください。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (ダイアログにエラー メッセージを表示する)。":::

#### <a name="dont-put-error-messages-in-dialogs"></a>してはいけないこと: ダイアログにエラー メッセージを表示する

タスク モジュールの上のダイアログにエラー メッセージを表示しないでください。わかりづらいユーザー エクスペリエンスが作成されます。

   :::column-end:::
:::row-end:::
