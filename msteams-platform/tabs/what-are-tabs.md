---
title: Teams のカスタム タブとは
author: laujan
description: Teams プラットフォームでのカスタム タブの概要
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 19c51d5c30f938dc5368b28b69ffeb29330887b4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566594"
---
# <a name="microsoft-teams-tabs"></a>Microsoft Teams のタブ

タブとは、Microsoft Teams に組み込まれている Teams 対応 Web ページです。 これらは簡単な HTML <iFrame \> タブで、アプリ マニフェストで宣言されたドメインを指していて、チーム内のチャネル、グループ チャット、または個々のユーザー用の個人用アプリとして追加できます。 アプリにカスタム タブを含めて独自の Web コンテンツを Teams に埋め込んだり、Teams 固有の機能を Web コンテンツに追加したりできます。 詳細については[、「JavaScript クライアント SDK Teamsを参照してください](/javascript/api/overview/msteams-client)。

Teams では、チャネル/グループ および 個人 の 2 種類のタブが利用可能です。 チャネル/グループ タブは、コンテンツをチャネルやグループのチャットに配信します。また、専用の Web ベースのコンテンツまわりに関する共同作業スペースを作成するのに優れた方法です。 [個人] タブは、個人を対象としたボットと共に、個人用アプリの一部であり、1 人のユーザーを対象としています。 簡単にアクセスできるように、左側のナビゲーション バーにピン留めすることができます。

## <a name="tab-features"></a>タブ機能

> [!div class="checklist"]
>
> * タブがボットも含まれるアプリに追加されると、ボットもチームに追加されます。
> * 現在のユーザーの Azure Active Directory (Azure AD) ID の認識。
> * `en-us` などの言語を示すユーザーのロケールを認識します。 
> * サポートされている場合、シングル サインオン (SSO) 機能があります。
> * ボットやアプリの通知を使用して、タブや、個人の作業項目などのサービス内のサブ エンティティにディープ リンクできます。
> * タブ内のリンクからタスク モジュールを開くことができます。
> * タブ内で SharePoint Web パーツを再利用できます。

## <a name="tabs-user-scenarios"></a>タブのユーザー シナリオ

**シナリオ:** Teams 内に既存の Web ベース リソースを取得します。 \
**例:** 情報提供企業の Web サイトをユーザーに提供する Teams アプリに [個人] タブを作成します。

**シナリオ:** Teams ボットまたはメッセージング拡張機能にサポート ページを追加します。 \
**例:** 作成する個人タブは *について* と *ヘルプの* を、Web ページ コンテンツをユーザーに提供します。

**シナリオ:** 協力対話と共同作業のためにユーザーが定期的にやり取りするアイテムへのアクセスを提供します。 \
**例:** 個々のアイテムに詳細なリンクを設定した [チャネル/グループ] タブを作成します。

## <a name="understand-how-tabs-work"></a>タブの動作を理解する

カスタム タブは、アプリ パッケージのアプリ マニフェストで宣言されます。 アプリのタブとして含める Web ページごとに、URL と範囲を定義します。 また、[Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) をページに追加して、ページの読み込みが終了したら `microsoftTeams.initialize()` を呼び出す必要があります。 この操作を行うと、Teams にページが表示されるようになり、Teams 固有の情報 (たとえば、Teams クライアントが *濃色テーマ* を実行している場合) へのアクセスが出来、結果に基づいてアクションを実行できるようになります。

チャネル/グループ または 個人 スコープ内でタブを表示するかどうかを選択した場合は、タブに <iframe 付き\>HTML[コンテンツ ページ](~/tabs/how-to/create-tab-pages/content-page.md)を表示する必要があります。個人 タブの場合、コンテンツ URL は`staticTabs`配列内の`contentUrl`プロパティによってTeams アプリのマニフェストに直接設定されます。 タブの内容は、すべてのユーザーに対して同じになります。

チャネル/グループ タブの場合は、ユーザーがコンテンツ ページの URL を構成するための追加の構成ページも作成する必要があ、,通常は、URL クエリ文字列パラメーターを使用し、そのコンテキストに適したコンテンツを読み込みます。 これは、チャネル/グループ タブを複数のチームまたはグループ チャットに追加できるためです。 以降にインストールが行われるたびに、ユーザーはタブを構成して、必要に応じて操作を調整することが出来ます。 ユーザーがタブを追加、またはタブを構成すると、Teams UI に表示されているタブに URL が関連付けられます。 タブの構成は、その URL にさらにパラメーターを追加するだけです。 たとえば、Azure Boards タブを追加すると、構成ページで、タブにロードするボードを選択することができます。 構成ページの URL は、アプリ マニフェストの `configurableTabs` 配列の `configurationUrl` プロパティで指定します。

複数のチャネルまたはグループ タブ、およびアプリごとに最大 16 個の個人用タブを使用できます。

## <a name="mobile-considerations"></a>モバイルに関する考慮事項

モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。 最適なユーザー エクスペリエンスを実現するには、タブ [を作成するときに](~/tabs/design/tabs-mobile.md) モバイル上のタブのガイダンスに従う必要があります。 モバイル[ストアを通じて配布Teamsモバイル](~/concepts/deploy-and-publish/appsource/publish.md)クライアントに対する個別の承認プロセスがあります。 このようなアプリの既定の動作は次のとおりです。

| **アプリの機能** | **アプリが承認された場合の動作** | **アプリが承認されていない場合の動作** |
| --- | --- | --- |
| **個人用タブ** | モバイル クライアントの下部バーにアプリが表示されます。 タブは、クライアントTeams開きます。 | モバイル クライアントの下部バーにアプリが表示されません。 |
| **チャネルタブとグループ タブ** | タブは、 を使用してクライアントTeams開きます `contentUrl` 。 | タブは、 を使用してクライアントの外部Teams開きます `websiteUrl` 。 |

> [!NOTE]
>
> アプリの既定の動作は、アプリ ストアを通じて配布Teamsです。 既定では、すべてのタブがクライアントでTeamsされます。
> モバイルに優しいアプリの評価を開始するには、アプリの詳細 teamsubm@microsoft.com 確認してください。

## <a name="see-also"></a>関連項目

* [デバイスのアクセス許可を要求する](../concepts/device-capabilities/native-device-permissions.md)
* [メディア機能を統合する](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [QR またはバーコード スキャナーを統合する](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [場所機能を統合する](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブの要件](~/tabs/how-to/tab-requirements.md)