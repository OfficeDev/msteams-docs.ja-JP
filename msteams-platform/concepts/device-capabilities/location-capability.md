---
title: 場所機能を統合する
author: Rajeshwari-v
description: コード スニペットとサンプルを使用Teams JavaScript クライアント SDK を使用して場所の機能を活用する方法について説明します。
keywords: 場所マップ機能ネイティブ デバイスのアクセス許可
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: a375d8f7c2692c9da8e220474c2c0ece97b623c2
ms.sourcegitcommit: a36760750ff4f510c374a4c956be57f7c1b4a0db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2022
ms.locfileid: "63675014"
---
# <a name="integrate-location-capabilities"></a>場所機能を統合する

ネイティブ デバイスの位置情報機能は、アプリと統合Teamsできます。  

JavaScript クライアント [SDK Microsoft Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)できます。アプリがユーザーのネイティブ デバイス機能にアクセスするために必要なツール[を提供します](native-device-permissions.md)。 [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) や [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) などの場所 API を使用して、アプリ内の機能を統合します。

## <a name="advantages-of-integrating-location-capabilities"></a>場所機能を統合する利点

Teams アプリに場所機能を統合する主な利点は、Teams プラットフォーム上の Web アプリ開発者が Microsoft Teams JavaScript クライアント SDK で位置情報機能を活用できるという利点です。

次の例は、場所機能の統合がさまざまなシナリオでどのように使用されるのか示しています。

* 工場では、監督者は、工場の近くで自分撮りを取得し、指定されたアプリを介して共有を求め、労働者の出席を追跡できます。 場所データもキャプチャされ、画像と共に送信されます。
* 位置情報機能を使用すると、サービス プロバイダーの保守スタッフは、携帯電話の塔の本物の正常性データを管理と共有できます。 管理は、キャプチャされた位置情報とメンテナンス スタッフが提出したデータの不一致を比較できます。

場所の機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要があります。 効果的な統合を行う場合は、場所 API [](#code-snippets) を呼び出すコード スニペットについて理解している必要があります。
API 応答エラーを理解して、アプリ内[](#error-handling)のエラーを処理することがTeamsです。

> [!NOTE]
> 現在、Microsoft Teams機能のサポートはモバイル クライアントでのみ利用できます。

## <a name="update-manifest"></a>マニフェストを更新する

プロパティを追加Teams指定して、[アプリ manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) `devicePermissions` ファイルを更新します`geolocation`。 これにより、アプリは場所機能の使用を開始する前に、ユーザーに必要なアクセス許可を求めできます。 アプリ マニフェストの更新プログラムは次のとおりです。

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> * [**アクセス許可の要求]** プロンプトは、関連する API が開始Teams自動的に表示されます。 詳細については、「デバイスのアクセス [許可を要求する」を参照してください](native-device-permissions.md)。
> * デバイスのアクセス許可はブラウザーによって異なります。 詳細については、「[ブラウザー デバイスのアクセス許可](browser-device-permissions.md)」を参照してください。

## <a name="location-apis"></a>場所 API

デバイスの位置情報機能を有効にするには、次の API セットを使用する必要があります。

| API      | [説明]   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | ユーザーの現在のデバイスの場所を指定するか、ネイティブの場所ピッカーを開き、ユーザーが選択した場所を返します。 |
|[showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | 地図上の場所を表示します。 |

> [!NOTE]
> API `getLocation()` は、次の入力 [構成と共に](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)提供されます `allowChooseLocation` `showMap`。 <br/> 値が true `allowChooseLocation` の *場合*、ユーザーは任意の場所を選択できます。<br/>  値が false の *場合*、ユーザーは現在の場所を変更できません。<br/> 値が false `showMap` の *場合*、現在の場所はマップを表示せずにフェッチされます。 `showMap` true に設定されている `allowChooseLocation` 場合は無視 *されます*。

次の図は、場所機能の Web アプリ エクスペリエンスを示しています。

![場所機能の Web アプリ エクスペリエンス](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a>コード スニペット

**場所を `getLocation` 取得する API の呼び出し:**

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

**場所を `showLocation` 表示する API の呼び出し:**

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

これらのエラーは、アプリで適切に処理Teamsがあります。 次の表に、エラー コードとエラーが生成される条件を示します。

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | INTERNAL_ERROR | 必要な操作の実行中に内部エラーが発生します。|
| **1000** | PERMISSION_DENIED |ユーザーは、アプリまたは web アプリTeams場所のアクセス許可を拒否しました。|
| **4000** | INVALID_ARGUMENTS | API は、間違った引数または不十分な必須引数を使用して呼び出されます。|
| **8000** | USER_ABORT |ユーザーが操作を取り消しました。|
| **9000** | OLD_PLATFORM | ユーザーは、API の実装が存在しない古いプラットフォーム ビルドに存在します。 ビルドをアップグレードすると、問題が解決します。|

### <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| アプリ のチェックインの現在の場所 | ユーザーは現在の場所をチェックインし、以前のすべての場所のチェックインを表示できます。| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/nodejs) |

## <a name="see-also"></a>関連項目

* [Teams でメディア機能を統合する](mobile-camera-image-permissions.md)
* [QR コードまたはバーコード スキャナー機能をアプリに統合Teams](qr-barcode-scanner-capability.md)
* [ユーザー選択ツールをユーザー 選択ツールにTeams](people-picker-capability.md)
