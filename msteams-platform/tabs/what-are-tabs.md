---
title: Microsoft Teams のタブ
author: surbhigupta
description: Teams プラットフォームでのカスタム タブの概要
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 6f18760670f81bea0e0c2bad6da9f15bd1982f0f
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2021
ms.locfileid: "60719841"
---
# <a name="microsoft-teams-tabs"></a>Microsoft Teams のタブ

タブとは、Microsoft Teams に組み込まれている Teams 対応 Web ページです。 これらは簡単な HTML <iFrame \> タブで、アプリ マニフェストで宣言されたドメインを指していて、チーム内のチャネル、グループ チャット、または個々のユーザー用の個人用アプリとして追加できます。 アプリにカスタム タブを含めて独自の Web コンテンツを Teams に埋め込んだり、Teams 固有の機能を Web コンテンツに追加したりできます。 詳細については[、「JavaScript クライアント SDK Teamsを参照してください](/javascript/api/overview/msteams-client)。

> [!IMPORTANT]
> 現在、カスタム タブは、Government Community Cloud (GCC)、GCC-High、および国防総省 (DOD) で使用できます。

次の図は、個人用タブを示しています。

![[個人] タブ](../assets/images/tabs/personaltab.png)

次の図は、Contoso チャネル タブを示しています。

![チャネルまたはグループのタブ](../assets/images/tabs/tabs.png)

> [!VIDEO https://www.youtube-nocookie.com/embed/Jw6i7Mkt0dg]


> [!VIDEO https://www.youtube-nocookie.com/embed/T2a8yJC3VcQ]

タブを操作する前に実行する必要がある前提条件は少なからずある。

個人用タブとチャネルタブ、またはグループタブには、Teams 2 種類があります。 [個人用タブ](~/tabs/how-to/create-personal-tab.md)は、個人スコープのボットと共に個人用アプリの一部であり、1 人のユーザーを対象とします。 簡単にアクセスできるように、左側のナビゲーション バーにピン留めすることができます。 [チャネルタブまたはグループ タブは](~/tabs/how-to/create-channel-group-tab.md) 、チャネルやグループ チャットにコンテンツを配信し、専用の Web ベースのコンテンツを中心に共同作業スペースを作成する優れた方法です。

個人用タブ [、チャネル](~/tabs/how-to/create-tab-pages/content-page.md) またはグループ タブ、またはタスク モジュールの一部としてコンテンツ ページを作成できます。 Microsoft Teams[](~/tabs/how-to/create-tab-pages/configuration-page.md)アプリを構成し、チャネルまたはグループ チャット タブ、メッセージング拡張機能、または Office 365 Connector を構成する構成ページを作成できます。 ユーザーがインストール後にタブを再構成し、アプリケーション [のタブ削除ページ](~/tabs/how-to/create-tab-pages/removal-page.md) を作成できます。 タブを含むTeamsアプリをビルドする場合は、Android クライアントと[iOS](~/tabs/design/tabs-mobile.md)クライアントの両方でタブがどのように機能Teamsがあります。 タブは、 [基本情報、](~/tabs/how-to/access-teams-context.md) ロケール、テーマ情報を使用してコンテキストを取得する必要があります。また、タブ内の情報 `entityId` `subEntityId` を識別する必要があります。

アダプティブ カードを使用してタブを構築し、ボットTeams別のバックエンドを不要にすることで、すべてのアプリ機能を一元化できます。 [ステージ ビュー](~/tabs/tabs-link-unfurling.md)は、新しい UI コンポーネントで、画面全体で開いたコンテンツをTeamsタブとしてピン留めできます。既存の[リンクの分岐](~/tabs/tabs-link-unfurling.md)解除サービスが更新され、アダプティブ カードとチャット サービスを使用して URL をタブに変換するために使用されます。 会話型[](~/tabs/how-to/conversational-tabs.md)のサブエンティティを使用して会話タブを作成できます。ユーザーは、タブ全体を議論する代わりに、特定のタスク、患者、販売機会などのサブエンティティに関する会話をタブで行えます。タブ余白を[変更して、](~/resources/removing-tab-margins.md)アプリを構築する際の開発者のエクスペリエンスを向上できます。

## <a name="tab-features"></a>タブ機能

タブ機能は次のとおりです。

* ボットも含むアプリにタブを追加すると、ボットもチームに追加されます。
* 現在のAzure Active Directory (AAD) ID の認識。
* ユーザーが言語を示すロケール認識 `en-us` 。
* サポートされている場合、シングル サインオン (SSO) 機能があります。
* ボットまたはアプリ通知を使用して、タブまたはサービス内のサブエンティティ (個々の作業項目など) へのディープ リンクを使用できます。
* タブ内のリンクからタスク モジュールを開くことができます。
* タブ内で SharePoint Web パーツを再利用できます。

## <a name="tabs-user-scenarios"></a>タブのユーザー シナリオ

**シナリオ:** Teams 内に既存の Web ベース リソースを取得します。 \
**例:** 情報提供企業の Web サイトをユーザーに提供する Teams アプリに [個人] タブを作成します。

**シナリオ:** Teams ボットまたはメッセージング拡張機能にサポート ページを追加します。 \
**例:** 作成する個人タブは **について** と **ヘルプの** を、Web ページ コンテンツをユーザーに提供します。

**シナリオ:** 協力対話と共同作業のためにユーザーが定期的にやり取りするアイテムへのアクセスを提供します。 \
**例:** チャネルまたはグループ タブを作成し、個々のアイテムに深くリンクします。

## <a name="understand-how-tabs-work"></a>タブの動作を理解する

次のいずれかの方法を使用して、タブを作成できます。

* [アプリ マニフェストでカスタム タブを宣言する](#declare-custom-tab-in-app-manifest)
* [アダプティブ カードを使用してタブを作成する](~/tabs/how-to/build-adaptive-card-tabs.md)

### <a name="declare-custom-tab-in-app-manifest"></a>アプリ マニフェストでカスタム タブを宣言する

カスタム タブは、アプリ パッケージのアプリ マニフェストで宣言されます。 アプリのタブとして含める Web ページごとに、URL と範囲を定義します。 さらに、JavaScript クライアント[SDK](/javascript/api/overview/msteams-client) Teamsページに追加し、ページの読み込み後 `microsoftTeams.initialize()` に呼び出します。 Teamsページを表示し、Teams特定の情報 (たとえば、クライアントが暗いテーマを実行Teamsなど) へのアクセスを提供します。

チャネルまたはグループ内、または個人用スコープ内でタブを公開する場合は、タブに iframe HTML コンテンツ ページ<表示する \> 必要があります。 [](~/tabs/how-to/create-tab-pages/content-page.md)個人用タブの場合、コンテンツ URL は、配列内Teamsによってアプリ マニフェスト `contentUrl` に直接設定 `staticTabs` されます。 タブのコンテンツは、すべてのユーザーで同じです。

チャネルタブまたはグループ タブの場合は、追加の構成ページを作成することもできます。 このページでは、通常、URL クエリ文字列パラメーターを使用して、そのコンテキストに適したコンテンツを読み込むコンテンツ ページ URL を構成できます。 これは、チャネルまたはグループ タブを複数のチームまたはグループ チャットに追加できるためです。 以降のインストールごとに、ユーザーはタブを構成でき、必要に応じてエクスペリエンスを調整できます。 ユーザーがタブを追加または構成すると、URL は、ユーザー インターフェイス (UI) に表示されるタブTeams関連付けます。 タブを構成すると、その URL に追加のパラメーターが追加されます。 たとえば、[ページ] タブをAzure Boardsすると、構成ページでタブが読み込まれるボードを選択できます。 構成ページの URL は、アプリ マニフェストの `configurableTabs` 配列の `configurationUrl` プロパティで指定します。

複数のチャネルまたはグループ タブ、およびアプリごとに最大 16 の個人用タブを使用できます。

### <a name="tools-you-can-use-to-build-tabs"></a>タブの作成に使用できるツール
* [Visual Studio Code 用 Teams ツールキット](../toolkit/visual-studio-code-overview.md)
* [Visual Studio 用 Teams ツールキット](../toolkit/visual-studio-overview.md)

## <a name="see-also"></a>関連項目

* [デバイスのアクセス許可を要求する](../concepts/device-capabilities/native-device-permissions.md)
* [メディア機能を統合する](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [QR またはバーコード スキャナーを統合する](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [場所機能を統合する](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [前提条件](~/tabs/how-to/tab-requirements.md)
