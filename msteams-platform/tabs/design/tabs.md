---
title: デスクトップと Web 用のタブの設計
description: Teamsタブ(デスクトップとウェブ)を設計し、UIキットMicrosoft Teamsを入手する方法を学びます。
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: baa17cd97ff4e2cad91615dced5c4e4cf5e533c8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566881"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>デスクトップと Web Microsoft Teams用のタブの設計

タブは、コンテンツ用の大きなキャンバスです。 アプリのデザインをガイドするために、次の情報は、ユーザーがTeamsでタブを追加、使用、および管理する方法を説明します。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、包括的なタブデザインガイドラインは、Microsoft Teams UI キットで確認できます。 UI キットには、ここでは説明されていないアクセシビリティやレスポンシブ サイジングなどの重要なトピックもあります。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>タブの追加

Teams ストア (AppSource) または次のいずれかのコンテキストでタブを追加できます。

* チャット
* チャネル
* 会議 (会議の前、中、または後)

次の例は、チャネルにタブを追加する方法を示しています。

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルに追加されるタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a>タブを設定する

アプリをチャンネル、チャット、または会議タブとして追加する短いセットアッププロセスがあります。経験は主にあなた次第です。 たとえば、アプリの使用方法といくつかのオプション設定の説明を持つことができます。 ユーザーを認証する必要がある場合は、ここにサインイン手順を含めます。

### <a name="tab-configuration-modal"></a>タブコンフィギュレーションモーダル

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブ構成モーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a>構造: タブ構成モーダル

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリロゴ**: アプリのフルカラーアプリロゴ。|
|2|**アプリ名**: アプリのフルネーム。|
|3|**iframe**: アプリのコンテンツのレスポンシブスペース。 たとえば、タブ設定や認証などです。|
|4|**リンクについて**: 完全な説明、アプリで必要なアクセス許可、プライバシー ポリシーや利用規約へのリンクなど、アプリに関する詳細情報を示すダイアログが開きます。
|5|**閉じるボタン**: モーダルを閉じます。|
|6|**チームメンバーに通知オプション**: モーダルは、タブを追加した投稿を他の人に知らせる投稿を作成するかどうかを尋ねます。|
|7|**戻るボタン**: ダイアログが開いた場所に基づいて、前のステップに進みます。|
|8|**保存ボタン**: タブ設定を完了します。|

### <a name="tab-authentication-with-single-sign-on"></a>シングル サインオンによるタブ認証

ユーザーが最初に Microsoft 資格情報でサインインする必要がある手順を追加できます。 この認証方法は、シングル サインオン (SSO) と呼ばれます。

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例はタブ認証画面を示しています。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>UI テンプレートを使用したタブ設定の設計

次の Teams UI テンプレートのいずれかを使用して、タブのセットアップ エクスペリエンスを設計します。

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々の項目に対してアクションを実行できるようにします。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および送信するためのものです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。

## <a name="view-a-tab"></a>タブを表示する

タブは、タスクボードやダッシュボードなどのコラボレーションコンテンツや重要な情報を表示できるTeamsでの全画面表示の Web エクスペリエンスを提供します。

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例は、タスク ボードを含むタブを示しています。" border="false":::

### <a name="anatomy-tab"></a>解剖学: タブ

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI の解剖学を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブオーバーフロー**: 名前の変更や削除などのタブアクションを開きます。|
|3|**タブチャット**: 右側にチャットスレッドを開き、ユーザーがコンテンツの横で会話をすることができます。|
|4|**iframe**: タブのコンテンツを表示します。

### <a name="designing-a-tab-with-ui-templates"></a>UI テンプレートを使用したタブの設計

次のTeams UI テンプレートのいずれかを使用して、タブエクスペリエンスを設計します。

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々の項目に対してアクションを実行できるようにします。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスク ボードは、かんばんボードまたはスイム レーンとも呼ばれ、作業項目やチケットの状態を追跡するためによく使用されるカードの集まりです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および送信するためのものです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左のナビゲーション テンプレートは、タブが何らかのナビゲーションを必要とする場合に役立ちます。 通常、タブ ナビゲーションは最小限に抑える必要があります。

## <a name="use-a-tab-to-collaborate"></a>タブを使用して共同作業を行う

タブを使用すると、コンテンツに関する会話を一元的に行うことができます。

### <a name="thread-discussion"></a>スレッドディスカッション

ユーザーは、新しいタブを追加すると、チャンネルやチャットに自動的に投稿できます。これにより、チーム メンバーに新しいコンテンツが通知され、タブへのリンクが提供されるだけでなく、ユーザーがタブについて話し始めることができます。

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているタブを示しています。" border="false":::

### <a name="side-by-side-discussion"></a>サイドバイサイドディスカッション

ユーザーは、タブのコンテンツを表示しながら、次に会話をすることができます。

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例は、右側にチャットを開いたタブを示しています。" border="false":::

### <a name="permissions-and-role-based-views"></a>権限とロールベースのビュー

ユーザーのアクセス許可によって、タブの操作性が異なる場合があります。 たとえば、1 人のユーザーがサインインしなくてもタブにアクセスできます。 ただし、別のユーザーは署名する必要があり、わずかに異なるコンテンツが表示されます。

## <a name="manage-a-tab"></a>タブの管理

タブの名前変更、削除、または変更を行うオプションを含めることができます。

### <a name="anatomy-tab-menu"></a>解剖学:タブメニュー

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブ メニューの UI の概要を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**設定**: (オプション)タブを追加した後にタブの設定を変更できます。|
|2|**名前の変更**: ユーザーは、チームにとってよりわかりやすい名前をタブに付けできます。|
|3|**削除**: チャンネル、チャット、または会議からタブを削除します。|

## <a name="tab-notifications-and-deep-linking"></a>タブ通知とディープリンク

あなたのタブへの深いリンクを含むメッセージを送信することができます。たとえば、カードには、ユーザーが選択できるバグ データの概要がタブに表示されます。タブアクティビティに関するメッセージを送信すると、すべてのユーザーに明示的に通知することなく、認識が高まります(ノイズのないアクティビティ)。 必要に応じて特定のユーザーを@mentionすることもできます。

次のいずれかの方法でタブアクティビティをユーザーに通知します。

* **Bot**: このメソッドは、特にタブ スレッドが対象となる場合に推奨されます。 タブのスレッド化された会話は、最近アクティブになった時点で表示されます。 このメソッドは、通知の送信方法をいくらか高度に行うこともできます。
* **メッセージ**: ユーザーのアクティビティ フィードに、 [タブへのディープ リンク](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)を示すメッセージが表示されます。

## <a name="best-practices"></a>ベスト プラクティス

次の推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="collaboration"></a>グループ作業

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="図は、タブ ナビゲーションのデザインをどうするか示しています。" border="false":::

#### <a name="do-facilitate-conversation"></a>行う: 会話を促進する

ユーザーが話すことができるコンテンツとコンポーネントを含めます。 チャット、チャンネル、会議のコンテキストに合わない場合は、タブに含めることができません。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="例は、タブ ナビゲーションのデザインを使用しない方法を示しています。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>しない: タブを他のウェブページと同じように扱う

タブは、ユーザーが一度表示する Web ページではありません。 タブには、ユーザーが一緒に何かを達成するために必要な最も重要で関連性の高いコンテンツが表示されます。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブ ナビゲーションのデザインの操作方法を示す例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a>実行: タスクとデータを制限する

タブは、特定のニーズに対応する場合に最適に機能します。 チームまたはグループに関連するタスクとデータの限定されたセットを含めます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブ ナビゲーションのデザインを使用しない操作を示す図。" border="false":::

#### <a name="dont-embed-your-entire-app"></a>しない: アプリ全体を埋め込む

タブを使用して、マルチレベルナビゲーションと複雑な操作を含むアプリ全体を表示すると、情報の過負荷につながります。

   :::column-end:::
:::row-end:::

### <a name="setup"></a>セットアップ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブ設定デザインの処理方法を示す図。" border="false":::

#### <a name="do-keep-it-simple"></a>行う:それをシンプルに保つ

アプリで認証が必要な場合は、Microsoft シングル サインオン (SSO) を統合して、よりシームレスなサインイン エクスペリエンスを実現してください。 また、タブを追加するための重要な情報と手順のみを含めます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブ設定デザインを使用しない操作を示す図。" border="false":::

#### <a name="dont-have-too-many-steps"></a>しない: 手順が多すぎます

タブを追加するための不要な手順を削除します。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブテーマの処理方法を示す図。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>行う: カラートークンTeams活用する

各Teamsテーマには独自の配色があります。 テーマの変更を自動的に処理するには、 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">デザインでカラー トークン (Fluent UI) を</a> 使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブテーマを使用しない内容を示す図。" border="false":::

#### <a name="dont-hard-code-color-values"></a>しない: ハードコードのカラー値

Teams色のトークンを使用しない場合、デザインの拡張性が低下し、管理に時間がかかります。

   :::column-end:::
:::row-end:::
