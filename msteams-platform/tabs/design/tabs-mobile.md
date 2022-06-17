---
title: モバイルのタブ
description: このモジュールでは、Microsoft Teams モバイル、認証、低帯域幅接続、モバイル クライアントでのテスト、配布などのタブの実装について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: da9757ee0153b3f2fe80e576e156f45bc90a15cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144267"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

タブを含むMicrosoft Teams アプリを構築する場合は、Android クライアントとiOS Microsoft Teams クライアントの両方でタブがどのように機能するかをテストする必要があります。 この記事では、考慮する必要がある主なシナリオの一部について説明します。

Teamsモバイル クライアントにチャネルまたはグループ タブを表示することを選択した場合、構成にはプロパティの[`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true)値が`websiteUrl`必要です。 最適なユーザー エクスペリエンスを確保するには、この記事のモバイル上のタブのガイダンスに従ってタブを作成する必要があります。

[Teams ストアを通じて配布される](~/concepts/deploy-and-publish/appsource/publish.md)アプリには、モバイル クライアントに対する個別の承認プロセスがあります。 このようなアプリの既定の動作は次のとおりです。

| **アプリ機能** | **アプリが承認された場合の動作** | **アプリが承認されていない場合の動作** |
| --- | --- | --- |
| **個人用タブ** | モバイル クライアントの下部のバーにアプリが表示されます。 Teams クライアントでタブが開きます。 | モバイル クライアントの下部のバーにアプリが表示されません。 |
| **チャネル タブとグループ タブ** | Teams クライアント`contentUrl`でタブが開きます。 | タブは、Teams クライアント`websiteUrl`の外部のブラウザーで開きます。 |

> [!NOTE]
>
> * Teamsで発行するために [AppSource](https://appsource.microsoft.com) に送信されたアプリは、モバイルの応答性のために自動的に評価されます。 クエリについては、teamsubm@microsoft.com に問い合 teamsubm@microsoft.com。
> * AppSource を通じて配布されていないすべてのアプリの場合、既定では、Teams クライアント内のアプリ内 Web ビューでタブが開き、個別の承認プロセスは必要ありません。
> * アプリの既定の動作は、Teams ストアを通じて配布される場合にのみ適用されます。 既定では、すべてのタブがTeams クライアントで開きます。
> * モバイルに適したアプリの評価を開始するには、アプリの詳細を teamsubm@microsoft.com してください。

## <a name="authentication"></a>認証

モバイル クライアントで認証を機能させるには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。

## <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、低帯域幅と断続的な接続で機能します。 アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。 また、進行状況インジケーターを使用して、実行時間の長いプロセスについてユーザーにフィードバックを提供する必要もあります。

## <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが正しく機能することを検証する必要があります。 Android デバイスの場合は、[DevTools を](~/tabs/how-to/developer-tools.md)使用して、実行中にタブをデバッグできます。 Tablet PCを含め、パフォーマンスの高いデバイスと低パフォーマンスの両方のデバイスでテストすることをお勧めします。

## <a name="distribution"></a>配布

Teams ストアに一覧表示されているアプリは、モバイル使用がTeamsモバイル クライアントで正常に機能することを承認する必要があります。 タブの可用性と動作は、アプリが承認されているかどうかによって異なります。

### <a name="apps-on-teams-store-approved-for-mobile"></a>モバイル向けに承認されたTeams ストア上のアプリ

次の表では、アプリがTeams ストアに一覧表示され、モバイルでの使用が承認された場合のタブの可用性と動作について説明します。

|機能   |モバイルの可用性   |モバイル動作|
|----------|-----------|------------|
|チャネル <br /> [グループ] タブと [グループ] タブ|はい|アプリの構成を使用して、Teams モバイル クライアントで`contentUrl`タブが開きます。|
|個人用アプリ|はい|個人用アプリ タブの各タブは、それぞれの`contentUrl`構成を使用してTeamsモバイル クライアントで開きます。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Teams ストア上のアプリがモバイルに対して承認されていない

次の表では、アプリがTeams ストアに一覧表示されているがモバイルでの使用が承認されていない場合のタブの可用性と動作について説明します。

| 機能 | モバイルの可用性 | モバイル動作 |
|----------|-----------|------------|
|[チャネルとグループ] タブ|はい|タブは、アプリの構成を使用するモバイル クライアントTeamsではなく、デバイスの既定の`websiteUrl`ブラウザーで開きます。これは、ソース コードの`setSettings()`[関数](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace)にも含める必要があります。 ただし、ユーザーは、アプリの横にある **[その他**] を選択し、[**開く**] を選択すると、Teamsモバイル クライアントのタブを表示できます。これにより、アプリの`contentUrl`構成がトリガーされます。|
|個人用アプリ|なし|該当なし|

### <a name="apps-not-on-teams-store"></a>Teams ストアにないアプリ

アプリをサイドロードするか、組織のアプリ カタログに発行する場合、タブの動作は、Microsoft for mobile によって承認されたアプリTeamsストア アプリと同じです。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [タブのコンテキストを取得する](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>関連項目

* [タブデザインのガイドライン](~/tabs/design/tabs.md)
* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [Teams モバイルの計画 - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
