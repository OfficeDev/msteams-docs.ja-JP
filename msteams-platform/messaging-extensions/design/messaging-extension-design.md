---
title: メッセージング拡張機能の設計
description: Teams メッセージング拡張機能を設計し、Microsoft Teams UI キットを取得する方法について説明します。
keywords: teams の設計ガイドラインは、メッセージング拡張機能のヒントのベスト プラクティスを参照します。
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: e3e4197e461f6d13f0c45ba2ce8bfb93b01b5e0f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020724"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Microsoft Teams メッセージング拡張機能の設計

メッセージング拡張機能は、アプリコンテンツを挿入したり、会話から離れることなくメッセージに作用するためのショートカットです。
アプリの設計をガイドするために、次の情報は、Teams でユーザーがメッセージング拡張機能を追加、使用、および管理する方法を示しています。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit には、必要に応じて取得および変更できる要素を含む、包括的なメッセージング拡張機能の設計ガイドラインがあります。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>メッセージング拡張機能の追加

メッセージング拡張機能は、次の Teams コンテキストに追加できます。

* Teams ストア (AppSource) から。
* 作成ボックスの近くのチャネル、チャット、または会議 (前、中、および後)。 これらの場所の 1 つでメッセージング拡張機能を追加する場合は、そのコンテキストでのみ使用できます。

次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

## <a name="set-up-a-messaging-extension"></a>メッセージング拡張機能を設定する

認証は必須ではありませんが、アプリがチケット追跡ツールのようなものである場合は、メッセージング拡張機能を使用するためにサインインするユーザーが必要な場合があります。

Teams アプリ全体で一貫性を保つには、サインイン画面をカスタマイズできない。 シングル サインオン (SSO) 認証を使用する場合、ユーザーは自動的にサインインします。

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="例では、サインイン ボタンを使用してメッセージング拡張機能のセットアップ画面を表示します。" border="false":::

## <a name="types-of-messaging-extensions"></a>メッセージング拡張機能の種類

メッセージング拡張機能には、検索コマンド、アクション コマンド、または両方を指定できます。 コマンドは、アプリの機能と Teams の使用例に適合する方法によって異なっています。

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、ユーザーはメッセージング拡張機能を使用して外部コンテンツをすばやく検索し、メッセージに挿入できます。 検索コマンドは、通常、作成ボックスで使用できます。 たとえば、Teams を離れることなく、コンテンツを共有することでディスカッションを開始または追加できます。

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例は、作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

#### <a name="compose-box-layout-options"></a>作成ボックスのレイアウト オプション

リストビューやグリッド ビューなど、メッセージング拡張機能の検索結果を表示 [するためのいくつかのオプションがあります](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能の検索結果のレイアウト オプションを示す図。" border="false":::

### <a name="action-commands"></a>操作コマンド

アクション コマンドを使用すると、ユーザーは Teams 内の外部サービスでアクションをトリガーし、要求を処理できます。 たとえば、アプリで注文を追跡する場合、ユーザーはチャット内から同僚のメッセージの内容を使用して新しい注文を作成できます。

アクション ベースのメッセージング拡張機能では、多くの場合、モーダル内でフォームまたは他の種類の構成を完了する必要があります。 これらのエクスペリエンスは、タスク モジュールで [作成できます](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。

## <a name="open-a-messaging-extension"></a>メッセージング拡張機能を開く

作成ボックスとメッセージ/投稿は、ユーザーがメッセージング拡張機能を使用する主要なコンテキストです。

### <a name="from-the-compose-box"></a>作成ボックスから

追加すると、ユーザーは作成ボックスの下にあるアプリ アイコンを選択して、メッセージング拡張機能を開くことができます。 この例では、拡張機能に検索コマンドとアクション コマンドがあります。

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>チャット メッセージまたはチャネル投稿から

追加すると、ユーザーはチャット メッセージまたはチャネル投稿の [その他] アイコンを選択して、拡張機能の :::image type="icon" source="../../assets/icons/teams-client-more.png"::: アクション コマンドを見つけることができます。 拡張機能が [使用状況に基づくその他 **のアクション] の下** に表示される場合があります。

> [!NOTE]
> Microsoft Teams モバイル プラットフォームでは、チャット メッセージまたはチャネル投稿からのその他のアクションのサポートは利用できません。 

#### <a name="chat-message"></a>チャット メッセージ

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャット メッセージからメッセージング拡張機能を開く方法を示しています。" border="false":::

#### <a name="channel-post"></a>チャネル投稿

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="例は、チャネル投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

## <a name="use-a-messaging-extension"></a>メッセージング拡張機能を使用する

次のシナリオは、ユーザーがメッセージング拡張機能を使用する主な方法を示しています。

### <a name="insert-content-into-a-message"></a>メッセージにコンテンツを挿入する

**1. メッセージング拡張機能を選択します**。 ユーザーは、作成ボックスから共有するコンテンツを検索できます。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="例は、作成ボックスから挿入するコンテンツを検索しているユーザーを示しています。" border="false":::

**2. コンテンツを挿入します**。 投稿後、他のユーザーはコンテンツに返信または選択して、アプリの詳細を表示できます。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="例は、チャネル会話にコンテンツを投稿するユーザーを示しています。" border="false":::

### <a name="take-action-on-a-message"></a>メッセージに対してアクションを実行する

**1. メッセージング拡張機能を選択します**。 アプリには、1 つ以上のアクション コマンドを含めできます。

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="例は、メッセージング拡張機能アクション コマンドを選択しているユーザーを示しています。" border="false":::

**2. アクションを完了します**。 アプリは、メッセージ アクションによって送信されたコンテンツまたはデータを受信および処理できます。 これにより、ユーザーは会話を続け、次の例では、アプリに直接情報を入力する心配はありません。

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="メッセージに対してアクションを実行する方法の例。" border="false":::

### <a name="preview-links"></a>リンクのプレビュー

メッセージング拡張機能を使用すると、認識された URL からメッセージにリッチ リンクを挿入することもできます (この機能はリンク解除と [呼ばれる](../../messaging-extensions/how-to/link-unfurling.md).)

**1. 作成ボックスに認識されたリンク** を貼り付けます。

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="例では、ユーザーがコンポスト ボックスにリンクを貼り付けする例を示します。" border="false":::

**2. コンテンツを挿入します**。 アプリが作成ボックス内の URL を認識すると、リンクは、Web コンテンツのコンテンツリッチ プレビューを提供するカードとしてレンダリングされます。 (詳細 [については、「アダプティブ カードの設計ガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md) 」を参照してください)。

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="例は、URL がアプリによって認識されるので、作成ボックスにリッチ コンテンツを含む方法を示しています。" border="false":::

## <a name="manage-a-messaging-extension"></a>メッセージング拡張機能の管理

アイコンを右クリックすると、ユーザーはメッセージング拡張機能をピン留め、削除、または構成できます。

## <a name="anatomy"></a>構造

### <a name="messaging-extension-in-the-compose-box"></a>作成ボックスのメッセージング拡張機能

次の例は、作成ボックスから開いたメッセージング拡張機能です。

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="作成ボックスのメッセージング拡張機能の UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリのロゴ**: アプリのロゴの色のアイコン。|
|2|**アプリ名**: アプリの完全な名前。|
|3|**[アクション コマンド] メニュー アイコン (オプション)**: メッセージング拡張機能のアクション コマンドの一覧を開きます (指定した場合)。
|4|**[検索]** ボックス : ユーザーが挿入するアプリ コンテンツを検索できます。|
|5|**タブ メニュー (オプション)**: 複数のコンテンツ カテゴリを提供します。|
|6|**[アクション コマンド] メニュー (オプション)**: アクション コマンドの一覧を表示します (指定した場合)。|
|7|**アプリのコンテンツ**: 主に検索結果を表示します。 この例では、リスト レイアウトを使用しています (グリッド レイアウトは別のオプションです)。|
|8|**アプリのロゴ**: アプリロゴのアウトライン アイコン。|

### <a name="messaging-extension-management-menu"></a>メッセージング拡張機能の管理メニュー

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能管理メニューの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**[ピン留め** 解除] : ユーザーがアプリをピン留めしている場合に使用できます。|
|2|**削除**: チャネル、チャット、または会議からメッセージング拡張機能を削除します。|

## <a name="best-practices"></a>ベスト プラクティス

### <a name="setup-and-general-usage"></a>セットアップと一般的な使用方法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="セットアップと一般的な使用方法の例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Do: シングル サインオンとの統合

SSO を使用すると、サインイン プロセスが簡単、高速、およびセキュリティで保護されます。 また、ユーザーが個人用アプリに既にサインインしている場合は、メッセージング拡張機能にアクセスするためにもう一度サインインする必要はありません。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="シングル サインオンとの統合の例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>[しない]: ユーザーを会話から離す

メッセージング拡張機能は、コンテキストの切り替えを減らすことが想定されるショートカットです。 拡張機能は、たとえば、Teams の外部の Web ページにユーザーを指示する必要があります。

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Do: メッセージング拡張機能を強調表示する

メッセージング拡張機能は、必ずしも簡単に見つけることができるとは限らない。 アプリの詳細ページに、その使い方のスクリーンショットを含める。 アプリにボットも含まれる場合は、ボットウェルカム ツアーにメッセージング拡張機能のヘルプ ドキュメントを含めることができます。

### <a name="templating"></a>テンプレート

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="テンプレートの例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Do: 可能であれば、Teams が設計作業の一部を処理する

使用例に合う場合は、検索ベースのメッセージング拡張機能の作成を検討してください。 Teams は、これらの種類の拡張機能を、組み込みのユーザー設定とアクセシビリティでレンダリングします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="設計作業の処理例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>[しない] タスク モジュールにアプリ全体を埋め込む

メッセージング拡張機能でアクション コマンドが必要な場合は、タスク モジュールをシンプルにし、アクションを完了するために必要なコンポーネントのみを表示します。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="例: それらを使用します。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do: Teams カラー トークンを活用する

各 Teams テーマには、独自の配色があります。 テーマの変更を自動的に処理するには、デザインでカラー <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">トークン (Fluent UI)</a> を使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="カラー トークンの例。" border="false":::

#### <a name="dont-hard-code-color-values"></a>[しない] : ハード コードの色の値

Teams カラー トークンを使用しない場合、デザインの拡張性が低く、管理に時間がかかっています。

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="アクションの例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Do: コンテキストで意味のあるアクション コマンドを含める

メッセージアクションは、ユーザーが見ているものに関連する必要があります。 たとえば、ユーザーの投稿のテキストを使用して、問題や作業項目を作成するためのショートカットをユーザーに提供します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="アクション コマンドの例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>[しない]: コンテキストに依存しないアクション コマンドを含める

[ダッシュボードを表示する] というメッセージ **アクションは** 、ほとんどの会話から切断されている可能性があります。

   :::column-end:::
:::row-end:::

### <a name="searches"></a>検索

#### <a name="do-show-search-results-while-typing"></a>Do: 入力中に検索結果を表示する

ユーザーが入力している間に、検索結果の候補を提供します。 最小限の文字数で、必要なコンテンツをより速く見つける場合があります。

#### <a name="dont-require-users-to-submit-a-query"></a>[しない]: ユーザーにクエリの送信を要求する

ユーザーにキーを押させるか、ボタンを選択してアプリにクエリを送信できます。 アプリ サービス サービスの方が簡単ですが、ユーザーは、入力時にリアルタイムの検索結果が表示されないと混乱する可能性があります。

#### <a name="do-consider-zero-term-queries"></a>Do: ゼロ用語クエリを検討する

たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示した情報を表示します。 会話にコンテンツを挿入する可能性があります。

## <a name="validate-your-design"></a>デザインを検証する

AppSource にアプリを公開する予定がある場合、アプリの提出時に失敗する原因となるデザイン上の問題を理解しておく必要があります。

> [!div class="nextstepaction"]
> [デザイン検証ガイドラインをチェックする](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
