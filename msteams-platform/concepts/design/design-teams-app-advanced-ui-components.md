---
title: 高度な UI コンポーネントを使用してアプリを設計する
author: heath-hamilton
description: 各コンポーネントで使用される UI コンポーネントTeams。
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 6f2bd9cd237751adb15db45bbd6e3cdfea35ce09
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328080"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>高度な UI Microsoft Teamsを使用したアプリの設計

次のコンポーネントは、ナビゲーションなどの一[](~/concepts/design/design-teams-app-basic-ui-components.md)般的な設計状況で使用Teams UI コンポーネントの組み合わせです。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

UI に<a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>キットには、Microsoft Teamsアプリを構築するために特別に設計されたコンポーネントとTeamsがあります。 UI キットでは、ここに示すコンポーネントを直接デザインに挿入し、各コンポーネントの使い方の例を確認できます。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Breadcrumb

Breadcrumbs は、アプリの階層を伝えるナビゲーション支援です。 ユーザーは、表示しているページが全体的なエクスペリエンスに適合する方法を理解し、その階層内の上位レベルへの 1 回のクリックアクセスを許可するのに役立ちます。

### <a name="top-use-cases"></a>上位の使用例

* コミュニケーション階層
* ナビゲーション

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、デスクトップ上のパンくずテンプレートを示しています。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="例は、モバイル上のパンくずテンプレートを示しています。" border="false":::

---

## <a name="left-nav"></a>左ナビゲーション

左側のナビゲーションを使用して、[ページ] タブ内の複数Teamsします。次の例では、左側のナビゲーションはチャネル リストとタブ コンテンツの間にあります。

### <a name="top-use-cases"></a>上位の使用例

* [ページ] タブ内の複数Teams参照します。
* 複雑なアプリを複数のページに分割します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、デスクトップ上の左側のナビゲーション テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="例は、モバイル上の左ナビゲーション テンプレートを示しています。" border="false":::

---

## <a name="notification-bar"></a>通知バー

通知バーは、ユーザーが即座にアクションを実行する必要が生じない、簡潔で重要なメッセージを表示するための専用の領域です。 特定の背景色とアイコンは、特定の種類のメッセージに関連付けられる (以下を参照)。

### <a name="top-use-cases"></a>上位の使用例

* 重大なメッセージ、エラー、および警告
* 成功メッセージ
* 情報メッセージまたはプロモーション メッセージ

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、デスクトップ上の通知バーの UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="例では、モバイルの通知バー UI テンプレートを表示します。" border="false":::

---

## <a name="stage"></a>ステージ

ステージを使用すると、ユーザーはコンテキストを切り替えることなく、画像、ファイル、web サイトなど、コンテンツを大規模なTeams表示できます。 ステージは、主にコンテンツを表示する目的です。 複雑な対話にはステージを使用しない。

ステージを実装する方法について [学習します](~/tabs/tabs-link-unfurling.md)。

### <a name="top-use-cases"></a>上位の使用例

* 別のアプリまたはブラウザーではなく、Teams内の大きなサーフェスにコンテンツを表示する
* スポットライト メディアまたは他のリッチ コンテンツ

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="例は、デスクトップ上のステージ テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

アプリは、アダプティブ カード、共有リンク、またはビジュアル コンポーネント (グラフなど) からステージを起動できます。

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="例は、モバイル上のステージ テンプレートを示しています。" border="false":::

---

## <a name="toolbar"></a>ツール バー

ツールバーは、コントロールのセットをグループ化するコンテナーです。

### <a name="top-use-cases"></a>上位の使用例

* アプリ コンテンツに関するコンテキスト アクション
* コンテキスト フィルターと検索
* ナビゲーションとパンくず

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="例は、デスクトップ上のツール バー テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="例は、モバイルのツール バー テンプレートを示しています。" border="false":::

---
