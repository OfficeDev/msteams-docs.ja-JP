---
title: デスクトップと Web 用のタブの設計
description: Teams タブ (デスクトップと Web) を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 840cb9f65f867358615ea006594433d8a1099111
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019686"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>Microsoft Teams デスクトップと Web 用のタブの設計

タブは、コンテンツの大きなキャンバスです。 アプリの設計をガイドするために、次の情報では、Teams でタブを追加、使用、管理する方法について説明し、説明します。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、包括的なタブ設計ガイドラインについては、Microsoft Teams UI Kit を参照してください。 UI キットには、ここでは説明しないアクセシビリティや応答性のサイジングなどの重要なトピックも含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>タブの追加

タブは、Teams ストア (AppSource) または次のいずれかのコンテキストから追加できます。

* チャット
* チャネル
* 会議 (会議の前、中、または後)

次の例は、チャネルにタブを追加する方法を示しています。

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルに追加されるタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a>タブを設定する

チャネル、チャット、または会議タブとしてアプリを追加する短いセットアップ プロセスがあります。エクスペリエンスは主にユーザーが行います。 たとえば、アプリの使い方とオプションの設定について説明できます。 ユーザーを認証する必要がある場合は、ここにサインイン 手順を含める必要があります。

### <a name="tab-configuration-modal"></a>タブ構成モーダル

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブ構成モーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a>構造: タブ構成モーダル

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリのロゴ**: アプリのフルカラー アプリ ロゴ。|
|2|**アプリ名**: アプリの完全な名前。|
|3|**iframe**: アプリのコンテンツのレスポンシブ スペース (タブ設定や認証など)。|
|4|**リンクについて**: アプリの詳細、アプリで必要なアクセス許可、プライバシー ポリシーと利用規約へのリンクなど、アプリに関する詳細を示すダイアログを開きます。
|5|**[閉じる**] ボタン: モーダルを閉じます。|
|6|**[チーム メンバーに通知する] オプション**: モーダルは、他のユーザーがタブを追加したと知らせる投稿を作成する場合に尋ねるメッセージを表示します。|
|7|**[戻る**] ボタン: ダイアログが開いた場所に基づいて、前の手順に進みます。|
|8|**[保存]** ボタン: タブのセットアップを完了します。|

### <a name="tab-authentication-with-single-sign-on"></a>シングル サインオンを使用したタブ認証

ユーザーが Microsoft 資格情報を使用して最初にサインインする必要がある手順を追加できます。 この認証方法は、シングル サインオン (SSO) と呼ばれています。

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例では、タブ認証画面を表示します。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>UI テンプレートを使用したタブセットアップの設計

タブセットアップエクスペリエンスを設計するには、次のいずれかの Teams UI テンプレートを使用します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。

## <a name="view-a-tab"></a>タブを表示する

タブは Teams のフルスクリーン Web エクスペリエンスを提供し、共同作業用のコンテンツ (タスク ボードやダッシュボードなど) と重要な情報を表示できます。

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例では、タスク ボードを含むタブを示します。" border="false":::

### <a name="anatomy-tab"></a>構造: タブ

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**タブ名**: タブのナビゲーション ラベル。|
|2|**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。|
|3|**タブ チャット**: 右側にチャット スレッドを開き、ユーザーがコンテンツの横で会話を行えます。|
|4|**iframe**: タブのコンテンツを表示します。

### <a name="designing-a-tab-with-ui-templates"></a>UI テンプレートを使用したタブの設計

タブ エクスペリエンスを設計するには、次のいずれかの Teams UI テンプレートを使用します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。 一般に、タブ ナビゲーションは最小限に抑えます。

## <a name="use-a-tab-to-collaborate"></a>タブを使用して共同作業を行う

タブは、中央の場所でのコンテンツに関する会話を容易にするのに役立ちます。

### <a name="thread-discussion"></a>スレッドディスカッション

ユーザーは、新しいタブを追加すると、チャネルまたはチャットに自動的に投稿できます。これにより、チーム メンバーに新しいコンテンツが通知され、タブへのリンクが提供されるだけでなく、ユーザーはタブについて話し始めできます。

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているタブを示しています。" border="false":::

### <a name="side-by-side-discussion"></a>サイド バイ サイドディスカッション

タブのコンテンツを表示している間、ユーザーは次に会話をすることができます。

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例では、右側にチャットが開いているタブが表示されます。" border="false":::

### <a name="permissions-and-role-based-views"></a>アクセス許可と役割ベースのビュー

ユーザーのアクセス許可に応じて、タブエクスペリエンスが異なる場合があります。 たとえば、1 人のユーザーがサインインせずにタブにアクセスできます。 ただし、別のユーザーは署名する必要があります。また、若干異なるコンテンツが表示されます。

## <a name="manage-a-tab"></a>タブの管理

タブの名前の変更、削除、または変更を行うオプションを含めできます。

### <a name="anatomy-tab-menu"></a>構造: タブ メニュー

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブ メニューの UI 構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**設定**: (オプション) タブの追加後にタブの設定を変更できます。|
|2|**名前** の変更 : ユーザーは、チームにとってより意味のある名前をタブに付けることができます。|
|3|**[削除**] : チャネル、チャット、または会議からタブを削除します。|

## <a name="tab-notifications-and-deep-linking"></a>タブ通知とディープ リンク

タブへのディープ リンクを含むメッセージを送信できます。たとえば、カードには、ユーザーがタブ内のバグ全体を表示するために選択できるバグ データの概要が表示されます。タブ アクティビティに関するメッセージを送信すると、全員に明示的に通知することなく (つまり、ノイズのないアクティビティ) 意識が向上します。 必要に応じて@mentionユーザーを追加できます。

タブ アクティビティをユーザーに通知するには、次のいずれかの方法を使用します。

* **ボット**: タブ スレッドが対象の場合は特に、このメソッドが優先されます。 タブのスレッドスレッドスレッドは、最近アクティブな状態で表示されます。 また、このメソッドを使用すると、通知の送信方法を洗練できます。
* **メッセージ**: タブへの深いリンクを含むメッセージがユーザーのアクティビティ [フィードに表示されます](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。

## <a name="best-practices"></a>ベスト プラクティス

### <a name="collaboration"></a>グループ作業

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="図は、タブ ナビゲーションデザインの操作方法を示しています。" border="false":::

#### <a name="do-facilitate-conversation"></a>Do: 会話を促進する

ユーザーが話せるコンテンツとコンポーネントを含める。 チャット、チャネル、または会議のコンテキスト内に収まらない場合は、タブに属していない。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="例は、タブ ナビゲーションデザインで何をしないかを示しています。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>[しない]: タブを他の Web ページと同様に扱う

タブは、誰かが一度表示する可能性がある Web ページではない。 タブには、ユーザーが一緒に何かを達成するために必要な、最も重要で関連性の高いコンテンツが表示されます。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブ ナビゲーションデザインの操作方法を示す例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a>Do: タスクとデータを制限する

タブは、特定のニーズに対応する場合に最適です。 チームまたはグループに関連するタスクとデータのセットを制限します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブ ナビゲーションデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-embed-your-entire-app"></a>[しない]: アプリ全体を埋め込む

タブを使用して、複数レベルのナビゲーションと複雑な操作でアプリ全体を表示すると、情報の過負荷が発生します。

   :::column-end:::
:::row-end:::

### <a name="setup"></a>セットアップ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブ セットアップの設計を実行する方法を示す図。" border="false":::

#### <a name="do-keep-it-simple"></a>Do: シンプルに保つ

アプリで認証が必要な場合は、Microsoft シングル サインオン (SSO) を統合して、よりシームレスなサインイン エクスペリエンスを実現してください。 また、タブを追加するための重要な情報と手順のみを含める必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブ セットアップデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-have-too-many-steps"></a>[しない]: 手順が多すぎます

タブを追加するための不要な手順を削除します。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do: Teams カラー トークンを活用する

各 Teams テーマには、独自の配色があります。 テーマの変更を自動的に処理するには、デザインでカラー <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">トークン (Fluent UI)</a> を使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="dont-hard-code-color-values"></a>[しない] : ハード コードの色の値

Teams カラー トークンを使用しない場合、デザインの拡張性が低く、管理に時間がかかっています。

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>デザインを検証する

AppSource にアプリを公開する予定がある場合、アプリの提出時に失敗する原因となるデザイン上の問題を理解しておく必要があります。

> [!div class="nextstepaction"]
> [デザイン検証ガイドラインをチェックする](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
