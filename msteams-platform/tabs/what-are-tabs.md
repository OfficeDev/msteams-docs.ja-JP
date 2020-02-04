---
title: Microsoft Teams のカスタムタブとは
author: laujan
description: Microsoft Teams プラットフォームのカスタムタブの概要
ms.topic: overview
ms.author: v-laujan
ms.openlocfilehash: 7560a9a7d19ca0182b2f5f45b304a96a0f2dddd4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675071"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>Microsoft Teams のカスタムタブとは

タブは、Microsoft Teams に組み込まれている Teams 対応の web ページです。 これらは、チーム内のチャネルの一部として、グループチャットに追加することも、個人用アプリとして個別のユーザー向けに追加することもできます。 アプリの一部として、カスタムタブを追加して Teams に独自の web コンテンツを埋め込んだり、 [teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client)を使用して web コンテンツに teams 固有の機能を追加したりすることができます。

> [!NOTE]
> Chrome 80 (初期2020でリリースが予定されています)。新しい cookie 値を紹介し、既定で cookie ポリシーを設定します。 既定のブラウザーの動作に依存するのではなく、cookie に対して使用する目的を設定することをお勧めします。 [SameSite cookie 属性 (2020 update)](../resources/samesite-cookie-update.md)を*参照してください*。

Teams チャネル/グループおよび personal で使用できるタブには2つの種類があります。 チャネル/グループタブでは、コンテンツをチャネルやグループのチャットに配信できます。また、専用の web ベースのコンテンツに関する共同作業スペースを作成するための優れた方法です。 個人用のタブは個人を対象とした bot と一緒に個人用アプリの一部であり、1人のユーザーに限定されます。 簡単にアクセスできるように、左側のナビゲーションバーにピン留めすることができます。

## <a name="tabs-user-scenarios"></a>タブのユーザーシナリオ

**シナリオ:** Teams 内に既存の web ベースのリソースを取り込む。 \
**例:** 情報提供の企業 web サイトをユーザーに提供する Teams アプリに [個人用] タブを作成します。

**シナリオ:** Teams の bot またはメッセージング拡張機能にサポートページを追加します。 \
**例:** について説明し、web ページのコンテンツをユーザーに提供する個人用タブを作成します。

**シナリオ:** 共同作業と共同作業のためにユーザーが定期的に操作するアイテムへのアクセスを提供します。 \
**例:** 各アイテムに詳細なリンクがある [チャネル/グループ] タブを作成します。

## <a name="how-do-tabs-work"></a>タブのしくみ

カスタムタブは、アプリパッケージのアプリマニフェストで宣言されています。 アプリのタブとして追加する web ページごとに、URL と範囲を定義します。 さらに、 [Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)をページに追加して、ページが読み`microsoftTeams.initialize()`込まれた後に呼び出す必要があります。 これにより、teams にページが表示されるようになり、teams 固有の情報 (たとえば、Teams クライアントが暗いテーマを実行している場合など) にアクセスできるようになり、結果に基づいてアクションを実行できるようになります。

チャネル/グループまたは個人のスコープ内でタブを表示するかどうかを選択した場合は、タブに IFramed 付き HTML[コンテンツページ](~/tabs/how-to/create-tab-pages/content-page.md)を表示する必要があります。個人用タブの場合、コンテンツ URL は、 `contentUrl` `staticTabs`配列内のプロパティによってマニフェストに直接設定されます。 タブの内容は、すべてのユーザーに対して同じになります。

[チャネル/グループ] タブでは、ユーザーがコンテンツページの URL を構成できる追加の構成ページも作成する必要があります。通常は、URL クエリ文字列パラメーターを使用して、そのコンテキストに適したコンテンツを読み込みます。 これは、[チャネル/グループ] タブを複数のチームまたはグループのチャットに追加できるためです。 以降の各インストールで、ユーザーはタブを構成して、必要に応じて操作を調整することができます。 たとえば、Azure DevOps ボードタブを追加すると、[構成] ページでタブが読み込まれるボードを選択できます。 構成ページの URL は、アプリマニフェスト`configurationUrl`内の`configurableTabs`配列のプロパティで指定されます。

アプリごとに最大16個の個人用タブを持つことができます (1) チャネル/グループタブの最大数は1つです。

## <a name="mobile-clients"></a>モバイル クライアント

Teams mobile クライアントに [チャネル/グループ] タブを表示する場合は、その`setSettings()` `websiteUrl`プロパティの値を設定する必要があります (以下を参照)。 個人用タブは現在、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。 モバイルクライアントでのタブの完全なサポートは、間もなくリリースされる予定です。 更新プログラムの準備をするには、タブを作成するときに[[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従ってください。
