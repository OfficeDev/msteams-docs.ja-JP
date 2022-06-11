---
title: 場所機能を統合する
author: Rajeshwari-v
description: Teams JavaScript クライアント SDK を使用して、コード スニペットとサンプルを使用して位置情報機能を活用する方法について説明します
keywords: 場所マップ機能のネイティブ デバイスのアクセス許可
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: ff2403331d3d51581be4711fb6fb14fcdb809544
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2022
ms.locfileid: "66033051"
---
# <a name="integrate-location-capabilities"></a>場所機能を統合する

ネイティブ デバイスの位置情報機能を Teams アプリと統合できます。  

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を使用できます。これは、アプリがユーザーの [ネイティブ デバイス機能](native-device-permissions.md) にアクセスするために必要なツールを提供します。 [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) や [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) などの場所 API を使用して、アプリ内の機能を統合します。

## <a name="advantages-of-integrating-location-capabilities"></a>場所の機能を統合する利点

Teams アプリで位置情報機能を統合する主な利点は、Teams プラットフォーム上の Web アプリ開発者が、Microsoft Teams JavaScript クライアント SDK で位置情報機能を活用できることです。

次の例は、場所機能の統合がさまざまなシナリオでどのように使用されるかを示しています。

* 工場では、監督者は、工場の近くで自分撮りをして、指定されたアプリを介して共有するように依頼することで、労働者の出席を追跡できます。 また、場所データもキャプチャされ、画像と共に送信されます。
* 場所の機能により、サービス プロバイダーのメンテナンス スタッフは、携帯電話の塔の本格的な正常性データを管理と共有できます。 管理は、キャプチャされた場所情報とメンテナンス スタッフによって送信されたデータの間の不一致を比較できます。

ロケーション機能を統合するには、アプリのマニフェスト ファイルを更新して API を呼び出す必要があります。 効果的な統合を実現するには、場所 API を呼び出すための [コード スニペット](#code-snippets) をよく理解している必要があります。
Teams アプリのエラーを処理するには、[API 応答エラー](#error-handling)を理解しておくことが重要です。

> [!NOTE]
> 現在、ロケーション機能に対する Microsoft Teams のサポートは、モバイル クライアントでのみ利用できます。

## <a name="update-manifest"></a>マニフェストを更新する

`devicePermissions` プロパティを追加して `geolocation` を指定することにより、Teamsアプリの [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) ファイルを更新します。 これにより、ユーザーがロケーション機能の使用を開始する前に、アプリがユーザーに必要な権限を要求できるようになります。 アプリ マニフェストの更新プログラムは次のとおりです。

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> * **アクセス許可要求** プロンプトは、関連する Teams API が開始されると自動的に表示されます。 詳細については、「[デバイスのアクセス許可要求](native-device-permissions.md)」 を参照してください。
> * デバイスのアクセス許可はブラウザーによって異なります。 詳細については、「[ブラウザー デバイスのアクセス許可](browser-device-permissions.md)」を参照してください。

## <a name="location-apis"></a>場所 API

デバイスの位置情報機能を有効にするには、次の API セットを使用する必要があります。

| API      | 説明   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | ユーザーの現在のデバイスの場所を指定するか、ネイティブの場所ピッカーを開き、ユーザーが選択した場所を返します。 |
|[showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | マップ上の場所を表示します。 |

> [!NOTE]
> `getLocation()` API には、次の[入力構成](/javascript/api/@microsoft/teams-js/microsoftteams.location.locationprops)、`allowChooseLocation`、および `showMap` が付属しています。<br/> `allowChooseLocation`の値が *true* の場合、ユーザーは任意の場所を選択できます。<br/>  値が *false* の場合、ユーザーは現在の場所を変更できません。<br/> `showMap` の値が *false* の場合、現在の場所は地図を表示せずに取得されます。 `allowChooseLocation` が *true* に設定されている場合、`showMap` は無視されます。

次の画像は、ロケーション機能の Web アプリ エクスペリエンスを示しています。

![場所の機能に関する Web アプリ エクスペリエンス](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a>コード スニペット

**場所を取得するために `getLocation` API を呼び出します:**

```javascript
let locationProps = {"allowChooseLocation":true,"showMap":true};
microsoftTeams.location.getLocation(locationProps, (err: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
          if (err) {
            output(err);
            return;
          }
          output(JSON.stringify(location));
});
```

**場所を表示するために `showLocation` APIを呼び出します:**

```javascript
let location = {"latitude":17,"longitude":17};
microsoftTeams.location.showLocation(location, (err: microsoftTeams.SdkError, result: boolean) => {
          if (err) {
            output(err);
            return;
          }
     output(result);
});
```

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | 内部エラーです(_E) | 必要な操作の実行中に内部エラーが発生しました。|
| **1000** | PERMISSION_DENIED |ユーザーが Teams アプリまたは Web アプリに対する場所のアクセス許可を拒否しました。|
| **4000** | 引数が無効です | API が間違った引数または不十分な必須引数で呼び出されました。|
| **8000** | USER_ABORT |ユーザーが操作を取り消しました。|
| **9000** | OLD_PLATFORM | ユーザーは、API の実装が利用できない以前のプラットフォーム ビルドを使用しています。 ビルドをアップグレードすると、問題が解決するはずです。|

### <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| アプリ チェックインの現在の場所 | ユーザーは現在の場所をチェックインし、以前のすべての場所のチェックインを表示できます。| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/nodejs) |

## <a name="see-also"></a>関連項目

* [Teams でメディア機能を統合する](mobile-camera-image-permissions.md)
* [Teams で QR コードまたはバーコード スキャナー機能を統合する](qr-barcode-scanner-capability.md)
* [Teams でユーザー ピッカーを統合する](people-picker-capability.md)
