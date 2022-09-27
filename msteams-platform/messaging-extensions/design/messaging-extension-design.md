---
title: メッセージ拡張機能のデザイン
description: Teams のメッセージ拡張機能をデザインして、Microsoft Teams UI Kit を取得する方法をご紹介します。 Teams の設計ガイドラインに関するリファレンス メッセージ拡張機能のヒントとベスト プラクティスについて説明します。
author: heath-hamilton
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: conceptual
ms.openlocfilehash: bb85c9c7d00fea47796e171cc1a0175367462942
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027082"
---
# <a name="designing-your-microsoft-teams-message-extension"></a>Microsoft Teams メッセージ拡張機能のデザイン

メッセージ拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作したりするためのショートカットです。
アプリのデザインに役立てるために、次の情報では、Teams でユーザーがどのようにメッセージ拡張機能を追加、使用、管理できるかを説明、図解しています。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit には、必要に応じて把握、変更できる要素を含む、より包括的なメッセージ拡張機能のデザインのガイドラインが掲載されています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-message-extension"></a>メッセージ拡張機能を追加する

メッセージ拡張機能は、次の Teams コンテキストで追加できます。

* Teams ストアから。
* 作成ボックスの近くにあるチャネル、チャット、または会議中 (または前後)。 これらの場所のいずれかにメッセージ拡張機能を追加すると、そのコンテキストで使用できるのは自分だけであるという点に注意してください。

次の例は、チャネルにメッセージ拡張機能を追加する方法を示しています。

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="例は、モバイルのチャネルの作成ボックスの近くにメッセージ拡張機能を追加する方法を示しています。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの作成ボックスの近くにメッセージ拡張機能を追加する方法を示しています。":::

## <a name="set-up-a-message-extension"></a>メッセージ拡張機能を設定する

認証は必須ではありませんが、アプリがチケット追跡ツールのようなものの場合は、メッセージ拡張機能を使用するためにユーザーにサインインしてもらう必要がある場合もあります。

Teams アプリ間で一貫性を保つために、サインイン画面をカスタマイズすることはできません。 シングル サインオン (SSO) 認証を使用すると、ユーザーは自動的にサインインします。

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="モバイルでサインイン ボタンを含むメッセージ拡張機能の設定画面を示す例です。":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="サインイン ボタンを含むメッセージ拡張機能の設定画面を示す例です。":::

## <a name="types-of-message-extensions"></a>メッセージ拡張機能の種類

メッセージ拡張機能には、検索コマンド、アクション コマンド、またはその両方を含めることができます。 コマンドは、アプリの機能と、Teams のユース ケース内でどのように適合するかによって異なります。

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、ユーザーはメッセージ拡張機能を使用して外部コンテンツをすばやく検索し、メッセージに挿入できます。 検索コマンドは、通常、作成ボックスで使用できます。 たとえば、Teams から離れることなくコンテンツを共有することで、ディスカッションを開始またはディスカッションに追加できます。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="例では、モバイルで作成ボックスから起動された検索ベースのメッセージ拡張機能を示しています。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例では、作成ボックスから起動された検索ベースのメッセージ拡張機能を示しています。":::

#### <a name="compose-box-layout-options"></a>作成ボックスのレイアウト オプション

メッセージ拡張機能の検索結果を表示するには、[リスト ビューやグリッド ビュー](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)など、いくつかのオプションがあります。

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージ拡張機能の検索結果のレイアウト オプションを示す図。":::

### <a name="action-commands"></a>操作コマンド

アクション コマンドを使用すると、ユーザーは Teams 内の外部サービスでアクションをトリガーし、要求を処理できます。 たとえば、アプリが注文を追跡する場合、ユーザーはチャット内から同僚のメッセージの内容を使用して新しい注文を作成できます。

アクション ベースのメッセージ拡張機能では、多くの場合、ユーザーはフォーム、またはモーダル内でその他の種類の構成を完了する必要があります。 [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用して、これらのエクスペリエンス作成できます。

## <a name="open-a-message-extension"></a>メッセージ拡張機能を開く

ユーザーがメッセージ拡張機能を使用する主要なコンテキストは、作成ボックスと、メッセージまたは投稿です。

### <a name="from-the-compose-box"></a>作成ボックスから

追加すると、ユーザーは作成ボックスの下にあるアプリ アイコンを選択して、メッセージ拡張機能を開くことができます。 これらの例では、拡張機能に検索コマンドとアクション コマンドがあります。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="例は、モバイルで作成ボックスからメッセージ拡張機能を開く方法を示しています。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、作成ボックスからメッセージ拡張機能を開く方法を示しています。":::

### <a name="from-a-chat-message-or-channel-post"></a>チャット メッセージまたはチャネルの投稿から

追加すると、ユーザーはチャット メッセージまたはチャネル投稿の **[その他]** の:::image type="icon" source="../../assets/icons/teams-client-more.png":::アイコンを選択して、拡張機能のアクション コマンドを見つけることができます。 拡張機能は、使用状況に基づいて **その他のアクション** に一覧表示される場合があります。

#### <a name="chat-message"></a>チャット メッセージ

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャット メッセージからメッセージ拡張機能を開く方法を示しています。":::

#### <a name="channel-post"></a>チャネルの投稿

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="例は、モバイルでチャネルの投稿からメッセージ拡張機能を開く方法を示しています。":::

## <a name="use-a-message-extension"></a>メッセージ拡張機能の使用

次のシナリオでは、ユーザーがメッセージ拡張機能を使用する主な方法を示します。

### <a name="insert-content-into-a-message"></a>メッセージにコンテンツを挿入する

**1. Select a message extension**. Users can search for the content they want to share from the compose box.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="たとえば、モバイルで作成ボックスから挿入するコンテンツを検索するユーザーを示しています。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="作成ボックスから挿入するコンテンツを検索するユーザーの例を示します。":::

**2. Insert content**. Once posted, others can reply or select the content to see more information in your app.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="ユーザーがモバイルでチャネルの会話にコンテンツを投稿する例を示します。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="ユーザーがチャネルの会話にコンテンツを投稿する例を示します。":::

### <a name="take-action-on-a-message"></a>メッセージに対してアクションを取る

**1. メッセージ​​拡張機能の選択**。 アプリには、1 つ以上のアクション コマンドを含めることができます。

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="ユーザーがメッセージ拡張機能のアクション コマンドを選択する例を示しています。":::

**2. アクションの完了**。 アプリは、メッセージ アクションによって送信されたコンテンツやデータを受信して処理できます。 ユーザーは会話を続けながら、アプリでアクションを完了します。

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="メッセージに対してアクションを実行する方法の例。":::

### <a name="preview-links"></a>リンクのプレビュー

メッセージ拡張機能を使用すると、認識された URL からメッセージにリッチなリンクを挿入することもできます (この機能は、[リンク展開の解除](../../messaging-extensions/how-to/link-unfurling.md) と呼ばれます)。

**1. 認識されたリンク** を作成ボックスに貼り付けます。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="例では、モバイルでユーザーが作成ボックスにリンクを貼り付ける例を示しています。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="たとえば、ユーザーが作成ボックスにリンクを貼り付ける例を示しています。":::

**2. Insert content**. If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content. (See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="例は、モバイルで URL がアプリによって認識されるから作成ボックスにリッチ コンテンツを含める方法を示しています。":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="例は、URL がアプリに認識されてから作成ボックスにリッチ コンテンツを含める方法を示しています。":::

## <a name="manage-a-message-extension"></a>メッセージ拡張機能の管理

アイコンを右クリックすると、ユーザーはメッセージ拡張機能のピン留め、削除、または構成を行うことができます。

## <a name="anatomy"></a>構造

### <a name="message-extension-in-the-compose-box"></a>作成ボックスのメッセージ拡張機能

次の例は、作成ボックスから開かれたメッセージ拡張機能です。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="モバイルで作成ボックスのメッセージ拡張機能の UI 構造を示す図。":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ名**: アプリのフル ネーム|
|2|**[アクション コマンド] メニュー アイコン (省略可能)**: メッセージ拡張機能のアクション コマンドのリストを開きます (指定した場合)。
|3|**検索ボックス**: ユーザーが挿入するアプリ コンテンツを検索できるようにします。|
|4|**タブ メニュー (省略可能)**: 複数のコンテンツ カテゴリを提供します。|
|5|**[アクション コマンド] メニュー (省略可能)**: アクション コマンドのリストを表示します (指定した場合)。|
|6|**アプリ コンテンツ**: 主に検索結果を表示します。|

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="作成ボックスのメッセージ拡張機能の UI 構造を示す図。":::

|カウンター|説明|
|----------|-----------|
|1|**アプリのロゴ**: アプリのロゴの色アイコン。|
|2|**アプリ名**: アプリのフル ネーム|
|3|**[アクション コマンド] メニュー アイコン (省略可能)**: メッセージ拡張機能のアクション コマンドのリストを開きます (指定した場合)。
|4|**検索ボックス**: ユーザーが挿入するアプリ コンテンツを検索できるようにします。|
|5|**タブ メニュー (省略可能)**: 複数のコンテンツ カテゴリを提供します。|
|6|**[アクション コマンド] メニュー (省略可能)**: アクション コマンドのリストを表示します (指定した場合)。|
|7 |**アプリ コンテンツ**: 主に検索結果を表示します。 この例では、リスト レイアウトを使用しています (グリッド レイアウトは別のオプションです)。|
|8 |**アプリのロゴ**: アプリのロゴの枠線アイコン。|

### <a name="message-extension-management-menu"></a>メッセージ拡張機能の管理メニュー

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージ拡張機能の管理メニューの UI 構造を示す図。":::

|カウンター|説明|
|----------|-----------|
|1|**ピン留めを外す**: ユーザーがアプリをピン留めしている場合に使用できます。|
|2|**削除**: チャネル、チャット、または会議からメッセージ拡張機能を削除します。|

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="setup-and-general-usage"></a>セットアップと一般的な使用方法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="セットアップと一般的な使用方法の例。":::

#### <a name="do-integrate-with-single-sign-on"></a>Do: シングル サインオンとの統合

SSO makes the sign-in process easier, faster, and secure. Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the message extension.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="シングル サインオンとの統合の例。":::

#### <a name="dont-take-users-away-from-the-conversation"></a>Don't: ユーザーを会話から除外しないでください

メッセージ拡張機能は、コンテキストの切り替えを減らすはずのショートカットです。 拡張機能は、たとえば、Teams の外部の Web ページにユーザーを誘導するものであってはいけません。

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-message-extension"></a>Do: メッセージ拡張機能のハイライト

メッセージ拡張機能は、必ずしも簡単に見つかるとは限りません。 アプリの詳細ページにその使用方法のスクリーンショットを含めます。 アプリにボットも含まれている場合は、ボットウェルカム ツアーにメッセージ拡張機能のヘルプ ドキュメントを含めることができます。

### <a name="templating"></a>テンプレート作成

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="テンプレートの例。":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Do: 可能であれば、Teams が設計作業の一部を処理できるようにします

ユース ケースに適している場合は、検索ベースのメッセージ拡張機能を作成することを検討してください。 Teams は、これらの種類の拡張機能を、組み込みのテーマ設定とアクセシビリティでレンダリングします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="設計作業を処理する例。":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>Don't: アプリ全体をタスク モジュールに埋め込まないでください

メッセージ拡張機能でアクション コマンドが必要な場合は、タスク モジュールをシンプルにし、アクションを完了するために必要なコンポーネントのみを表示します。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="テーマの例。":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>実行: Teams のカラー トークンを活用する

各 Teams テーマには独自の配色があります。 テーマの変更を自動的に処理するには、デザインで[カラー トークン (Fluent UI)](https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme) を使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="カラー トークンの例。":::

#### <a name="dont-hard-code-color-values"></a>Don't: 色の値をハードコード化しないでください

Teams のカラー トークンを使用しない場合、デザインのスケーラビリティが低下し、管理に時間がかかります。

   :::column-end:::
:::row-end:::

### <a name="actions"></a>アクション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="アクションの例。":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Do: コンテキストで意味のあるアクション コマンドを含めます

メッセージ アクションは、ユーザーが見ている内容に関連している必要があります。 たとえば、他のユーザーの投稿のテキストを使用して、問題や作業項目を作成するためのショートカットをユーザーに提供します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="アクション コマンドの例。":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>Don't: コンテキストに依存しないアクション コマンドを含めないでください

**ダッシュボードを表示** するメッセージ アクションは、ほとんどの会話から切断されているように見える可能性があります。

   :::column-end:::
:::row-end:::

### <a name="searches"></a>検索

#### <a name="do-show-search-results-while-typing"></a>Do: 入力中に検索結果を表示します

ユーザーの入力中に、おすすめの検索結果を提供します。 最小限の文字数を入力するだけですばやくコンテンツを見つけることができます。

#### <a name="dont-require-users-to-submit-a-query"></a>Don't: ユーザーにクエリの送信を要求しないでください。

ユーザーがキーを押すか、またはボタンを選択してアプリにクエリを送信するようにすることができます。 App Services サービスの方が簡単な場合もありますが、ユーザーは入力時にリアルタイムの検索結果が表示されないと混乱する可能性があります。

#### <a name="do-consider-zero-term-queries"></a>Do: ゼロ用語クエリを検討してください

たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示した内容を表示します。 そのコンテンツを会話に挿入したい可能性があります。
