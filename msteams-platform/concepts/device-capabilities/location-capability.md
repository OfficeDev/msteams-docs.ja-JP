---
title: 場所機能を統合する
author: Rajeshwari-v
description: Teams JavaScript クライアント SDK を使用して場所の機能を活用する方法
keywords: 場所マップ機能ネイティブ デバイスのアクセス許可
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 98d37c4f34f638f129c07b012d98ec54c7c8e44f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019861"
---
# <a name="integrate-location-capabilities"></a>場所機能を統合する 

このドキュメントでは、ネイティブ デバイスの位置情報機能を Teams アプリに統合する方法について説明します。  

[アプリがユーザーのネイティブ デバイス](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)機能にアクセスするために必要なツールを提供する Microsoft Teams JavaScript クライアント SDK[を使用できます](native-device-permissions.md)。 [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)や[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true)などの場所 API を使用して、アプリ内の機能を統合します。 

## <a name="advantages-of-integrating-location-capabilities"></a>場所機能を統合する利点

Teams アプリに場所機能を統合する主な利点は、Teams プラットフォーム上の Web アプリ開発者が Microsoft Teams JavaScript クライアント SDK で位置情報機能を活用できるという利点です。 

次の例は、場所機能の統合がさまざまなシナリオでどのように使用されるのか示しています。
* 工場では、監督者は、工場の近くで自分撮りを取得し、指定されたアプリを介して共有を求め、労働者の出席を追跡できます。 場所データもキャプチャされ、画像と共に送信されます。
* 位置情報機能を使用すると、サービス プロバイダーの保守スタッフは、携帯電話の塔の本物の正常性データを管理と共有できます。 管理は、キャプチャされた位置情報とメンテナンス スタッフが提出したデータの不一致を比較できます。

場所の機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要があります。 効果的な統合を行う場合は、場所[](#code-snippets)API を呼び出すコード スニペットについて理解している必要があります。 Teams アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。

> [!NOTE] 
> 現在、場所の機能に対する Microsoft Teams のサポートは、モバイル クライアントでのみ使用できます。

## <a name="update-manifest"></a>マニフェストの更新

プロパティを追加し [ 、manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions) Teams アプリを更新 `devicePermissions` します `geolocation` 。 これにより、アプリは場所機能の使用を開始する前に、ユーザーに必要なアクセス許可を求めできます。

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> 関連 **する Teams** API が開始されると、[アクセス許可の要求] プロンプトが自動的に表示されます。 詳細については、「デバイスのアクセス [許可を要求する」を参照してください](native-device-permissions.md)。

## <a name="location-apis"></a>場所 API

デバイスの位置情報機能を有効にするには、次の API セットを使用する必要があります。

| API      | 説明   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | ユーザーの現在のデバイスの場所を指定するか、ネイティブの場所ピッカーを開き、ユーザーが選択した場所を返します。 |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | 地図上の場所を表示する |

> [!NOTE]

> `getLocation()`API は、次の入力[構成](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)と共に `allowChooseLocation` 提供されます `showMap` 。 <br/> 値が true `allowChooseLocation` の *場合*、ユーザーは任意の場所を選択できます。<br/>  値が false の *場合*、ユーザーは現在の場所を変更できません。<br/> 値が false の `showMap` *場合*、現在の場所はマップを表示せずにフェッチされます。 `showMap` true に設定 `allowChooseLocation` されている場合は無視 *されます*。 


**場所機能用の Web アプリ エクスペリエンス** 
 ![場所機能の Web アプリ エクスペリエンス](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。 

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | INTERNAL_ERROR | 必要な操作の実行中に内部エラーが発生します。|
| **1000** | PERMISSION_DENIED |ユーザーが Teams アプリまたは Web アプリに対する場所のアクセス許可を拒否しました。|
| **4000** | INVALID_ARGUMENTS | API は、間違った引数または不十分な必須引数を使用して呼び出されます。|
| **8000** | USER_ABORT |ユーザーが操作を取り消しました。|
| **9000** | OLD_PLATFORM | ユーザーは、API の実装が存在しない古いプラットフォーム ビルドに存在します。 ビルドをアップグレードすると、問題が解決します。|

## <a name="code-snippets"></a>コード スニペット

**`getLocation`場所を取得する API の呼び出し:**

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

**`showLocation`場所を表示する API の呼び出し:**

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

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [Teams でのメディア機能の統合](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Teams に QR またはバーコード スキャナー機能を統合する](qr-barcode-scanner-capability.md)
