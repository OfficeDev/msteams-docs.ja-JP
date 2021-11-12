---
title: デスクトップ、Web、およびモバイル用のデザイン タブ
description: デスクトップ、Web、およびモバイル用の Teams タブを設計する方法を学び、Microsoft Teams UI キットを入手します。 タブの機能と外観、ユーザー認証の構築、タブ通知、タブでのディープ リンクについて説明します。
author: heath-hamilton
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
keywords: UI キット管理タブ セットアップ シングルサインオン sso ディープ リンク 役割ベースのビュー スレッド ディスカッション
ms.openlocfilehash: c2c081a1cb0ca96cce7cc55a9e39facc9cd691db
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948587"
---
# <a name="design-your-tab-for-microsoft-teams"></a>Microsoft Teams 用のタブを設計する

タブは、アプリ コンテンツ用の大きなキャンバスです。 アプリのデザインに役立てるために、次の情報では、Teams でユーザーがどのようにタブを追加、使用、管理できるかを説明、図解しています。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI キット

Microsoft Teams UI キットには、必要に応じて取得および変更できる要素を含む、包括的なタブ設計ガイドラインがあります。 UI キットには、アクセシビリティやレスポンシブ サイズ設定など、ここでは取り上げていない重要なトピックも含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI キット (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>タブを追加する

Teams ストア (AppSource) から、または次のいずれかのコンテキストでタブを追加できます。

* チャット
* チャネル
* 会議 (会議の前、中、または後に)

### <a name="mobile"></a>モバイル

ユーザーは、チャネルの **[その他]** ボタン (以下の例) を選択するか、タブが追加されたチャットを選択することで、タブにアクセスできます。

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="例は、チャネルに追加されているモバイル タブを示しています。" border="false":::

### <a name="desktop"></a>デスクトップ

次の例は、ユーザーがチャネルにタブを追加する方法を示しています。

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルに追加されているタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a>タブを設定する

アプリをチャネル、チャット、または会議タブとして追加するための短い設定プロセスがあります。このエクスペリエンスは主にユーザーが自由に決めることができます。 たとえば、アプリの使用方法といくつかのオプション設定の説明があります。 ユーザーを認証する必要がある場合は、ここにサインイン手順を含めてください。

### <a name="tab-configuration-dialog"></a>タブ構成ダイアログ

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブ構成モーダルを示しています。" border="false":::

#### <a name="anatomy-tab-configuration-dialog"></a>構造: タブ構成ダイアログ

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリのロゴ**: フルカラーのアプリ ロゴ。|
|2|**アプリ名**: アプリのフル ネーム|
|3|**iframe**: アプリのコンテンツ(タブ設定や認証など) のレスポンシブなスペース。|
|4|**リンクについて**: 完全な説明、アプリに必要な権限、プライバシー ポリシーとサービス使用条件へのリンクなど、アプリに関する詳細情報を表示するダイアログを開きます。|
|5|**[閉じる] ボタン**: ダイアログを閉じます。|
|6 |**[チーム メンバーに通知する] オプション**: このダイアログは、タブを追加したことを他の人に知らせる投稿を作成するかどうかをユーザーに確認します。|
|7 |**[戻る] ボタン**: ダイアログが開いた場所に基づいて、ひとつ前の手順に移動します。|
|8 |**[保存]** ボタン: タブ セットアップを完了します。|

### <a name="tab-authentication-with-single-sign-on"></a>シングル サインオンを使用したタブ認証

ユーザーが最初に Microsoft 資格情報を使用してサインインする必要があるステップを追加できます。 この認証方法は、シングル サインオン (SSO) と呼ばれています。

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例は、タブ認証画面を示しています。" border="false":::

### <a name="design-a-tab-setup-with-ui-templates"></a>UI テンプレートを使用してタブ セットアップを設計する

次の Teams UI テンプレートのいずれかを使用して、タブ セットアップ エクスペリエンスを設計します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。

## <a name="view-a-tab"></a>タブを表示する

タブは、Teams で全画面の Web エクスペリエンスを提供し、タスクボードやダッシュボードなどのグループ作業コンテンツや重要な情報を表示できます。

### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="例は、タスクボードを備えたモバイル タブを示しています。" border="false":::

### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例では、タスク ボードを含むタブを示しています。" border="false":::

### <a name="anatomy-tab"></a>構造: タブ

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="タブの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブ チャット**: ユーザーがコンテンツの横で会話を行えるチャットを開きます。|
|3|**webview**: アプリのコンテンツを表示します。|

#### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="この図は、タブの UI 構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。|
|3|**タブ チャット**: 右側にチャットを開き、ユーザーがコンテンツの横で会話を行えるようにします。|
|4|**iframe**: アプリのコンテンツを表示します。|

### <a name="design-a-tab-with-ui-templates-and-advanced-components"></a>UI テンプレートと高度なコンポーネントを使用してタブを設計する

次の Teams テンプレートとコンポーネントのいずれかを使用して、タブ エクスペリエンスの設計に役立ててください。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): かんばんボードまたはスイム レーンと呼ばれることもあるタスク ボードは、作業項目またはチケットのステータスを追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): タブにナビゲーションが必要な場合は、左側のナビゲーション コンポーネントが役立ちます。 一般に、タブ ナビゲーションは最小限に抑える必要があります。

## <a name="use-a-tab-to-collaborate"></a>タブを使用してグループ作業を行う

タブは、中央の場所にあるコンテンツに関する会話を容易にするのに役立ちます。

### <a name="thread-discussion"></a>スレッド ディスカッション

ユーザーは、新しいタブを追加すると、チャネルやチャットに自動的に投稿することができます。 これにより、チーム メンバーに新しいコンテンツが通知され、タブへのリンクが提供されるだけでなく、人々はタブについて話し始めることができます。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているモバイル タブを示しています。" border="false":::

#### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているタブを示しています。" border="false":::

### <a name="tab-chat"></a>タブ チャット

ユーザーは、表示しているタブ コンテンツの横で会話を行えます。 デスクトップでは、チャットはアプリ コンテンツの横に開きます。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="例は、コンテキスト内のチャット領域を持つモバイル タブを示しています。" border="false":::

#### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例は、右側にチャットが開いているタブを示しています。" border="false":::

### <a name="permissions-and-role-based-views"></a>アクセス許可と役割ベースのビュー

ユーザーのアクセス許可に応じて、タブ エクスペリエンスが異なる場合があります。 たとえば、1 人のユーザーはサインインせずにタブにアクセスできます。 しかし、別のユーザーはサインインする必要があり、少し異なるコンテンツが表示されます。

## <a name="manage-a-tab"></a>タブの管理

タブの名前を変更、削除、または変更するためのオプションを含めることができます。

### <a name="anatomy-tab-menu"></a>構造: タブ メニュー

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="モバイル タブ メニューの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**ブラウザーで開く**: デバイスの既定のブラウザーでアプリを開きます。|
|2|**[リンクのコピー]**: ユーザーは、タブへのリンクをコピーして共有できます。|
|3|**設定**: (オプション) タブの設定を追加した後に変更します。|
|4|**名前の変更**: ユーザーは、チャネル、チャット、または会議にとって意味のある名前をタブに付けることができます。|
|5|**削除**: チャネル、チャット、または会議からタブを削除します。|

#### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブ メニューの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**設定**: (オプション) タブが追加された後、ユーザーがタブの設定を変更できるようにします。|
|2|**名前の変更**: ユーザーは、チャネル、チャット、または会議にとって意味のある名前をタブに付けることができます。|
|3|**削除**: チャネル、チャット、または会議からタブを削除します。|

## <a name="tab-notifications-and-deep-linking"></a>タブ通知とディープ リンク

タブへのディープ リンクを含むメッセージを送信できます。 たとえば、カードには、ユーザーが選択してバグ全体をタブに表示できるバグ データの概要が表示されます。 タブ アクティビティに関するメッセージを送信すると、全員に明示的に通知することなく (つまり、ノイズのないアクティビティで) 意識が高まります。 必要に応じて @mention ユーザーを追加できます。

タブ アクティビティをユーザーに通知するには、次のいずれかの方法を使用します。

* **ボット**: タブ スレッドが対象の場合は特に、このメソッドが優先されます。 タブのスレッド化された会話は、最近アクティブになったものとして表示に移動されます。 この方法では、通知の送信方法をある程度洗練することもできます。
* **メッセージ**: [タブへのディープ リンク](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)を含むメッセージがユーザーのアクティビティ フィードに表示されます。

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="collaboration"></a>グループ作業

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="図は、タブ ナビゲーション デザインで何を行えば良いかを示しています。" border="false":::

#### <a name="do-facilitate-conversation"></a>するべきこと: 会話を促進する

ユーザーが話すことができるコンテンツとコンポーネントを含めてください。 チャット、チャンネル、または会議のコンテキストに収まらない場合は、タブに属していません。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="例は、タブ ナビゲーション デザインですべきでないことを示しています。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>すべきでないこと: タブを他の Web ページと同様に扱う

タブは、誰かが一度表示する可能性のある Web ページではありません。 タブには、人々が共同で何かを達成するために必要な、最も重要で関連性のあるコンテンツを表示する必要があります。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="例は、タブ ナビゲーション デザインで何を行えば良いかを示しています。" border="false":::

#### <a name="do-limit-tasks-and-data"></a>するべきこと: タスクとデータを制限する

タブは、特定のニーズに対応する場合に最適に機能します。 チームまたはグループに関連する限定されたタスクとデータのセットを含めてください。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブ ナビゲーションデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-embed-your-entire-app"></a>すべきでない事: アプリ全体を埋め込まないでください

タブを使用して、マルチ レベルのナビゲーションと複雑なインタラクションを備えたアプリ全体を表示すると、情報の過負荷が発生します。

   :::column-end:::
:::row-end:::

### <a name="setup"></a>セットアップ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブ セットアップの設計を実行する方法を示す図。" border="false":::

#### <a name="do-keep-it-simple"></a>するべきこと: シンプルに保つ

アプリで認証が必要な場合は、Microsoft シングル サインオン (SSO) を統合して、よりシームレスなサインイン エクスペリエンスを実現してください。 また、タブを追加するための重要な情報と手順のみを含めてください。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブ セットアップの設計で何をしないかを示す図。" border="false":::

#### <a name="dont-have-too-many-steps"></a>すべきでないこと: 手順を増やしすぎないでください。

タブを追加するための不要な手順を削除してください。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブのテーマをどうするかを示す図。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>実行: Teams のカラー トークンを活用する

各 Teams テーマには独自の配色があります。 テーマの変更を自動的に処理するには、デザインで<a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">カラー トークン (Fluent UI)</a> を使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブのテーマをどうすべきでないかを示す図。" border="false":::

#### <a name="dont-hard-code-color-values"></a>Don't: 色の値をハードコード化しないでください

Teams カラー トークンを使用しない場合、デザインの拡張性が低下し、管理に時間がかかります。

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>関連項目

[タブ余白の変更](~/resources/removing-tab-margins.md)
