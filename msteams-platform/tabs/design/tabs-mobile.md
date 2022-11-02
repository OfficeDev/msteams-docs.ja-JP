---
title: モバイルのタブ
description: Android および iOS Microsoft Teams クライアント (モバイル)、認証、低帯域幅接続、テスト、または配布のタブ機能について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 8dac56cd609466c116f39baf5dc9d9a7970645ec
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820081"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

タブを含む Microsoft Teams アプリを構築する場合は、Android クライアントと iOS Microsoft Teams クライアントの両方でタブがどのように機能するかをテストする必要があります。 この記事では、考慮する必要がある主要なシナリオの一部について説明します。

Teams モバイル クライアントにチャネルまたはグループ タブを表示する場合は、構成に [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) プロパティの値が `websiteUrl` 必要です。 最適なユーザー エクスペリエンスを確保するには、タブを作成するときに、この記事のモバイルのタブに関するガイダンスに従う必要があります。

[Teams ストアを通じて配布される](~/concepts/deploy-and-publish/appsource/publish.md)アプリには、モバイル クライアント用の個別の承認プロセスがあります。 このようなアプリの既定の動作は次のとおりです。

| **アプリ機能** | **アプリが承認された場合の動作** | **アプリが承認されていない場合の動作** |
| --- | --- | --- |
| **個人用タブ** | モバイル クライアントの下部バーにアプリが表示されます。 Teams クライアントでタブが開きます。 | モバイル クライアントの下部バーにアプリが表示されません。 |
| **チャネル タブとグループ タブ** | を使用して `contentUrl`Teams クライアントでタブが開きます。 | タブは、 を使用して `websiteUrl`Teams クライアントの外部のブラウザーで開きます。 |

> [!NOTE]
>
> * Teams に発行するために [AppSource](https://appsource.microsoft.com) に送信されたアプリは、モバイルの応答性のために自動的に評価されます。 任意のクエリについては、teamsubm@microsoft.com に問い合わせしてください。
> * AppSource を介して配布されていないすべてのアプリの場合、タブは既定で Teams クライアント内のアプリ内 Web ビューで開き、個別の承認プロセスは必要ありません。
> * アプリの既定の動作は、Teams ストアを通じて配布された場合にのみ適用されます。 既定では、すべてのタブが Teams クライアントで開きます。
> * モバイルに適したアプリの評価を開始するには、アプリの詳細を teamsubm@microsoft.com します。

## <a name="authentication"></a>認証

モバイル クライアントで認証を機能させるには、Teams JavaScript SDK を少なくともバージョン 1.4.1 にアップグレードする必要があります。

## <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、低帯域幅と断続的な接続で機能します。 アプリは、コンテキスト メッセージをユーザーに提供することで、タイムアウトを適切に処理する必要があります。 また、進行状況インジケーターを使用して、実行時間の長いプロセスに関するフィードバックをユーザーに提供する必要があります。

## <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが正しく機能することを検証する必要があります。 Android デバイスの場合は、 [DevTools を](~/tabs/how-to/developer-tools.md) 使用して、実行中にタブをデバッグできます。 タブレットを含む高パフォーマンスデバイスと低パフォーマンスデバイスの両方でテストすることをお勧めします。

## <a name="distribution"></a>配布

Teams ストアに一覧表示されているアプリは、Teams モバイル クライアントでモバイルを適切に機能させるために承認されている必要があります。 タブの可用性と動作は、アプリが承認されているかどうかによって異なります。

### <a name="apps-on-teams-store-approved-for-mobile"></a>モバイル向けに承認された Teams ストア上のアプリ

次の表では、アプリが Teams ストアに一覧表示され、モバイルでの使用が承認されている場合のタブの可用性と動作について説明します。

|機能   |モバイルの可用性   |モバイル動作|
|----------|-----------|------------|
|チャネル <br /> [グループ] タブ|はい|アプリの構成を使用して、Teams モバイル クライアントで `contentUrl` タブが開きます。|
|個人用アプリ|はい|個人用アプリ タブの各タブは、それぞれの `contentUrl` 構成を使用して Teams モバイル クライアントで開きます。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Teams ストア上のアプリがモバイル向けに承認されていない

次の表では、アプリが Teams ストアに一覧表示されているが、モバイルでの使用が承認されていない場合のタブの可用性と動作について説明します。

| 機能 | モバイルの可用性 | モバイル動作 |
|----------|-----------|------------|
|[チャネルとグループ] タブ|はい|アプリの構成を使用して Teams モバイル クライアントではなく、デバイスの既定の`websiteUrl`ブラウザーでタブが開きます。これは、ソース コードの`setSettings()`[関数](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace)にも含める必要があります。 ただし、ユーザーは Teams モバイル クライアントのタブを表示するには、アプリの横にある **[その他** ] を選択し、[ **開く**] を選択すると、アプリの `contentUrl` 構成がトリガーされます。|
|個人用アプリ|いいえ|対象外|

> [!NOTE]
> ボットメッセージは、モバイル アプリにボットとタブの両方の機能がある場合、チャット セクションに表示されます。
>
> ボット アプリの **[チャット** ] を選択し、[ **その他 (...)]** を選択すると、そのアプリのタブ機能が一覧に表示されません。 ただし、[**チャット**] セクションの右下にある [**その他] (...)** を選択した場合は、そのアプリのボット アプリ機能へのリンクを含むタブ アプリを表示できます。

### <a name="apps-not-on-teams-store"></a>Teams ストアにないアプリ

アプリをサイドローディングする場合、または組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [タブのコンテキストを取得する](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](../what-are-tabs.md)
* [アダプティブ カードを使用してタブをビルドする](../how-to/build-adaptive-card-tabs.md)
* [プライベート タブを作成する](../how-to/create-personal-tab.md)
* [Teams モバイルの応答タブを計画する](../../concepts/design/plan-responsive-tabs-for-teams-mobile.md)
* [Microsoft Teams 用のタブを設計する](tabs.md)
* [Microsoft Teams タブの DevTools](../how-to/developer-tools.md)
* [アプリのテスト](../../concepts/build-and-test/test-app-overview.md)
* [Microsoft Teams アプリを配布する](../../concepts/deploy-and-publish/apps-publish-overview.md)
* [Teams アプリ パッケージを作成する](../../concepts/build-and-test/apps-package.md)
