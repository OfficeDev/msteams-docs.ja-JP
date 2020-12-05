---
title: Teams のカスタムタブとは
author: laujan
description: Teams プラットフォームのカスタムタブの概要
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: e89f07133f86b6c0700e6a71d8e53bf6d9831196
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576849"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>Microsoft Teams のカスタム タブとは

タブとは、Microsoft Teams に組み込まれている Teams 対応 Web ページです。 これらの \> タグは、アプリマニフェストで宣言されているドメインをポイントし、個々のユーザーのためにチーム、グループチャット、または個人用アプリの内部にあるチャネルの一部として追加できる、単純な HTML <iframe タグです。 ユーザー設定のタブをアプリに含めることにより、独自の web コンテンツを Teams に埋め込んだり、チーム固有の機能を web コンテンツに追加したりすることができます。 [Teams JavaScript client SDK](/javascript/api/overview/msteams-client) を参照してください。

> [!NOTE]
> Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../resources/samesite-cookie-update.md)」を *参照してください*。

Teams で使用できるタブには、チャネル/グループと個人の2種類があります。 チャネルまたはグループのタブは、チャネルとグループのチャットにコンテンツを配信し、専用の web ベースコンテンツの周囲に共同作業スペースを作成するための優れた方法です。 [個人] タブは、個人を対象としたボットと共に、個人用アプリの一部であり、1 人のユーザーを対象としています。 簡単にアクセスできるように、左側のナビゲーション バーにピン留めすることができます。

## <a name="lesser-known-tab-features"></a>あまり知られていないタブの機能

> [!div class="checklist"]
>
> * タブがボットも含まれるアプリに追加されると、ボットもチームに追加されます。
> * 現在のユーザーの Azure Active Directory (Azure AD) ID の認識。
> * `en-us` などの言語を示すユーザーのロケールを認識します。 
> * サポートされている場合は、シングルサインオン (SSO) 機能。
> * ボットやアプリの通知を使用して、タブや、個人の作業項目などのサービス内のサブ エンティティにディープ リンクできます。
> * タブ内のリンクからタスクモジュールを開く機能。
> * タブ内で SharePoint Web パーツを再利用できます。

## <a name="tabs-user-scenarios"></a>タブのユーザー シナリオ

**シナリオ:** Teams 内に既存の Web ベース リソースを取得します。 \
**例:** 情報提供企業の Web サイトをユーザーに提供する Teams アプリに [個人] タブを作成します。

**シナリオ:** Teams ボットまたはメッセージング拡張機能にサポート ページを追加します。 \
**例:***について* 説明し、web ページのコンテンツをユーザーに提供する個人用 *タブを作成* します。

**シナリオ:** 協力対話と共同作業のためにユーザーが定期的にやり取りするアイテムへのアクセスを提供します。 \
**例:** 個々のアイテムに詳細なリンクを設定した [チャネル/グループ] タブを作成します。

## <a name="how-do-tabs-work"></a>タブのしくみ

カスタム タブは、アプリ パッケージのアプリ マニフェストで宣言されます。 アプリ内のタブとして追加する web ページごとに、URL と範囲を定義します。 また、[Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) をページに追加して、ページの読み込みが終了したら `microsoftTeams.initialize()` を呼び出す必要があります。 これにより、teams にページが表示されるようになり、teams 固有の情報 (たとえば、Teams クライアントが *暗いテーマ* を実行している場合など) にアクセスできるようになり、結果に基づいてアクションを実行できるようになります。

チャネル/グループまたは個人のスコープ内でタブを公開するかどうかにかかわらず、 \> タブに <iframe HTML [コンテンツページ](~/tabs/how-to/create-tab-pages/content-page.md) を表示する必要があります。個人用タブの場合、コンテンツ URL は、配列内のプロパティによって Teams アプリマニフェストに直接設定され `contentUrl` `staticTabs` ます。 タブの内容は、すべてのユーザーに対して同じになります。

チャネルまたはグループのタブでは、ユーザーがコンテンツページの URL を構成できる追加の構成ページも作成する必要があります。通常は、URL クエリ文字列パラメーターを使用して、そのコンテキストに適したコンテンツを読み込みます。 これは、[チャネル/グループ] タブを複数のチームまたはグループ チャットに追加できるためです。 以降の各インストールでは、ユーザーはタブを構成できるようになり、必要に応じて操作を調整することができます。 ユーザーがタブを追加または構成すると、URL が Teams UI に表示されるタブに関連付けられます。 タブの構成は、その URL にさらにパラメーターを追加するだけです。 たとえば、[Azure ボード] タブを追加すると、[構成] ページで、タブがどのボードを読み込むかを選択できるようになります。 構成ページの URL は、アプリ マニフェストの `configurableTabs` 配列の `configurationUrl` プロパティで指定します。

1 つのアプリに対して、最大 1 つの [チャネル/グループ] タブと、最大 16 個の [個人] タブを設定できます。

## <a name="mobile-clients"></a>モバイル クライアント

Teams mobile クライアントに [チャネル/グループ] タブを表示する場合は、その `setSettings()` プロパティの値を設定する必要があり `websiteUrl` ます。 最適なユーザー環境を確保するには、タブを作成するときに [[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md) に従ってください。

> [!div class="nextstepaction"]
> [詳細情報: デバイスのアクセス許可を要求する](/concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
>[詳細情報: カメラとイメージギャラリーのアクセス許可](/concepts/device-capabilities/mobile-camera-image-permissions.md)