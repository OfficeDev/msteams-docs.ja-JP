---
title: メッセージング拡張機能の設計
description: Teamsメッセージング拡張機能を設計し、Microsoft Teams UI キットを入手する方法について説明します。
keywords: チーム設計ガイドライン 参照メッセージング拡張機能のヒント ベスト プラクティス
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ed1f0f2eb2ce8d429a8a780bd2c4c4eb421d6d54
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566216"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Microsoft Teamsメッセージング拡張機能の設計

メッセージング拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作を行ったりするためのショートカットです。
アプリの設計をガイドするために、次の情報は、ユーザーがTeamsでメッセージング拡張機能を追加、使用、および管理する方法を説明します。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、包括的なメッセージング拡張機能の設計ガイドラインについては、「Microsoft Teams UI キット」を参照してください。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>メッセージング拡張機能を追加する

メッセージング拡張機能は、次のTeamsコンテキストで追加できます。

* Teams ストア (AppSource) から。
* チャンネル、チャット、または会議 (作成中、および後) で、作成ボックスの近く。 これらの場所のいずれかでメッセージング拡張機能を追加する場合は、そのコンテキストでしか使用できません。

次の例は、チャネルにメッセージング拡張機能を追加する方法を示しています。

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="例は、チャネルの作成ボックスの近くにメッセージング拡張機能を追加する方法を示しています。" border="false":::

## <a name="set-up-a-messaging-extension"></a>メッセージング拡張機能の設定

認証は必須ではありませんが、アプリがチケット追跡ツールのようなものの場合は、メッセージング拡張機能を使用するためにサインインするユーザーが必要な場合があります。

Teamsアプリ間で一貫性を保つには、サインイン画面をカスタマイズすることはできません。 シングル サインオン (SSO) 認証を使用する場合、ユーザーは自動的にサインインします。

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="例は、サインイン ボタンを使用してメッセージング拡張機能のセットアップ画面を示しています。" border="false":::

## <a name="types-of-messaging-extensions"></a>メッセージング拡張機能の種類

メッセージング拡張機能には、検索コマンド、アクション コマンド、またはその両方を含めることができます。 コマンドは、アプリの機能と、ユース ケース内での機能Teams合わせて異なります。

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、メッセージング拡張機能を使用して、外部コンテンツをすばやく検索し、メッセージに挿入できます。 検索コマンドは、通常、作成ボックスで使用できます。 たとえば、コンテンツを共有することでディスカッションを開始したり、ディスカッションに追加したりTeamsできます。

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="例は、新規作成ボックスから起動された検索ベースのメッセージング拡張機能を示しています。" border="false":::

#### <a name="compose-box-layout-options"></a>作成ボックスレイアウトオプション

[リスト ビューやグリッド ビュー](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)など、メッセージング拡張機能の検索結果を表示するためのオプションがいくつかあります。

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="メッセージング拡張機能の検索結果のレイアウト オプションを示す図。" border="false":::

### <a name="action-commands"></a>操作コマンド

アクションコマンドを使用すると、ユーザーはTeams内の外部サービスでアクションをトリガーし、要求を処理できます。 たとえば、アプリが注文を追跡する場合、ユーザーはチャット内から同僚のメッセージの内容を使用して新しい注文を作成できます。

アクションベースのメッセージング拡張機能では、多くの場合、ユーザーがフォームまたはその他の種類の構成をモーダル内で入力する必要があります。 [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用してこれらのエクスペリエンスを作成できます。

## <a name="open-a-messaging-extension"></a>メッセージング拡張機能を開く

作成ボックスとメッセージまたは投稿は、ユーザーがメッセージング拡張機能を使用する主要なコンテキストです。

### <a name="from-the-compose-box"></a>作成ボックスから

追加すると、ユーザーは作成ボックスの下にあるアプリアイコンを選択して、メッセージング拡張機能を開くことができます。 この例では、拡張機能には検索コマンドとアクションコマンドがあります。

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="例は、作成ボックスからメッセージング拡張機能を開く方法を示しています。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>チャット メッセージまたはチャネル投稿から

追加すると、ユーザーは :::image type="icon" source="../../assets/icons/teams-client-more.png"::: チャットメッセージまたはチャンネル投稿の[その他]アイコンを選択して、拡張機能のアクションコマンドを見つけることができます。 拡張機能は、使用状況に基づいて **[その他のアクション]** の下に表示される場合があります。

> [!NOTE]
> チャット メッセージやチャネル投稿からのその他のアクションのサポートは、モバイル プラットフォームではMicrosoft Teamsできません。 

#### <a name="chat-message"></a>チャット メッセージ

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="例は、チャット メッセージからメッセージ拡張機能を開く方法を示しています。" border="false":::

#### <a name="channel-post"></a>チャンネル投稿

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="例は、チャネル投稿からメッセージング拡張機能を開く方法を示しています。" border="false":::

## <a name="use-a-messaging-extension"></a>メッセージング拡張機能を使用する

次のシナリオは、ユーザーがメッセージング拡張機能を使用する主な方法を示しています。

### <a name="insert-content-into-a-message"></a>メッセージにコンテンツを挿入する

**1. メッセージング拡張機能 を選択** します。 ユーザーは、作成ボックスから共有するコンテンツを検索できます。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="例は、作成ボックスから挿入するコンテンツを検索するユーザーを示しています。" border="false":::

**2. コンテンツを挿入** します。 投稿されると、他のユーザーは返信したり、コンテンツを選択して、アプリの詳細情報を表示したりできます。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="例は、ユーザーがチャネル会話にコンテンツを投稿する例です。" border="false":::

### <a name="take-action-on-a-message"></a>メッセージに対するアクションの実行

**1. メッセージング拡張機能 を選択** します。 アプリには、1 つ以上のアクション コマンドを含めることができます。

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="例は、メッセージング拡張機能アクション コマンドを選択するユーザーを示しています。" border="false":::

**2. アクションを完了します**。 アプリは、メッセージ アクションによって送信されたコンテンツやデータを受信して処理できます。 これにより、ユーザーは会話を続けることができ、次の例では、アプリに直接情報を入力する心配はありません。

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="メッセージに対するアクションの実行方法の例。" border="false":::

### <a name="preview-links"></a>プレビュー リンク

また、メッセージング拡張機能を使用すると、認識された URL からリッチ リンクをメッセージに挿入することもできます (この機能は [リンク展開](../../messaging-extensions/how-to/link-unfurling.md)と呼ばれます)。

**1. 認識されたリンクを作成ボックスに貼り付けます** 。

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="例は、ユーザーがコンポスト ボックスにリンクを貼り付けた場合を示しています。" border="false":::

**2. コンテンツを挿入** します。 アプリが作成ボックス内の URL を認識すると、Web コンテンツのコンテンツリッチ プレビューを提供するカードとしてリンクがレンダリングされます。 (詳細については [、アダプティブ カード設計ガイドライン](../../task-modules-and-cards/cards/design-effective-cards.md) を参照してください)。

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="URL がアプリで認識されるため、URL に作成ボックスにリッチ コンテンツが含まれる方法を例に示します。" border="false":::

## <a name="manage-a-messaging-extension"></a>メッセージング拡張機能の管理

アイコンを右クリックすると、ユーザーはメッセージング拡張機能をピン留め、削除、または構成できます。

## <a name="anatomy"></a>構造

### <a name="messaging-extension-in-the-compose-box"></a>[新規作成] ボックスのメッセージング拡張機能

次の例は、作成ボックスから開いたメッセージング拡張機能です。

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="作成ボックス内のメッセージング拡張機能の UI の解剖学を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリロゴ**: アプリロゴのカラーアイコン。|
|2|**アプリ名**: アプリのフルネーム。|
|3|**アクションコマンドメニューアイコン(オプション)**: メッセージング拡張機能のアクションコマンドのリストを開きます(指定した場合)。
|4|**検索ボックス**: ユーザーは、挿入するアプリのコンテンツを検索できます。|
|5|**タブメニュー (オプション)**: 複数のコンテンツカテゴリを提供します。|
|6|**[アクション コマンド] メニュー (オプション):** アクション コマンドの一覧を表示します (指定した場合)。|
|7|**アプリコンテンツ**: 主に検索結果を表示します。 ここでの例は、リストレイアウトを使用しています(グリッドレイアウトは別のオプションです)。|
|8|**アプリロゴ**: アプリロゴのアウトラインアイコン。|

### <a name="messaging-extension-management-menu"></a>メッセージング拡張機能管理メニュー

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="メッセージング拡張機能管理メニューの UI の構成を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**固定解除**: ユーザーがアプリをピン留めしている場合に使用できます。|
|2|**削除**: チャネル、チャット、または会議からメッセージ拡張機能を削除します。|

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="setup-and-general-usage"></a>セットアップと一般的な使用法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="セットアップと一般的な使用方法の例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>行う: シングル サインオンと統合

SSO により、サインイン プロセスがより簡単、より高速、およびセキュリティで保護されます。 また、ユーザーが個人用アプリに既にサインインしている場合は、メッセージング拡張機能にアクセスするために再度サインインする必要はありません。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="シングル サインオンとの統合の例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>しない: ユーザーを会話から遠ざける

メッセージング拡張機能は、コンテキストの切り替えを減らすことが想定されるショートカットです。 たとえば、拡張機能では、Teamsの外部の Web ページにユーザーを誘導しないでください。

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>行う: メッセージング拡張機能を強調表示します。

メッセージング拡張機能は、必ずしも簡単に見つけるとは限りません。 アプリの詳細ページに、その使用方法のスクリーンショットを含めます。 アプリにボットも含まれている場合は、ボットのウェルカム ツアーにメッセージング拡張機能のヘルプ ドキュメントを含めることができます。

### <a name="templating"></a>テンプレート

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="テンプレートの例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>行う:可能であれば、Teams設計作業の一部を処理してみましょう

ユース ケースに適している場合は、検索ベースのメッセージング拡張機能を作成することを検討してください。 Teamsでは、組み込みのテーマとアクセシビリティを備えたこれらのタイプの拡張機能をレンダリングします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="設計作業の処理例" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>しない: タスク モジュールにアプリ全体を埋め込む

メッセージング拡張機能でアクション コマンドが必要な場合は、タスク モジュールをシンプルにし、アクションを完了するために必要なコンポーネントのみを表示します。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="テーマの例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>行う: カラートークンTeams活用する

各Teamsテーマには独自の配色があります。 テーマの変更を自動的に処理するには、 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">デザインでカラー トークン (Fluent UI) を</a> 使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="カラートークンの例。" border="false":::

#### <a name="dont-hard-code-color-values"></a>しない: ハードコードのカラー値

Teams色のトークンを使用しない場合、デザインの拡張性が低下し、管理に時間がかかります。

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="アクションの例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>行う: コンテキストで意味のあるアクション コマンドを含める

メッセージアクションは、ユーザーが見ているものに関連付ける必要があります。 たとえば、ユーザーの投稿のテキストを使用して問題や作業項目を作成するためのショートカットをユーザーに提供します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="アクション コマンドの例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>しない: コンテキストに依存しないアクション コマンドを含める

**ダッシュボードを表示** するメッセージ アクションは、ほとんどの会話から切断されているように見えるでしょう。

   :::column-end:::
:::row-end:::

### <a name="searches"></a>検索

#### <a name="do-show-search-results-while-typing"></a>行う: 入力中に検索結果を表示する

ユーザーが入力している間に、推奨される検索結果を提供します。 必要なコンテンツは最小限の文字ですばやく見つかる場合があります。

#### <a name="dont-require-users-to-submit-a-query"></a>しない: ユーザーにクエリの送信を要求する

ユーザーがキーを押したり、ボタンを選択してアプリにクエリを送信したりできます。 アプリ サービス サービスでは、この操作が簡単に行える場合がありますが、入力時にリアルタイムの検索結果が表示されないという混乱が生じる場合があります。

#### <a name="do-consider-zero-term-queries"></a>実行: ゼロターム クエリを検討する

たとえば、ユーザーが検索ボックスに何かを書き込む前に、アプリで最後に表示された内容を表示します。 そのコンテンツを会話に挿入したい場合があります。
