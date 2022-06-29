---
title: 高度な UI コンポーネントを使用してアプリを設計する
author: heath-hamilton
description: 階層リンク、通知バー、ステージ ビューなどの Teams UI コンポーネントと関連するユース ケースについて説明します。
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: 30d429bf927b3cb9422fc4f3ea238ce9eceae49e
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485725"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>高度な UI コンポーネントを使用した Microsoft Teams アプリの設計

次のコンポーネントは、ナビゲーションなどの Teams の一般的な設計状況に使用できる [基本的な UI コンポーネント](~/concepts/design/design-teams-app-basic-ui-components.md) の組み合わせです。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

<a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a> に基づいて、Microsoft Teams UI Kit には、Teams アプリを構築するために特別に設計されたコンポーネントとパターンが含まれています。 UI キットでは、ここに示されているコンポーネントを直接デザインに取り込んで挿入し、各コンポーネントの使用方法の例をさらに確認できます。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Breadcrumb

階層リンクは、アプリの階層を伝えるナビゲーション支援です。 ユーザーは、表示しているページが全体的なエクスペリエンスにどのように適合しているかを理解し、その階層内の上位レベルへのワンクリック アクセスを提供するのに役立ちます。

### <a name="top-use-cases"></a>上位のユース ケース

* 階層の通信
* ナビゲーション

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="モバイルでの階層リンク テンプレートの例を示します。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="デスクトップ上の階層リンク テンプレートの例を示します。" border="false":::

## <a name="left-nav"></a>左ナビゲーション

左側のナビゲーションを使用して、[Teams] タブ内の複数のページを参照します。次の例では、左側のナビゲーションはチャネル リストとタブ コンテンツの間にあります。

### <a name="top-use-cases"></a>上位のユース ケース

* Teams タブ内の複数のページを参照します。
* 複雑なアプリを複数のページに分割します。

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="モバイル上の左側のナビゲーション テンプレートの例を示します。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="デスクトップ上の左側のナビゲーション テンプレートの例を示します。" border="false":::

## <a name="notification-bar"></a>通知バー

通知バーは、ユーザーがすぐにアクションを実行する必要のない、簡単で重要なメッセージを表示するための専用領域です。 特定の背景色とアイコンは、特定の種類のメッセージに関連付けられます (以下を参照)。

Fluent UI [アラート](https://fluentsite.z22.web.core.windows.net/0.59.0/components/alert/definition) コンポーネントを使用して通知バーを実装できます。

### <a name="top-use-cases"></a>上位のユース ケース

* 重大なメッセージ、エラー、および警告。
* 成功メッセージ
* 情報メッセージまたはプロモーション メッセージ

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="モバイル上の通知バー UI テンプレートの例を示します。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="デスクトップ上の通知バー UI テンプレートの例を示します。" border="false":::

## <a name="stage-view"></a>ステージ ビュー

ステージ ビューを使用すると、ユーザーはコンテキストを切り替えずに Teams の大きな画面にコンテンツ (画像、ファイル、Web サイトなど) を表示できます。 このコンポーネントは、主にコンテンツを表示するためのコンポーネントです。 複雑な対話には使用しないでください。

[ステージ ビュー](~/tabs/tabs-link-unfurling.md)を実装する方法について説明します。

### <a name="top-use-cases"></a>上位のユース ケース

* 別のアプリやブラウザーの代わりに、Teams 内の大きな画面にコンテンツを表示します。
* スポットライト メディアまたはその他のリッチ コンテンツ

### <a name="mobile"></a>Mobile

アプリは、アダプティブ カード、共有リンク、またはビジュアル コンポーネント (グラフなど) からステージを起動できます。

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="モバイルでのステージ テンプレートの例を示します。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="デスクトップ上のステージ テンプレートの例を示します。" border="false":::

## <a name="toolbar"></a>ツールバー

ツール バーは、一連のコントロールをグループ化するためのコンテナーです。

### <a name="top-use-cases"></a>上位のユース ケース

* アプリ コンテンツに対するコンテキスト アクション。
* コンテキスト フィルターと検索。
* ナビゲーションと階層リンク。

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="モバイル上のツール バー テンプレートの例を示します。" border="false":::

### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="デスクトップ上のツール バー テンプレートの例を示します。" border="false":::
