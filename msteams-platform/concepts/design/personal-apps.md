---
title: 個人用アプリをデザインする
description: 個人用アプリを設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b3f08c39a7900b80fb46d167fae8d9e8bdbcc574
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101556"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>アプリの個人用アプリを設計Microsoft Teams

個人用アプリには、ボット、プライベート ワークスペース、または両方を指定できます。 コンテンツを作成または表示する場所のように機能する場合や、アプリが複数のチャネルのタブとして構成されている場合に、ユーザーが自分のコンテンツを一目で見る場合があります。

アプリの設計をガイドするために、次の情報は、ユーザーがアプリで個人用アプリを追加、使用、および管理する方法をTeams。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、包括的な個人用アプリ設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。 UI キットには、ここでは説明しないアクセシビリティや応答性のサイジングなどの重要なトピックも含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>個人用アプリを追加する

Teams ストア (AppSource) またはアプリ のフライアウトから個人用アプリを追加するには、Teams の左側にある [その他] アイコンを選択します (次の例を参照)。

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="例は、アプリのフライアウトから個人用アプリを追加する方法を示しています。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a>個人用アプリを使用する (プライベート ワークスペース)

プライベート ワークスペースを使用すると、アプリのコンテンツを一か国間で表示することなく、一Teams。

(実装ノート: プライベート ワークスペースは個人用タブ [*機能に基づいて作成*](../../build-your-first-app/build-personal-tab.md) されます)。

### <a name="anatomy-personal-app-private-workspace"></a>Anatomy: 個人用アプリ (プライベート ワークスペース)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネント構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**アプリの属性**: アプリのロゴと名前。|
|B|**タブ**: 個人用アプリのナビゲーションを提供します。 たとえば、[概要] タブまたは **[ヘルプ]** タブ **を含** めることができます。|
|C|**Popout ビュー**: 親ウィンドウからスタンドアロンの子ウィンドウにアプリコンテンツをプッシュします。|
|D|**[その他]** メニュー: 追加のアプリ情報とオプションが含まれます。 (代わりに、タブ **設定** することもできます)。|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**タブ**: 個人用アプリのナビゲーションを提供します。|
|1|**iframe**: アプリのコンテンツを表示します。|

### <a name="designing-with-ui-templates"></a>UI テンプレートを使用した設計

個人用タブを設計するには、次Teams UI テンプレートのいずれかを使用します。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。 一般に、タブ ナビゲーションは最小限に抑えます。

## <a name="use-a-personal-app-bot"></a>個人用アプリ (ボット) の使用

個人用アプリには、1 対 1 の会話とプライベート通知用のボットを含めできます (たとえば、同僚がアートボードにコメントを投稿する場合など)。 ボットは、指定したタブで使用できます。

### <a name="anatomy-personal-app-bot"></a>解剖学: 個人用アプリ (ボット)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="例は、個人用ボット コンポーネントの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**[ボット]** タブ: たとえば、[チャット] タブ **を含** め、ボットの会話と通知にアクセスします。|
|B|**ボット メッセージ**: ボットは、多くの場合、メッセージや通知をカード (アダプティブ カードなど) の形式で送信します。|
|C|**[作成]** ボックス : ボットにメッセージを送信する入力フィールド。|

## <a name="manage-a-personal-tab"></a>個人用タブの管理

ユーザーは、アプリのTeamsを右クリックして、他のアプリ オプションをピン留め、削除、構成できます。

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="例では、個人用アプリを管理するためのオプションを示します。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="tab-priority"></a>タブの優先度

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Do: 最初のタブに最も関連性の高いコンテンツを表示する

応答性の高いサイズ設定では、右側のタブが切り捨てられたり、見えなくなる場合があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="例は、最初のタブで最も関連性の高いコンテンツを表示する個人用アプリを示しています。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>[しない] セカンダリ コンテンツまたはメタデータを含むリード

標準の Web アプリと同様に、タブ ナビゲーションはアプリの主な機能を意味する順序で進む必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="例は、セカンダリ コンテンツまたはメタデータを先頭に個人アプリを示しています。" border="false":::

### <a name="tab-hierarchy"></a>タブ階層

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Do: タブは等しい階層で、主要なアプリ ページを表す必要があります

タブは、アプリの主な機能とコンテンツを分類する必要があります。 応答性の高いサイズ設定では、右側のコンテンツが切り捨てられたり、見えなくなる可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="例は、同じ階層のタブを持つ個人用アプリを示しています。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>[しない]: 階層の異なるレベルを含める

コンテンツは論理的な順序で進行し、ユーザーが意味を持つ必要があります。 密接に関連する 2 つのタブがある場合は、それらを 1 つのタブに組み合わせることを検討してください。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="例では、階層レベルが異なる個人用アプリを示します。" border="false":::

### <a name="first-run-experience"></a>初回実行時エクスペリエンス

#### <a name="do-include-a-first-run-experience"></a>Do: 初回実行エクスペリエンスを含める

個人用アプリを初めて使用する場合は、少なくともウェルカム 画面が表示される必要があります。 ボットの場合は、ボットが実行できる操作を説明し、サインイン ボタンなどのクイック アクションを提供します。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="例は、個人用アプリの初回実行時の操作を示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="別の例は、個人用アプリの初回実行時の操作を示しています。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>[しない]: 空白の画面から開始する

ユーザーがアプリを初めて実行した時に何も表示しない場合、ユーザーは混乱する可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="例は、個人用アプリの初回実行時に実行しない操作を示しています。" border="false":::

### <a name="personalized-content"></a>パーソナライズされたコンテンツ

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Do: ユーザーに関連するアプリ コンテンツを集約する

個人用タブでもボットでも、アプリ内のユーザーのアクティビティにのみ関連するコンテンツを表示します。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="例では、個人用アプリと個人用コンテンツを操作する方法を示します。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="別の例は、個人用アプリと個人用コンテンツを操作する方法を示しています。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>[しない]: 関連のないコンテンツまたは広いコンテンツを表示する

個人のコンテキストでは、ユーザーが参加しないチームのコンテンツを表示しない。 個人用ボットのコンテンツは、グループではなく、個人に焦点を当てる必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="例は、個人用アプリと個人用設定されたコンテンツで何をしないかを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="別の例は、個人用アプリと個人用コンテンツを使用しない方法を示しています。" border="false":::

### <a name="complex-app-features"></a>複雑なアプリ機能

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do: ユーザーがブラウザーの複雑な機能にアクセスするを許可する

アプリは、Teamsのコア タスクに集中する必要がありますが、完全なスタンドアロン アプリはブラウザーで表示できます。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理する方法を示しています。" border="false":::

#### <a name="dont-include-your-entire-app"></a>[しない]: アプリ全体を含める

アプリを特別に作成しない限り、Teamsツールでは意味のない機能を使用している可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理しない方法を示しています。" border="false":::

## <a name="see-also"></a>関連項目

これらの他の設計ガイドラインは、個人用アプリの範囲に応じて役立つ場合があります。

* [タブの設計](../../tabs/design/tabs.md)
* [ボットの設計](../../bots/design/bots.md)
