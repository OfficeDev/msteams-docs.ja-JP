---
title: デスクトップと web 用のタブの設計
description: Teams タブ (デスクトップと web) を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604702"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>Microsoft Teams デスクトップおよび web 用のタブの設計

タブは、コラボレーションを促進するコンテンツの大きなキャンバスです。 アプリの設計をガイドするには、次の情報を参照して、Teams でのタブの追加、使用、管理を行う方法を示します。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、包括的なタブデザインガイドラインを見つけることができます。 UI キットには、ここでは説明していないアクセシビリティや応答性の高いサイズ変更などの重要なトピックもあります。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>タブの追加

Teams ストア (AppSource) または次のいずれかのコンテキストからタブを追加できます。

* チャット
* チャネル
* 会議 (会議の前、中、または後)

次の例は、チャネルにタブを追加する方法を示しています。

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルで追加されているタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a>タブを設定する

アプリをチャネル、チャット、または会議のタブとして追加するための短いセットアッププロセスがあります。これらの機能は、ユーザーにとって非常に大きくなります。 たとえば、アプリの使用方法とオプションの設定を行う方法について説明します。 ユーザーを認証する必要がある場合は、ここにサインイン手順を含めます。

### <a name="tab-configuration-modal"></a>タブの構成のモーダル

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブの構成のモーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a>構造: タブの構成のモーダル

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリロゴ**: アプリのフルカラーアプリのロゴ。|
|2 |**アプリ名**: アプリの完全な名前。|
|3 |**iframe**: アプリのコンテンツ (タブ設定または認証など) に対する応答性の高いスペース。|
|4 |**リンクについて**: 詳細な説明、アプリに必要なアクセス許可など、アプリに関する詳細情報を示すダイアログボックスを開き、プライバシーポリシーおよびサービス条件へのリンクを表示します。
|5 |**[閉じる] ボタン**: モーダルを閉じます。|
|6 |[**チームメンバーに通知する] オプション**: 他のユーザーにタブを追加することを知らせる投稿を作成するかどうかを確認するには、[モーダル] を選択します。|
|7 |[**戻る] ボタン**: ダイアログが開いている場所に基づいて、前の手順に進みます。|
|8 |[**保存] ボタン**: タブの設定を完了します。|

### <a name="tab-authentication-with-single-sign-on"></a>シングルサインオンを使用したタブ認証

ユーザーが Microsoft 資格情報を使用して最初にサインインする必要がある手順を追加できます。 この認証方法は、シングルサインオン (SSO) と呼ばれます。

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例は、タブ認証画面を示しています。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>UI テンプレートを使用してタブ設定を設計する

次の Teams UI テンプレートのいずれかを使用して、タブのセットアップ環境を設計します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。
* [Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。

## <a name="view-a-tab"></a>タブを表示する

タブは、チームで全画面表示の web 環境を提供します。これにより、コラボレーションコンテンツ (タスクボードやダッシュボードなど) や重要な情報を表示できます。

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例は、タスクボードを含むタブを示しています。" border="false":::

### <a name="anatomy-tab"></a>[構造]: タブ

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI の構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**[タブ名**]: タブのナビゲーションラベル。|
|2 |**Tab overflow**: 名前の変更や削除などのタブアクションを開きます。|
|3 |**タブチャット**: チャットスレッドを右側に開き、ユーザーがコンテンツの横に会話できるようにします。|
|4 |**iframe**: タブのコンテンツを表示します。

### <a name="designing-a-tab-with-ui-templates"></a>UI テンプレートを使用してタブを設計する

次の Teams UI テンプレートのいずれかを使用して、タブの動作を設計します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [タスクボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。
* [Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。
* [左](../../concepts/design/design-teams-app-ui-templates.md#left-nav)ナビゲーション: タブにいくつかのナビゲーションが必要な場合は、左側のナビゲーションテンプレートが役立ちます。 一般的に、タブナビゲーションは最小限にする必要があります。

## <a name="use-a-tab-to-collaborate"></a>タブを使用して共同作業する

タブを使用すると、コンテンツに関する会話を一元的に容易に行うことができます。

### <a name="thread-discussion"></a>スレッドディスカッション

新しいタブを追加すると、ユーザーはチャネルまたはチャットに自動的に投稿できるようになります。これにより、新しいコンテンツのチームメンバーに通知されるだけでなく、tab へのリンクも表示されるので、ユーザーはタブについての会話を開始できます。

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネルスレッドで説明されているタブを示しています。" border="false":::

### <a name="side-by-side-discussion"></a>Side-by-side ディスカッション

タブのコンテンツを表示しているときに、ユーザーは次の会話を行うことができます。

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例は、右側にチャットが開いているタブを示しています。" border="false":::

### <a name="permissions-and-role-based-views"></a>アクセス許可と役割ベースのビュー

ユーザーのアクセス許可によっては、タブの動作が異なる場合があります。 たとえば、1人のユーザーがサインインせずにタブにアクセスできます。 ただし、別のユーザーが署名する必要があり、多少異なる内容が表示されます。

## <a name="manage-a-tab"></a>タブを管理する

タブの名前変更、削除、または変更を行うオプションを含めることができます。

### <a name="anatomy-tab-menu"></a>分析: タブメニュー

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブメニューの UI の構造を示す図。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**設定**: (オプション) ユーザーが追加されたタブの設定を変更できます。|
|2 |[**名前の変更**]: ユーザーは、チームにとってわかりやすい名前をタブに付けることができます。|
|3 |**削除**: チャネル、チャット、または会議からタブを削除します。|

## <a name="tab-notifications-and-deep-linking"></a>タブ通知とディープリンク

詳細なリンクを持つメッセージをタブに送信できます。たとえば、カードはバグデータの概要を示しています。これは、ユーザーが選択してバグ全体をタブに表示することができます。Tab アクティビティに関するメッセージを送信すると、ユーザーに明示的に通知することなく (つまり、ノイズのないアクティビティ)、認識が向上します。 必要に応じて特定のユーザーを @mention することもできます。

Tab アクティビティをユーザーに通知するには、次のいずれかの方法を実行します。

* **Bot**: このメソッドは、特に tab スレッドが対象の場合に適しています。 タブのスレッドスレッドは、最近アクティブになったときと同じように表示に移動します。 また、このメソッドを使用すると、通知の送信方法をいくらか洗練することができます。
* **メッセージ**: ユーザーのアクティビティフィードにメッセージが表示され、 [タブへの詳細なリンク](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)が表示されます。

## <a name="best-practices"></a>ベスト プラクティス

### <a name="collaboration"></a>グループ作業

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="タブナビゲーションデザインの操作を示す図" border="false":::

#### <a name="do-facilitate-conversation"></a>Do: 会話を促進する

ユーザーが説明できるコンテンツとコンポーネントを含めます。 チャット、チャネル、または会議のコンテキスト内に収まらない場合は、タブに含まれません。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="タブナビゲーションデザインではできないことを示す図" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>いいえ: 他の web ページと同じようにタブを扱います

タブは、誰かが一度に表示する可能性がある web ページではありません。 タブには、ユーザーが共同作業を行うために必要とする、最も重要な関連コンテンツが表示されます。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>ナビゲーション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブナビゲーションデザインの操作を示す図" border="false":::

#### <a name="do-limit-tasks-and-data"></a>Do: タスクとデータを制限する

タブは特定のニーズに対応するために最適に機能します。 チームまたはグループに関連するタスクとデータの限定されたセットを含めます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブナビゲーションデザインではできないことを示す図" border="false":::

#### <a name="dont-embed-your-entire-app"></a>いいえ: アプリ全体を埋め込む

タブを使用して、複数レベルのナビゲーションを備えたアプリ全体を表示し、複雑な対話によって情報の過負荷につながります。

   :::column-end:::
:::row-end:::

### <a name="setup"></a>セットアップ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブセットアップデザインの操作を示す図" border="false":::

#### <a name="do-keep-it-simple"></a>Do: シンプルを維持する

アプリで認証が必要な場合は、Microsoft シングルサインオン (SSO) を統合して、よりシームレスなサインイン操作を実行してみてください。 また、基本的な情報と、タブを追加する手順についても記載します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブセットアップデザインでは実行しないことを示す図" border="false":::

#### <a name="dont-have-too-many-steps"></a>いいえ: 手順が多すぎます

タブを追加するための不要な手順を削除します。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>テーマ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブのテーマの操作を示す図" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do: Teams のカラートークンを活用する

各 Teams テーマには独自の配色があります。 テーマの変更を自動的に処理するには、設計で <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color token (FLUENT UI)</a> を使用します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブのテーマを使用していないことを示す図" border="false":::

#### <a name="dont-hard-code-color-values"></a>いいえ: ハードコードの色の値

Teams のカラートークンを使用しない場合、設計のスケーラビリティが低下し、管理にかかる時間が長くなります。

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。

> [!div class="nextstepaction"]
> [設計検証ガイドラインの確認](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
