---
title: モバイルのタブ
description: モバイル、認証、低帯域幅Microsoft Teams、モバイル クライアントでのテスト、配布などについて、タブを実装する方法について学習します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: アプリのモバイル タブ チャネル グループ認証の配布
ms.openlocfilehash: eb0bc5b0415f1879619cc704a77501406bcea397
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356372"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

タブを含むアプリをMicrosoft Teamsする場合は、Android クライアントと iOS クライアントの両方でタブがどのように機能Microsoft Teamsがあります。 この記事では、考慮する必要がある主要なシナリオの一部について説明します。

モバイル クライアントにチャネルまたはグループ タブを表示Teams場合[`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true)、構成にはプロパティの値が必要`websiteUrl`です。 最適なユーザー エクスペリエンスを実現するには、タブを作成する際に、この記事のモバイルタブのガイダンスに従う必要があります。

モバイル [ストアを通じて配布Teamsモバイル](~/concepts/deploy-and-publish/appsource/publish.md) クライアントに対する個別の承認プロセスがあります。 このようなアプリの既定の動作は次のとおりです。

| **アプリの機能** | **アプリが承認された場合の動作** | **アプリが承認されていない場合の動作** |
| --- | --- | --- |
| **[個人] タブ** | モバイル クライアントの下部バーにアプリが表示されます。 タブは、クライアントTeams開きます。 | モバイル クライアントの下部バーにアプリが表示されません。 |
| **チャネルタブとグループ タブ** | タブが使用しているクライアントTeams開きます`contentUrl`。 | タブは、 を使用してクライアントの外部Teams開きます`websiteUrl`。 |

> [!NOTE]
> * AppSource に送信された[アプリ](https://appsource.microsoft.com)は、モバイルの応答性Teams自動的に評価されます。 クエリの場合は、ユーザーに問い合 teamsubm@microsoft.com。
> * AppSource を介して配布されていないすべてのアプリでは、タブは既定で Teams クライアント内のアプリ内 Web ビューで開き、個別の承認プロセスは必要ありません。
> * アプリの既定の動作は、アプリ ストアを通じて配布Teamsです。 既定では、すべてのタブがクライアントでTeamsされます。
> * モバイルに優しいアプリの評価を開始するには、アプリの詳細 teamsubm@microsoft.com 確認してください。

## <a name="authentication"></a>認証

モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。

## <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、低帯域幅と断続的な接続で機能します。 アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。 また、進行状況インジケーターを使用して、長時間実行されるプロセスに対するフィードバックをユーザーに提供する必要があります。

## <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。 Android デバイスの場合、 [DevTools を使用して](~/tabs/how-to/developer-tools.md) 、実行中にタブをデバッグできます。 タブレットを含む高パフォーマンスデバイスと低パフォーマンスデバイスの両方でテストをお勧めします。

## <a name="distribution"></a>配布

モバイル クライアントで適切にTeams機能するには、モバイル ストアに一覧表示されているアプリTeams必要があります。 タブの可用性と動作は、アプリが承認されたかどうかによって異なります。

### <a name="apps-on-teams-store-approved-for-mobile"></a>モバイル用にTeamsストア上のアプリ

次の表では、アプリがモバイル ストアに表示され、モバイルでの使用が承認Teamsタブの可用性と動作について説明します。

|機能   |モバイルの可用性   |モバイル動作|
|----------|-----------|------------|
|チャネル <br /> [グループ] タブ|必要|アプリの構成を使用Teamsモバイル クライアントのタブが開`contentUrl`きます。|
|個人用アプリ|はい|[個人用アプリ] タブの各タブが、それぞれの構成Teamsモバイル クライアントで開`contentUrl`きます。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>モバイル向Teamsアプリが承認されていないアプリ

次の表は、アプリがモバイル ストアに表示されているが、モバイルでの使用がTeams場合のタブの可用性と動作について説明します。

| 機能 | モバイルの可用性 | モバイル動作 |
|----------|-----------|------------|
|[チャネルとグループ] タブ|はい|タブは、アプリの構成を使用して Teams `websiteUrl` モバイル クライアントではなく、デバイスの既定のブラウザーで開きます。これは、ソース コードの機能にも含める必要`setSettings()`[があります](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace)。 ただし、ユーザーはアプリの横にある [Teams] を選択し、[開く]  を選択してアプリの構成をトリガーすることで、モバイル クライアントのタブを表示`contentUrl`できます。|
|個人用アプリ|なし|該当なし|

### <a name="apps-not-on-teams-store"></a>アプリがストアTeamsしない

アプリをサイドロードする場合や、組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブのコンテキストを取得する](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>関連項目

* [タブデザインのガイドライン](~/tabs/design/tabs.md)
* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのTeamsを計画する - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
