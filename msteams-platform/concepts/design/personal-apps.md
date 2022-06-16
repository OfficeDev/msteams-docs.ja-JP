---
title: 個人用アプリをデザインする
description: Teams 個人用アプリを設計して Microsoft Teams UI キットを入手する方法、ダッシュボード、フォーム、モバイルおよびデスクトップ エクスペリエンス用のタスク ボードなどのコンポーネントを作成する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
keywords: UI キット個人用アプリ ウェブビュー ナビゲーション ボット タブ iframe ダッシュボード フォーム テンプレート
ms.openlocfilehash: fe22f63ec3bf93011f3acebd8f1269496e8444e5
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123928"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Microsoft Teams の個人用アプリの設計

個人用アプリは、ボット、プライベート ワークスペース、またはその両方にすることができます。 コンテンツを作成または表示する場所のように機能する場合もあれば、アプリが複数のチャネルのタブとして構成されている場合に、ユーザーが自分のものすべてを一目で確認できる場合もあります。

アプリのデザインに役立てるために、次の情報では、Teams でユーザーがどのように個人用アプリを追加、使用、管理できるかを説明、図解しています。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットには、必要に応じて取得および変更できる要素を含む、包括的な個人用アプリ設計ガイドラインがあります。 UI キットには、アクセシビリティやレスポンシブ サイズ設定など、ここでは取り上げていない重要なトピックも含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI キット (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>個人用アプリの追加

ユーザーは、Teams の左側にある **[その他]** アイコン (次の例を参照) を選択して、Teams ストアまたはアプリ フライアウトから個人用アプリを追加できます。

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="例は、フライアウト アプリから個人用アプリを追加する方法を示しています。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a>個人用アプリを使用する (プライベート ワークスペース)

プライベート ワークスペースを使用すると、ユーザーは Teams を離れることなく、自分にとって意味のあるアプリ コンテンツを中央の場所に表示できます。

(実装上の注意: プライベート ワークスペースは、[*個人用タブ*](../../tabs/how-to/create-personal-tab.md)機能に基づいています。)

### <a name="anatomy-personal-app-private-workspace"></a>構造: 個人用アプリ (プライベート ワークスペース)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネントの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**アプリ属性**: アプリ名。|
|B|**タブ**: 個人用アプリのナビゲーションを提供します。|
|C|**その他のメニュー**: アプリのその他のオプションと情報が含まれています。|
|D|**プライマリ ナビゲーション**: アプリのその他の主要な Teams 機能へのナビゲーションを提供します。|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**タブ**: 個人用アプリのナビゲーションを提供します。|
|1|**webview**: アプリのコンテンツを表示します。|

#### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="この例は、個人用タブのコンポーネントの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**アプリの属性**: アプリのロゴと名前。|
|B|**タブ**: 個人用アプリのナビゲーションを提供します。|
|C|**ポップアウト ビュー**: アプリのコンテンツを親ウィンドウからスタンドアロンの子ウィンドウにプッシュします。|
|D|**その他のメニュー**: アプリのその他のオプションと情報が含まれています。 (または、**[設定]** をタブにすることもできます。)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="この例は、個人用タブの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**タブ**: 個人用アプリのナビゲーションを提供します。|
|1|**iframe**: アプリのコンテンツを表示します。|

### <a name="design-with-ui-templates-and-advanced-components"></a>UI テンプレートと高度なコンポーネントを使用して設計する

次の Teams テンプレートとコンポーネントのいずれかを使用して、個人用タブの設計に役立ててください。

* [リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。
* [タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): かんばんボードまたはスイム レーンと呼ばれることもあるタスク ボードは、作業項目またはチケットのステータスを追跡するためによく使用されるカードのコレクションです。
* [ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。
* [フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。
* [空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、最初の実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。
* [左ナビゲーション](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 個人用アプリにナビゲーションが必要な場合は、左側のナビゲーション コンポーネントが役立ちます。 一般に、タブ ナビゲーションは最小限に抑える必要があります。

## <a name="use-a-personal-app-bot"></a>個人用アプリを使用する (ボット)

個人用アプリには、1 対 1 の会話やプライベート通知 (たとえば、同僚がアートボードにコメントを投稿した場合) 用のボットを含めることができます。 ユーザーは、指定したタブでボットを操作します。

### <a name="anatomy-personal-app-bot"></a>構造: 個人用アプリ (ボット)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="例は、個人用ボットのコンポーネントの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**ボットのエントリ ポイント**: ユーザーが個人用アプリのボット機能にアクセスするためのエントリ ポイント。|
|B|**[戻る] ボタン**: ユーザーをプライベート ワークスペースに戻します。|
|C|**ボット メッセージ**: ボットは、多くの場合、カード (アダプティブ カードなど) の形式でメッセージと通知を送信します。|
|D|**[作成] ボックス**: メッセージをボットに送信するための入力フィールド。|

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="例は、個人用ボット コンポーネントの構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**[ボット] タブ**: たとえば、ボットの会話と通知にアクセスするための **[チャット]** タブを含めます。|
|B|**ボット メッセージ**: ボットは、多くの場合、カード (アダプティブ カードなど) の形式でメッセージと通知を送信します。|
|C|**[作成] ボックス**: メッセージをボットに送信するための入力フィールド。|

## <a name="manage-a-personal-tab"></a>個人用タブを管理する

Teams の左側で、ユーザーは個人用アプリを右クリックして、他のアプリ オプションを固定、削除、および構成できます。

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="例は、個人用アプリを管理するためのオプションを示しています。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="tab-priority"></a>タブの優先度

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>実行する: 最初のタブに最も関連性の高いコンテンツを表示する

レスポンシブ サイズ設定では、右側のタブが切り捨てられたり、表示されなくなったりする場合があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="例は、最初のタブに最も関連性の高いコンテンツを表示する個人用アプリを示しています。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>実行しない: セカンダリ コンテンツまたはメタデータでリードする

標準の Web アプリと同様に、タブ ナビゲーションは、アプリの主な機能を理解しやすい順序で実行する必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="例は、セカンダリ コンテンツまたはメタデータでリードする個人用アプリを示しています。" border="false":::

### <a name="tab-hierarchy"></a>タブ階層

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>実行する: タブは同じ階層であり、主要なアプリ ページを表す必要があります

タブは、アプリの主な機能とコンテンツを分類する必要があります。 レスポンシブ サイズ設定では、右側のコンテンツが切り捨てられたり、表示されなくなったりする場合があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="例は、同じ階層のタブを持つ個人用アプリを示しています。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>実行しない: さまざまなレベルの階層を含める

コンテンツは、ユーザーが理解しやすい論理的な順序で実行する必要があります。 密接に関連する 2 つのタブがある場合は、それらを 1 つのタブに結合することを検討してください。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="例は、階層のレベルが異なる個人用アプリを示しています。" border="false":::

### <a name="first-run-experience"></a>初回実行時エクスペリエンス

#### <a name="do-include-a-first-run-experience"></a>実行する: 初回実行エクスペリエンスを含める

個人用アプリを初めて使用するときは、少なくともウェルカム画面が表示されているはずです。 ボットの場合、ボットが実行できることを説明し、サインイン ボタンなどの迅速なアクションを提供します。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="例は、個人用アプリの初回実行エクスペリエンスで何をするかを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="別の例は、個人用アプリの初回実行エクスペリエンスで何をするかを示しています。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>実行しない: 空白の画面から開始する

アプリを初めて実行したときに何も表示されない場合、ユーザーは混乱する可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="例は、個人用アプリの初回実行エクスペリエンスで何をしないかを示しています。" border="false":::

### <a name="personalized-content"></a>パーソナライズされたコンテンツ

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>実行する: ユーザーに関連するアプリ コンテンツを集約する

個人用タブであろうとボットであろうと、アプリ内のユーザーのアクティビティのみに関連するコンテンツを表示します。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="例は、個人用アプリとパーソナライズされたコンテンツで何をするかを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="別の例は、個人用アプリとパーソナライズされたコンテンツで何をするかを示しています。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>実行しない: 無関係または過度に広いコンテンツを表示する

個人用コンテキストでは、ユーザーが参加していないチームのコンテンツを表示しないでください。 個人用ボットのコンテンツは、グループではなく個人に焦点を当てる必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="例は、個人用アプリとパーソナライズされたコンテンツで何をしないかを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="別の例は、個人用アプリとパーソナライズされたコンテンツで何をしないかを示しています。" border="false":::

### <a name="complex-app-features"></a>複雑なアプリ機能

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>実行する: ユーザーがブラウザーの複雑な機能にアクセスできるようにする

アプリは Teams のコア タスクに重点を置く必要がありますが、ブラウザーで完全なスタンドアロン アプリを表示することはできます。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理する方法を示しています。" border="false":::

#### <a name="dont-include-your-entire-app"></a>実行しない: アプリ全体を含める

Teams 専用のアプリを作成していない限り、コラボレーション ツールでは意味をなさない機能がある可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理しない方法を示しています。" border="false":::

## <a name="see-also"></a>関連項目

個人用アプリの範囲によっては、次の他の設計ガイドラインが役立つ場合があります。

* [タブの設計](../../tabs/design/tabs.md)
* [ボットの設計](../../bots/design/bots.md)
