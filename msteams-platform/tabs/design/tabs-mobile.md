---
title: モバイルのタブ
description: モバイルでタブを実装するための開発者Microsoft Teams説明します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 41ba96b64bd31f3b226aeba72969bc44c1ae8955
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630657"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

タブを含む Microsoft Teams アプリを構築する場合は、Android クライアントと iOS クライアントの両方でタブがどのように機能Microsoft Teamsがあります。 以下のセクションでは、考慮する必要がある主要なシナリオの一部について説明します。

## <a name="authentication"></a>認証

モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。

## <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、低帯域幅と断続的な接続で定期的に機能する必要があります。 アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。 また、長時間実行されるプロセスに対してユーザーにフィードバックを提供するユーザー進行状況インジケーターも必要です。

## <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。 Android デバイスの場合 [、DevTools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。 タブレットを含む、高パフォーマンスデバイスと低パフォーマンスデバイスの両方でテストすることをお勧めします。

## <a name="distribution"></a>配布

モバイル クライアントで適切にTeams機能するには、モバイル ストアに一覧表示されているアプリTeams必要があります。 タブの可用性と動作は、アプリが承認されたかどうかによって異なります。

### <a name="apps-on-teams-store-approved-for-mobile"></a>モバイル用にTeamsストア上のアプリ

次の表では、アプリがモバイル ストアに表示され、モバイルTeams承認された場合のタブの可用性と動作について説明します。

|機能   |モバイルの可用性   |モバイル動作|
|----------|-----------|------------|
|チャネル <br /> [グループ] タブ|はい|アプリの構成を使用Teamsモバイル クライアントのタブが開 `contentUrl` きます。|
|個人用アプリ|はい|[個人用アプリ] タブの各タブが、Teamsを使用してモバイル クライアントに表示 `contentUrl` されます。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>モバイルで承認Teamsアプリストアのアプリ

次の表は、アプリがモバイル ストアに一覧表示されているが、モバイルTeams承認されていない場合のタブの可用性と動作について説明します。

| 機能 | モバイルの可用性 | モバイル動作 |
|----------|-----------|------------|
|[チャネルとグループ] タブ|はい|タブは、アプリの構成を使用して Teams モバイル クライアントではなく、デバイスの既定のブラウザーで開きます。これは、ソース コードの関数にも含める `websiteUrl` 必要 `setSettings()` [があります](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。 ただし、アプリの横にある [詳細] を選択し、[開く]を選択すると、Teams モバイルクライアントのタブが表示され、アプリの構成がトリガー `contentUrl` されます。|
|個人用アプリ|なし|該当なし|

### <a name="apps-not-on-teams-store"></a>アプリがストアTeamsしない

アプリをサイドロードする場合や、組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。

## <a name="see-also"></a>関連項目

* [タブデザインのガイドライン](~/tabs/design/tabs.md)
