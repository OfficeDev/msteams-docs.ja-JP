---
title: Microsoft Teams のカスタム タブとは
author: laujan
description: Microsoft Teams プラットフォームでのカスタム タブの概要
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: f338387e658733981c16b36ed2a05c15132fc87c
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652062"
---
# <a name="what-are-tabs"></a>タブとは

タブを使用すると、web ベースのコンテンツを Teams に埋め込むことができます。 これは、アプリマニフェストで宣言されているドメインをポイントする単純な iframe で、チームチャネル、グループチャット、または個人用アプリの一部にすることができます。 **[Teams JavaScript client SDK](/javascript/api/overview/msteams-client) を参照してください。

> [!NOTE]
> Chrome 80 は新しい cookie 値を導入し、既定で cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../../resources/samesite-cookie-update.md)」を*参照してください*。

Teams には、[チャネル]、[グループ]、[個人用] タブという2種類のタブがあります。 チャネルまたはグループのタブでは、コンテンツをチャネルやグループのチャットに配信できます。また、専用の web ベースのコンテンツに関するコラボレーションスペースを作成するための優れた方法です。 個人用のタブは個人を対象とする bot と一緒に、個人のアプリの一部であり、1人のユーザーと対話するために使用されます。 簡単にアクセスできるように、左側のナビゲーション バーにピン留めすることができます。

## <a name="user-scenarios"></a>ユーザーのシナリオ

**シナリオ:** Teams 内に既存の Web ベース リソースを取得します。 \
**例:** 情報提供企業の Web サイトをユーザーに提供する Teams アプリに [個人] タブを作成します。

**シナリオ:** Teams ボットまたはメッセージング拡張機能にサポート ページを追加します。 \
**例:** 説明とヘルプの Web ページ コンテンツをユーザーに提供する [個人] タブを作成します。

**シナリオ:** 協力対話と共同作業のためにユーザーが定期的にやり取りするアイテムへのアクセスを提供します。 \
**例:** 個々のアイテムに詳細なリンクを設定した [チャネル/グループ] タブを作成します。

## <a name="how-do-tabs-work"></a>タブのしくみ

カスタム タブは、アプリ パッケージのアプリ マニフェストで宣言されます。 アプリのタブとして追加する Web ページごとに、URL と範囲を定義します。 また、[Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) をページに追加して、ページの読み込みが終了したら `microsoftTeams.initialize()` を呼び出す必要があります。 この操作を行うと、Teams にページが表示されるようになります。Teams 固有の情報 (たとえば、Teams クライアントが濃色テーマを実行している場合) にアクセスし、その結果に基づいてアクションを実行できるようになります。

[チャネル/グループ] または [個人] のスコープ内でタブを表示するかどうかを選択した場合は、タブに IFrame 付き HTML [コンテンツ ページ](~/tabs/how-to/create-tab-pages/content-page.md)を表示する必要があります。[個人] タブの場合、コンテンツ URL は、`staticTabs` 配列内の `contentUrl` プロパティによってマニフェストに直接設定されます。 タブの内容は、すべてのユーザーに対して同じになります。

[チャネル/グループ] タブの場合は、ユーザーがコンテンツ ページの URL を構成するための追加の構成ページも作成する必要があります。通常は、URL クエリ文字列パラメーターを使用して、そのコンテキストに適したコンテンツを読み込みます。 これは、[チャネル/グループ] タブを複数のチームまたはグループ チャットに追加できるためです。 以降にインストールが行われるたびに、ユーザーはタブを構成して、必要に応じて操作を調整することができます。 ユーザーがタブを追加するか、タブを構成すると、Teams UI に表示されているタブに URL が関連付けられます。 タブの構成は、その URL にさらにパラメーターを追加するだけです。 たとえば、[Azure DevOps ボード] タブを追加すると、構成ページで、タブにロードするボードを選択することができます。 構成ページの URL は、アプリ マニフェストの `configurableTabs` 配列の `configurationUrl` プロパティで指定します。

最大で1つのチャネル/グループタブ、およびアプリごとに最大16個の個人用タブを持つことができます。

## <a name="lesser-known-tab-features"></a>あまり知られていないタブ機能

* Bot があるアプリにタブが追加されると、その bot もチームに追加されます。
* 現在のユーザーの Azure Active Directory ID の認識。
* ユーザーが言語を示すロケールの認識 (例: `en-us` )。
* SSO 機能 (サポートされている場合)。
* Bot またはアプリの通知を、タブまたはサービス内のサブエンティティ (個別の作業項目など) へのディープリンクに使用できます。
* タブ内のリンクからタスク モジュールを開くことができます。
* タブで SharePoint web パーツを再利用します。

## <a name="tabs-on-mobile"></a>モバイルのタブ

Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。 [個人] タブは現在、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。 モバイル クライアントでのタブの完全なサポートは、間もなくリリースされる予定です。 更新プログラムの準備を行うには、タブの作成時に、[モバイルでのタブのガイダンス](~/tabs/design/tabs-mobile.md)に従ってください。

## <a name="learn-more"></a>詳細情報

* [アプリを計画する](../../concepts/extensibility-points.md)
* [アプリのビルド](../../concepts/building-an-app.md)
* [アプリの展開](../../concepts/deploy-and-publish/overview.md)
