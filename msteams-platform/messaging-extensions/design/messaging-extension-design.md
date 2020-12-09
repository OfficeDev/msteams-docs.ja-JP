---
title: メッセージング拡張機能の設計
description: Teams メッセージング拡張機能を設計し、Microsoft Teams UI キットを取得する方法について説明します。
keywords: teams 設計ガイドラインリファレンスメッセージング拡張のヒントベストプラクティス
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604854"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Microsoft Teams メッセージング拡張機能の設計

メッセージング拡張機能は、会話から離れずに、アプリコンテンツを挿入したり、メッセージに対して動作したりするためのショートカットです。

アプリの設計をガイドするには、次の情報を参照してください。 Teams でのメッセージング拡張機能の追加、使用、および管理の方法を示します。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、包括的なメッセージング拡張設計ガイドラインを見つけることができます。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>メッセージング拡張機能を追加する

メッセージング拡張機能は、次の Teams コンテキストで追加できます。

* Teams ストア (AppSource) から。
* [新規作成] ボックスの近くにあるチャネル、チャット、または会議 (前、中、および後)。 これらのいずれかの場所にメッセージング拡張機能を追加した場合は、そのコンテキストで使用できるだけのことに注意してください。

次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの [新規作成] ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

## <a name="set-up-a-messaging-extension"></a>メッセージング拡張機能を設定する

認証は必須ではありませんが、アプリがチケット追跡ツールのようなものである場合、メッセージング拡張機能を使用するには、ユーザーにサインインする必要があります。

Teams アプリ間での一貫性を保つため、サインイン画面をカスタマイズすることはできません。 シングルサインオン (SSO) 認証を使用する場合、ユーザーは自動的にサインインします。

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="例は、[サインイン] ボタンがある [メッセージング拡張機能のセットアップ] 画面を示しています。" border="false":::

## <a name="types-of-messaging-extensions"></a>メッセージング拡張機能の種類

メッセージング拡張機能には、検索コマンド、アクションコマンド、またはその両方を使用できます。 自分のコマンドは、アプリの機能によって異なり、Teams 内でそれらがどのように使用されるかによっても異なります。

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、ユーザーはメッセージング拡張機能を使用して外部コンテンツをすばやく検索し、メッセージに挿入することができます。 検索コマンドは、通常、[新規作成] ボックスで使用できます。 たとえば、Teams を離れることなく、コンテンツを共有することでディスカッションを開始または追加できます。

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例は、[新規作成] ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

#### <a name="compose-box-layout-options"></a>新規作成ボックスのレイアウトオプション

[リストビューやグリッドビュー](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)など、メッセージング拡張機能の検索結果を表示するためのいくつかのオプションがあります。

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能検索結果のレイアウトオプションを示す図" border="false":::

### <a name="action-commands"></a>操作コマンド

アクションコマンドを使用すると、ユーザーは Teams 内の外部サービスでのアクションをトリガーしたり、要求を処理したりできます。 たとえば、アプリで注文を追跡している場合、ユーザーは、自分のチャットの外部から同僚のメッセージの内容を使用して、新しい注文を作成することができます。

アクションベースのメッセージング拡張機能では、多くの場合、ユーザーがモーダル内でフォームまたはその他の種類の構成を完了する必要があります。 これらのエクスペリエンスは、 [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用して作成できます。

## <a name="open-a-messaging-extension"></a>メッセージング拡張機能を開く

新規作成ボックスとメッセージ/投稿は、ユーザーがメッセージング拡張機能を使用するプライマリコンテキストです。

### <a name="from-the-compose-box"></a>[新規作成] ボックス

追加されたユーザーは、[新規作成] ボックスの下にあるアプリのアイコンを選択することによって、メッセージング拡張機能を開くことができます。 この例では、拡張機能に検索コマンドとアクションコマンドがあります。

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、[新規作成] ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>チャットメッセージまたはチャネル投稿から

追加されたユーザーは、 **More** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: チャットメッセージまたはチャネルの投稿にある [その他] アイコンを選択して、拡張機能のアクションコマンドを見つけることができます。 使用状況に応じて、拡張機能が [ **その他のアクション** ] の下に一覧表示されることがあります。

#### <a name="chat-message"></a>チャット メッセージ

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャットメッセージからメッセージング拡張機能を開く方法を示しています。" border="false":::

#### <a name="channel-post"></a>チャネル投稿

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="例は、チャネル投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

## <a name="use-a-messaging-extension"></a>メッセージング拡張機能を使用する

次のシナリオは、ユーザーがメッセージング拡張機能を使用する主な方法を示しています。

### <a name="insert-content-into-a-message"></a>メッセージにコンテンツを挿入する

**1. メッセージング拡張機能を選択** します。 ユーザーは、[新規作成] ボックスから共有するコンテンツを検索できます。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="例は、[新規作成] ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

**2. コンテンツを挿入** します。 投稿した後、他のユーザーがコンテンツを返信または選択して、アプリに詳細情報を表示することができます。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="例は、チャネル会話にコンテンツを送信するユーザーを示しています。" border="false":::

### <a name="take-action-on-a-message"></a>メッセージに対してアクションを実行する

**1. メッセージング拡張機能を選択** します。 アプリには、1つ以上のアクションコマンドを含めることができます。

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="この例は、メッセージング拡張機能のアクションコマンドを選択するユーザーを示しています。" border="false":::

**2. アクションを完了** します。 アプリは、メッセージアクションによって送信されたコンテンツまたはデータを受信し、処理することができます。 これにより、ユーザーが自分のアプリに情報を直接入力しても、次の例のような会話に残すことができます。

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="例は、[新規作成] ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

### <a name="preview-links"></a>プレビューのリンク

また、メッセージング拡張機能では、認識された URL からのリッチリンクをメッセージに挿入することもできます (この機能は [link unfurling](../../messaging-extensions/how-to/link-unfurling.md)と呼ばれます)。

**1. 認識** されたリンクを [新規作成] ボックスに貼り付けます。

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="例は、compost ボックスにリンクを貼り付けたユーザーを示しています。" border="false":::

**2. コンテンツを挿入** します。 アプリで [新規作成] ボックスの URL を認識している場合は、web コンテンツのコンテンツを豊富にプレビューするカードとしてリンクが表示されます。 (詳細については、「 [アダプティブカードのデザインガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md) 」を参照してください)。

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="例では、アプリによって認識された後の URL が、[新規作成] ボックスにいくつかのリッチコンテンツを含むことを示しています。" border="false":::

## <a name="manage-a-messaging-extension"></a>メッセージング拡張機能を管理する

アイコンを右クリックすると、ユーザーはメッセージング拡張機能を固定、削除、または構成することができます。

## <a name="anatomy"></a>構造

### <a name="messaging-extension-in-the-compose-box"></a>[新規作成] ボックスのメッセージング拡張機能

次の例は、[新規作成] ボックスから開かれたメッセージング拡張機能です。

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="[新規作成] ボックスでのメッセージング拡張機能の UI の構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|アプリ **ロゴ**: アプリロゴのカラーアイコン。|
|2 |**アプリ名**: アプリの完全な名前。|
|3 |**アクションコマンドメニューアイコン (オプション)**: メッセージング拡張機能のアクションコマンドの一覧を開きます (指定した場合)。
|4 |**検索ボックス**: ユーザーが挿入するアプリコンテンツを検索できます。|
|5 |**タブメニュー (オプション)**: 複数のコンテンツカテゴリを提供します。|
|6 |**アクションコマンドメニュー (オプション)**: アクションコマンドの一覧を表示します (任意の数を指定する場合)。|
|7 |**アプリコンテンツ**: 主に検索結果を表示します。 この例では、リストレイアウトを使用しています (グリッドレイアウトは別のオプションです)。|
|8 |アプリ **ロゴ**: アプリロゴのアウトラインアイコン。|

### <a name="messaging-extension-management-menu"></a>メッセージング拡張機能の管理メニュー

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能管理メニューの UI の構造を示す図" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**固定** 解除: ユーザーがアプリを固定している場合に使用できます。|
|2 |**Remove**: チャネル、チャット、または会議からメッセージング拡張機能を削除します。|

## <a name="best-practices"></a>ベスト プラクティス

### <a name="setup-and-general-usage"></a>セットアップと一般的な使用法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Do: シングルサインオンと統合する

SSO を使用すると、サインインプロセスが簡単に、より速く、かつ安全になります。 また、ユーザーが個人用アプリに既にサインインしている場合は、再度サインインしてメッセージング拡張機能にアクセスする必要もありません。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>いいえ: ユーザーを会話から離します。

メッセージング内線番号は、コンテキスト切り替えが減少すると想定されるショートカットです。 たとえば、ユーザーが Teams 以外の web ページにアクセスするということはできません。

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Do: メッセージング拡張機能を強調表示する

メッセージング拡張機能は、必ずしも簡単に見つけることができません。 アプリの詳細ページでの使用方法を示したスクリーンショットを含めます。 アプリに bot も含まれている場合は、ボットウェルカムツアーにメッセージング拡張機能のヘルプドキュメントを含めることができます。

### <a name="templating"></a>テンプレート

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Do: 可能であれば、チームがいくつかのデザイン作業を処理できるようにします

ユースケースにとって意味がある場合は、検索ベースのメッセージング拡張機能を作成することを検討してください。 Teams では、これらの種類の拡張子が組み込みのテーマとアクセシビリティを使用してレンダリングされます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>[しない]: タスクモジュールにアプリ全体を埋め込む

メッセージング拡張機能にアクションコマンドが必要な場合は、タスクモジュールをシンプルにし、アクションを実行するために必要なコンポーネントのみを表示します。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do: Teams のカラートークンを活用する

各 Teams テーマには独自の配色があります。 テーマの変更を自動的に処理するには、設計で <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color token (FLUENT UI)</a> を使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-hard-code-color-values"></a>いいえ: ハードコードの色の値

Teams のカラートークンを使用しない場合、設計のスケーラビリティが低下し、管理にかかる時間が長くなります。

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Do: コンテキストに適したアクションコマンドを含める

メッセージアクションは、ユーザーが閲覧しているものと関連付けられます。 たとえば、ユーザーに対して、他のユーザーの投稿のテキストを使用して、懸案事項または作業項目を作成するためのショートカットを提供します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="メッセージング拡張機能のベストプラクティスを示す例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>省略: コンテキスト以外のアクションコマンドを含める

ダッシュボードを表示するメッセージアクションは、ほとんどの会話から切断され **ている** ように見えます。

   :::column-end:::
:::row-end:::

### <a name="searches"></a>現われる

#### <a name="do-show-search-results-while-typing"></a>Do: 入力中に検索結果を表示する

ユーザーの入力中に推奨される検索結果を提供します。 必要なコンテンツを最小限の文字で迅速に見つけることができます。

#### <a name="dont-require-users-to-submit-a-query"></a>いいえ: クエリの送信をユーザーに要求する

アプリに対してクエリを送信するためのキーを押すか、ボタンを選択することができます。 App services サービスの方が簡単な場合もありますが、ユーザーが入力したリアルタイム検索結果が表示されないと混乱する可能性があります。

#### <a name="do-consider-zero-term-queries"></a>Do: 0 個のクエリを考慮する

たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示されたものを表示します。 そのようなコンテンツを会話に挿入することができます。

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。

> [!div class="nextstepaction"]
> [設計検証ガイドラインの確認](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
