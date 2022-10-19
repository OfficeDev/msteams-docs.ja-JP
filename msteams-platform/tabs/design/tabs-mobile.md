---
title: モバイルのタブ
description: Android および iOS Microsoft Teams クライアント (モバイル) でのタブ機能、認証、低帯域幅接続、テスト、または配布方法について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 0dbb74d5c2854897f82708aa83a0c49df4f28890
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575769"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

タブを含む Microsoft Teams アプリを構築する場合は、Android クライアントと iOS Microsoft Teams クライアントの両方でタブがどのように機能するかをテストする必要があります。 この記事では、考慮する必要がある主なシナリオの一部について説明します。

Teams モバイル クライアントにチャネルまたはグループ タブを表示することを選択した場合、構成にはプロパティの [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) 値が `websiteUrl` 必要です。 最適なユーザー エクスペリエンスを確保するには、この記事のモバイル上のタブのガイダンスに従ってタブを作成する必要があります。

[Teams ストアを通じて配布される](~/concepts/deploy-and-publish/appsource/publish.md)アプリには、モバイル クライアント用の個別の承認プロセスがあります。 このようなアプリの既定の動作は次のとおりです。

| **アプリ機能** | **アプリが承認された場合の動作** | **アプリが承認されていない場合の動作** |
| --- | --- | --- |
| **個人用タブ** | モバイル クライアントの下部のバーにアプリが表示されます。 Teams クライアントでタブが開きます。 | モバイル クライアントの下部のバーにアプリが表示されません。 |
| **チャネル タブとグループ タブ** | を使用して `contentUrl`Teams クライアントでタブが開きます。 | タブは、Teams クライアント `websiteUrl`の外部のブラウザーで開きます。 |

> [!NOTE]
>
> * Teams で発行するために [AppSource](https://appsource.microsoft.com) に送信されたアプリは、モバイル応答性のために自動的に評価されます。 クエリについては、teamsubm@microsoft.com に問い合 teamsubm@microsoft.com。
> * AppSource を通じて配布されていないすべてのアプリの場合、既定では Teams クライアント内のアプリ内 Web ビューでタブが開き、個別の承認プロセスは必要ありません。
> * アプリの既定の動作は、Teams ストアを通じて配布される場合にのみ適用されます。 既定では、すべてのタブが Teams クライアントで開きます。
> * モバイルに適したアプリの評価を開始するには、アプリの詳細を teamsubm@microsoft.com してください。

## <a name="authentication"></a>認証

モバイル クライアントで認証を機能させるには、Teams JavaScript SDK を少なくともバージョン 1.4.1 にアップグレードする必要があります。

## <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、低帯域幅と断続的な接続で機能します。 アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。 また、進行状況インジケーターを使用して、実行時間の長いプロセスについてユーザーにフィードバックを提供する必要もあります。

## <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが正しく機能することを検証する必要があります。 Android デバイスの場合、 [DevTools を](~/tabs/how-to/developer-tools.md) 使用して、実行中にタブをデバッグできます。 タブレットを含め、パフォーマンスの高いデバイスと低パフォーマンスの両方のデバイスでテストすることをお勧めします。

## <a name="distribution"></a>配布

Teams ストアに一覧表示されているアプリは、Teams モバイル クライアントで正常に機能するには、モバイルでの使用を承認する必要があります。 タブの可用性と動作は、アプリが承認されているかどうかによって異なります。

### <a name="apps-on-teams-store-approved-for-mobile"></a>モバイル向けに承認された Teams ストア上のアプリ

次の表では、アプリが Teams ストアに一覧表示され、モバイルでの使用が承認された場合のタブの可用性と動作について説明します。

|機能   |モバイルの可用性   |モバイル動作|
|----------|-----------|------------|
|チャネル <br /> [グループ] タブと [グループ] タブ|はい|アプリの構成を使用して、Teams モバイル クライアントでタブが `contentUrl` 開きます。|
|個人用アプリ|はい|個人用アプリ タブの各タブは、それぞれの `contentUrl` 構成を使用して Teams モバイル クライアントで開きます。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Teams ストア上のアプリがモバイルに対して承認されていない

次の表では、アプリが Teams ストアに一覧表示されているがモバイルでの使用が承認されていない場合のタブの可用性と動作について説明します。

| 機能 | モバイルの可用性 | モバイル動作 |
|----------|-----------|------------|
|[チャネルとグループ] タブ|はい|アプリの構成を使用する Teams モバイル クライアントではなく、デバイスの既定の`websiteUrl`ブラウザーでタブが開きます。これは、ソース コードの`setSettings()`[関数](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace)にも含める必要があります。 ただし、ユーザーは Teams モバイル クライアントのタブを表示するには、アプリの横にある **[その他** ] を選択し、[ **開く**] を選択すると、アプリの `contentUrl` 構成がトリガーされます。|
|個人用アプリ|いいえ|対象外|

> [!NOTE]
> モバイル アプリにボットとタブの両方の機能がある場合、ボット メッセージはチャット セクションに表示されます。
>
> ボット アプリの **[チャット** ] を選択し、[ **その他 ] (...)** を選択すると、そのアプリのタブ機能が一覧に表示されません。 ただし、[**チャット**] セクションの右下にある **[その他] (...)** を選択した場合は、そのアプリのボット アプリ機能へのリンクを含むタブ アプリを表示できます。

### <a name="apps-not-on-teams-store"></a>Teams ストアにないアプリ

アプリをサイドロードするか、組織のアプリ カタログに発行する場合、タブの動作は、Microsoft for Mobile で承認された Teams ストア アプリと同じです。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [タブのコンテキストを取得する](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>関連項目

* [タブデザインのガイドライン](~/tabs/design/tabs.md)
* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [Teams モバイルの計画 - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
