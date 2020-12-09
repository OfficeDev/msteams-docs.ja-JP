---
title: 個人用アプリを設計する
description: Teams personal app を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605021"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Microsoft Teams 用の個人用アプリを設計する

個人アプリは、ボット、プライベートワークスペース、またはその両方にすることができます。 アプリが複数のチャネルのタブとして構成されている場合は、コンテンツを作成または表示する場所のような機能をユーザーに提供することもあります。

アプリの設計をガイドするには、次の情報を参照して、ユーザーが Teams で個人アプリを追加、使用、および管理する方法について説明します。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、アプリの総合的な設計ガイドラインを見つけることができます。 UI キットには、ここでは説明していないアクセシビリティや応答性の高いサイズ変更などの重要なトピックもあります。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>個人用アプリを追加する

Teams ストア (AppSource) またはアプリポップアップから個人用アプリを追加するには、Teams の左側にある [ **その他** ] アイコンを選択します (次の例を参照)。

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="例は、アプリのポップアップから個人用アプリを追加する方法を示しています。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a>個人用アプリを使用する (プライベートワークスペース)

プライベートワークスペースを使用すると、Teams を離れずに、中心となる場所で重要なアプリコンテンツを表示できます。

(実装メモ: プライベートワークスペースは、[ [*個人用] タブ*](../../build-your-first-app/build-personal-tab.md) の機能に基づいています。)

### <a name="anatomy-personal-app-private-workspace"></a>分析: 個人アプリ (プライベートワークスペース)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネントの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**アプリの属性**: アプリのロゴと名前。|
|B|**タブ**: 個人用アプリのナビゲーションを提供します。 たとえば、[ **バージョン情報** ] タブまたは [ **ヘルプ** ] タブを含めます。|
|C|**Popout view**: アプリのコンテンツを親ウィンドウからスタンドアロンの子ウィンドウにプッシュします。|
|D|**[その他のメニュー]**: 追加のアプリ情報とオプションが含まれています。 (または、タブを **設定** することもできます)。|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造の構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**タブ**: 個人用アプリのナビゲーションを提供します。|
|1 |**iframe**: アプリのコンテンツを表示します。|

### <a name="designing-with-ui-templates"></a>UI テンプレートを使用して設計する

次の Teams UI テンプレートのいずれかを使用して、[個人用] タブの設計に役立てることができます。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [タスクボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。
* [Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。
* [左](../../concepts/design/design-teams-app-ui-templates.md#left-nav)ナビゲーション: タブにいくつかのナビゲーションが必要な場合は、左側のナビゲーションテンプレートが役立ちます。 一般的に、タブナビゲーションは最小限にする必要があります。

## <a name="use-a-personal-app-bot"></a>個人アプリ (bot) を使用する

個人用アプリには、1対1の会話およびプライベート通知用の bot を含めることができます (たとえば、同僚がアートボードにコメントを投稿した場合)。 Bot は、指定したタブで使用できます。

### <a name="anatomy-personal-app-bot"></a>分析: Personal app (bot)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="例は、パーソナル bot コンポーネントの分析を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**Bot タブ**: たとえば、ボット会話や通知にアクセスするための [ **チャット** ] タブを含みます。|
|B|**Bot メッセージ**: bot は、メッセージと通知をカード (アダプティブカードなど) 形式で送信することがよくあります。|
|C|**新規作成ボックス**: bot にメッセージを送信するための入力フィールド。|

## <a name="best-practices"></a>ベスト プラクティス

### <a name="tab-priority"></a>タブの優先度

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>実行: 最初のタブに最も関連のあるコンテンツを表示する

応答性の高いサイズに設定すると、右側のタブが切り捨てられるか、表示されなくなることがあります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>いいえ: セカンダリコンテンツまたはメタデータをリードします。

標準的な web アプリと同様に、タブナビゲーションは、アプリの主要な機能を理解するために役立つ順序で実行する必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="tab-hierarchy"></a>タブ階層

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Do: タブを同じ階層にして、主要なアプリページを表す必要があります。

タブでは、アプリの主要な機能とコンテンツを分類する必要があります。 応答性の高いサイズに設定すると、右側のコンテンツが切り捨てられるか、表示されなくなることがあります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>異なる階層のレベルを含めないでください。

コンテンツは、ユーザーが理解しやすくなる論理的な順序で実行する必要があります。 互いに密接な関係がある2つのタブがある場合は、1つのタブに結合することを検討してください。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="first-run-experience"></a>初回実行時エクスペリエンス

#### <a name="do-include-a-first-run-experience"></a>実行: 最初の実行環境を含める

個人用アプリを初めて使用するときは、少なくともようこそ画面が表示されている必要があります。 Bot の場合は、bot が実行できることを説明し、サインインボタンなどのクイック操作を提供します。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>いいえ: 空の画面で開始します

アプリを初めて実行したときに何も表示されない場合は、ユーザーが混乱する可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="personalized-content"></a>個人用コンテンツ

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Do: ユーザーに関連するアプリコンテンツを集計する

個人のタブか bot かにかかわらず、アプリ内のユーザーのアクティビティのみに関連するコンテンツが表示されます。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>[しない]: 関連性のないコンテンツまたは過度に広いコンテンツを表示する

個人コンテキストでは、ユーザーが所属していない teams のコンテンツは表示されません。 個人 bot コンテンツは、グループではなく個人に焦点を当てる必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="complex-app-features"></a>複雑なアプリ機能

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do: ブラウザーで複雑な機能にアクセスすることをユーザーに許可する

アプリは Teams のコアタスクに焦点を当てる必要がありますが、完全なスタンドアロンアプリをブラウザーで表示することもできます。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-include-your-entire-app"></a>アプリ全体を含めないでください。

特に Teams 用のアプリを作成していない場合は、コラボレーションツールで意味を持たない機能が存在する可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

## <a name="manage-a-personal-tab"></a>個人用タブを管理する

Teams の左側で、ユーザーは個人用アプリを右クリックして、他のアプリオプションを固定、削除、および構成できます。

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="例は、個人用アプリを管理するためのオプションを示しています。" border="false":::

## <a name="learn-more"></a>詳細情報

個人アプリの範囲によっては、次のような設計ガイドラインが役になることがあります。

* [タブのデザイン](../../tabs/design/tabs.md)
* [Bot のデザイン](../../bots/design/bots.md)

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。

> [!div class="nextstepaction"]
> [設計検証ガイドラインの確認](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
