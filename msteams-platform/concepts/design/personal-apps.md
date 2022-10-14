---
title: 個人用アプリをデザインする
description: Microsoft Teams UI キットを使用して個人用アプリを設計するための UI 要素を含む設計ガイドラインを実装する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 4646d47c5aa325291f060ea192dcc1705b414ac7
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575797"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Microsoft Teams の個人用アプリの設計

個人用アプリは、ボット、プライベート ワークスペース、またはその両方にすることができます。 コンテンツを作成または表示する場所として機能する場合があります。 それ以外の場合は、アプリが複数のチャネルのタブとして構成されている場合に、ユーザーが自分の物であるすべてのものを鳥の目で見るビューをユーザーに提供します。

アプリのデザインに役立てるために、次の情報では、Teams でユーザーがどのように個人用アプリを追加、使用、管理できるかを説明、図解しています。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットには、必要に応じて取得および変更できる要素を含む、包括的な個人用アプリ設計ガイドラインがあります。 UI キットには、アクセシビリティやレスポンシブ サイズ設定など、ここでは取り上げていない重要なトピックも含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI キット (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>個人用アプリの追加

ユーザーは、Teams の左側にある **[その他]** アイコン (次の例を参照) を選択して、Teams ストアまたはアプリ フライアウトから個人用アプリを追加できます。

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="例は、フライアウト アプリから個人用アプリを追加する方法を示しています。":::

## <a name="use-a-personal-app-private-workspace"></a>個人用アプリを使用する (プライベート ワークスペース)

プライベート ワークスペースを使用すると、ユーザーは Teams を離れることなく、自分にとって意味のあるアプリ コンテンツを中央の場所に表示できます。

(実装上の注意: プライベート ワークスペースは、[*個人用タブ*](../../tabs/how-to/create-personal-tab.md)機能に基づいています。)

### <a name="anatomy-personal-app-private-workspace"></a>構造: 個人用アプリ (プライベート ワークスペース)

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネントの構造を示しています。":::

|カウンター|説明|
|----------|-----------|
|A|**アプリ属性**: アプリ名。|
|B|**タブ**: 個人用アプリのナビゲーションを提供します。|
|C|**その他のメニュー**: その他のアプリのオプションと情報が含まれています。|
|D|**プライマリ ナビゲーション**: アプリのその他の主要な Teams 機能へのナビゲーションを提供します。|

#### <a name="configure-and-add-multiple-actions-in-navbar"></a>**NavBar で複数のアクションを構成して追加する**

右上のナビゲーション バーに複数のアクションを追加し、アプリ内の追加アクション用のオーバーフロー メニューを作成できます。

>[!NOTE]
> オーバーフロー メニューを含め、ナビゲーション バーに最大 5 つのアクションを追加できます。

:::image type="content" source="../../assets/images/overflow-menu-and-multiple-actionsoptions.png" alt-text="スクリーンショットは、ナビゲーション バーとオーバーフロー メニューを示す例です。":::

**NavBar で複数のアクションを構成して追加** するには、[setNavBarMenu](/javascript/api/@microsoft/teams-js/microsoftteams.menus?view=msteams-client-js-1.12.1&preserve-view=true) API を呼び出します。 にプロパティ`MenuItem`を追加します`displayMode enum`。 ナビゲーション `displayMode enum` バーにメニューを表示する方法を定義します。 既定値 `displayMode enum` は `ifRoom`.

NavBar で使用可能な要件と領域に基づいて、次のいずれかを考慮して設定 `displayMode enum` します。

* 空きがある場合は、NavBar にアイテムを配置するように設定 `ifRoom = 0` します。
* 空きがない場合は、その項目は常に NavBar のオーバーフロー メニューに配置されますが、NavBar には配置されないように設定 `overflowOnly = 1`します。

複数のアクションのオーバーフロー メニューを使用して NavBar を構成する例を次に示します。

```typescript
const menuItems = [item1, item2, item3, item4, item5]
microsoftTeams.menus.setNavBarMenu(menuItems, (id: string) => {
  output(`Clicked ${id}`)
  return true;
})
```

> [!NOTE]
> API では `setNavBarMenu` 、[ **更新]** ボタンは制御されません。 既定で表示されます。

:::image type="content" source="../../assets/images/overflow-menu-and-multple-actions.png" alt-text="スクリーンショットは、オーバーフロー メニューのナビゲーション バーと複数のアクションを示す例です。":::

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造を示しています。":::

|カウンター|説明|
|----------|-----------|
|A|**タブ**: 個人用アプリのナビゲーションを提供します。|
|1|**webview**: アプリのコンテンツを表示します。|

#### <a name="desktop"></a>デスクトップ

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="この例は、個人用タブのコンポーネントの構造を示しています。":::

|カウンター|説明|
|----------|-----------|
|A|**アプリの属性**: アプリのロゴと名前。|
|B|**タブ**: 個人用アプリのナビゲーションを提供します。|
|C|**ポップアウト ビュー**: アプリのコンテンツを親ウィンドウからスタンドアロンの子ウィンドウにプッシュします。|
|D|**その他のメニュー**: その他のアプリのオプションと情報が含まれています。 (または、**[設定]** をタブにすることもできます。)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="この例は、個人用タブの構造を示しています。":::

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

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="例は、個人用ボットのコンポーネントの構造を示しています。":::

|カウンター|説明|
|----------|-----------|
|A|**ボットのエントリ ポイント**: ユーザーが個人用アプリのボット機能にアクセスするためのエントリ ポイント。|
|B|**[戻る] ボタン**: ユーザーをプライベート ワークスペースに戻します。|
|C|**ボット メッセージ**: ボットは、多くの場合、カード (アダプティブ カードなど) の形式でメッセージと通知を送信します。|
|D|**[作成] ボックス**: メッセージをボットに送信するための入力フィールド。|

#### <a name="configure-back-button"></a>[戻る構成] ボタン

Teams アプリで [戻る] ボタンを選択すると、アプリ内を移動せずに Teams プラットフォームに戻ります。

アプリ内を移動するには、[戻る] ボタンを構成して、[戻る] ボタンを選択すると、前の手順に戻ってアプリ内を移動できます。

**戻るボタンを構成** するには、次のいずれかの条件に応じて戻るボタンの機能を処理する [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true) API を呼び出します。

* に`false`設定すると`registerBackButtonHandler`、JavaScript SDK によって API が`navigateBack`呼び出され、Teams プラットフォームが戻るボタンを処理します。
* に`true`設定すると`registerBackButtonHandler`、アプリは戻るボタンの機能を処理し (前の手順に戻ってアプリ内を移動できます)、Teams プラットフォームはそれ以上のアクションを実行しません。

戻るボタンを構成する例を次に示します。

```typescript
microsoftTeams.registerBackButtonHandler(() => {
  const selectOption = registerBackReturn.options[registerBackReturn.selectedIndex].value
  var isHandled = false
  if (selectOption == 'true') 
    isHandled = true;
  output(`onBack isHandled ${isHandled}`)
  return isHandled;
})
```

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="例は、個人用ボット コンポーネントの構造を示しています。":::

|カウンター|説明|
|----------|-----------|
|A|**[ボット] タブ**: たとえば、ボットの会話と通知にアクセスするための **[チャット]** タブを含めます。|
|B|**ボット メッセージ**: ボットは、多くの場合、カード (アダプティブ カードなど) の形式でメッセージと通知を送信します。|
|C|**[作成] ボックス**: メッセージをボットに送信するための入力フィールド。|

## <a name="manage-a-personal-tab"></a>個人用タブを管理する

Teams の左側で、ユーザーは個人用アプリを右クリックして、他のアプリ オプションを固定、削除、および構成できます。

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="例は、個人用アプリを管理するためのオプションを示しています。":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="tab-priority"></a>タブの優先度

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>実行する: 最初のタブに最も関連性の高いコンテンツを表示する

レスポンシブ サイズ設定では、右側のタブが切り捨てられたり、表示されなくなったりする場合があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="例は、最初のタブに最も関連性の高いコンテンツを表示する個人用アプリを示しています。":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>実行しない: セカンダリ コンテンツまたはメタデータでリードする

標準の Web アプリと同様に、タブ ナビゲーションは、アプリの主な機能を理解しやすい順序で実行する必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="例は、セカンダリ コンテンツまたはメタデータでリードする個人用アプリを示しています。":::

### <a name="tab-hierarchy"></a>タブ階層

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>実行する: タブは同じ階層であり、主要なアプリ ページを表す必要があります

タブは、アプリの主な機能とコンテンツを分類する必要があります。 レスポンシブ サイズ設定では、右側のコンテンツが切り捨てられたり、表示されなくなったりする場合があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="例は、同じ階層のタブを持つ個人用アプリを示しています。":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>実行しない: さまざまなレベルの階層を含める

コンテンツは、ユーザーが理解しやすい論理的な順序で実行する必要があります。 密接に関連する 2 つのタブがある場合は、それらを 1 つのタブに結合することを検討してください。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="例は、階層のレベルが異なる個人用アプリを示しています。":::

### <a name="first-run-experience"></a>初回実行時エクスペリエンス

#### <a name="do-include-a-first-run-experience"></a>実行する: 初回実行エクスペリエンスを含める

個人用アプリを初めて使用するときは、少なくともウェルカム画面が表示されているはずです。 ボットの場合、ボットが実行できることを説明し、サインイン ボタンなどの迅速なアクションを提供します。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="例は、個人用アプリの初回実行エクスペリエンスで何をするかを示しています。":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="別の例は、個人用アプリの初回実行エクスペリエンスで何をするかを示しています。":::

#### <a name="dont-start-with-a-blank-screen"></a>実行しない: 空白の画面から開始する

アプリを初めて実行したときに何も表示されない場合、ユーザーは混乱する可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="例は、個人用アプリの初回実行エクスペリエンスで何をしないかを示しています。":::

### <a name="personalized-content"></a>パーソナライズされたコンテンツ

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>実行する: ユーザーに関連するアプリ コンテンツを集約する

個人用タブであろうとボットであろうと、アプリ内のユーザーのアクティビティのみに関連するコンテンツを表示します。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="例は、個人用アプリとパーソナライズされたコンテンツで何をするかを示しています。":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="別の例は、個人用アプリとパーソナライズされたコンテンツで何をするかを示しています。":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>実行しない: 無関係または過度に広いコンテンツを表示する

個人用コンテキストでは、ユーザーが参加していないチームのコンテンツを表示しないでください。 個人用ボットのコンテンツは、グループではなく個人に焦点を当てる必要があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="例は、個人用アプリとパーソナライズされたコンテンツで何をしないかを示しています。":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="別の例は、個人用アプリとパーソナライズされたコンテンツで何をしないかを示しています。":::

### <a name="complex-app-features"></a>複雑なアプリ機能

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>実行する: ユーザーがブラウザーの複雑な機能にアクセスできるようにする

アプリは Teams のコア タスクに重点を置く必要がありますが、ブラウザーで完全なスタンドアロン アプリを表示することはできます。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理する方法を示しています。":::

#### <a name="dont-include-your-entire-app"></a>実行しない: アプリ全体を含める

Teams 専用のアプリを作成していない限り、コラボレーション ツールでは意味をなさない機能がある可能性があります。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理しない方法を示しています。":::

## <a name="see-also"></a>関連項目

個人用アプリの範囲によっては、次の他の設計ガイドラインが役立つ場合があります。

* [タブの設計](../../tabs/design/tabs.md)
* [ボットをデザインする](../../bots/design/bots.md)
* [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true)
* [DisplayMode 列挙型](/javascript/api/@microsoft/teams-js/menus.displaymode?view=msteams-client-js-latest&preserve-view=true)
