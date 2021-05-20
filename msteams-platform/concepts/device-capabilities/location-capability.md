---
title: 場所機能を統合する
author: Rajeshwari-v
description: Teams JavaScript クライアント SDK を使用して位置情報機能を活用する方法
keywords: 位置情報マップ機能 ネイティブ デバイスのアクセス許可
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b85f19e74d0a8121dd290fc395c1018178437b3a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566188"
---
# <a name="integrate-location-capabilities"></a>場所機能を統合する 

このドキュメントでは、ネイティブ デバイスの位置情報機能をTeams アプリに統合する方法について説明します。  

[JavaScript クライアント SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)使用すると、アプリがユーザーのネイティブ[デバイス機能](native-device-permissions.md)にアクセスするために必要なツールを提供します。 [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)や[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true)などの場所 API を使用して、アプリ内の機能を統合します。 

## <a name="advantages-of-integrating-location-capabilities"></a>ロケーション機能を統合する利点

Teams アプリに位置情報機能を統合する主な利点は、Teams プラットフォーム上の Web アプリ開発者が、Microsoft Teams JavaScript クライアント SDK を使用して位置情報機能を活用できることです。 

次の例は、さまざまなシナリオで場所機能の統合がどのように使用されているかを示しています。
* 工場では、スーパーバイザーは、工場の近くで自分撮りを取り、指定されたアプリを介してそれを共有するように求めることによって、労働者の出席を追跡することができます。 ロケーションデータもキャプチャされ、画像と一緒に送信されます。
* 位置情報機能により、サービス プロバイダーの保守スタッフは、携帯電話塔の本物の正常性データを管理と共有できます。 管理は、キャプチャされた位置情報とメンテナンス スタッフが送信したデータの不一致を比較できます。

位置情報機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要があります。 効果的な統合を行うには、場所 API を呼び出す [コード スニペット](#code-snippets) をよく理解している必要があります。 Teamsアプリのエラーを処理するには[、API 応答エラー](#error-handling)を理解しておくことが重要です。

> [!NOTE] 
> 現在、位置情報の機能のMicrosoft Teamsサポートは、モバイル クライアントでのみ使用できます。

## <a name="update-manifest"></a>マニフェストの更新

Teamsアプリ[のmanifest.js](../../resources/schema/manifest-schema.md#devicepermissions)を更新するには、プロパティを追加 `devicePermissions` して `geolocation` を指定します。 これにより、位置情報機能を使用する前に、アプリがユーザーに必要なアクセス許可を要求できます。

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> 関連するTeams API が開始されると、[**アクセス許可の要求**] プロンプトが自動的に表示されます。 詳細については、 [デバイスのアクセス許可の要求](native-device-permissions.md)を参照してください。

## <a name="location-apis"></a>ロケーション API

デバイスの位置情報機能を有効にするには、次の API セットを使用する必要があります。

| API      | 説明   |
| --- | --- |
|[場所を取得します。](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | ユーザーの現在のデバイスの場所を指定するか、ネイティブの場所ピッカーを開き、ユーザーが選択した場所を返します。 |
|[ショーロケーション](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | 地図上に場所を表示します。 |

> [!NOTE]

> `getLocation()`API は、次の[入力構成](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true) `allowChooseLocation` と 、 と共に提供されます `showMap` 。 <br/> の値が `allowChooseLocation` *true* の場合、ユーザーは任意の場所を選択できます。<br/>  値が *false* の場合、ユーザーは現在の場所を変更できません。<br/> の値が `showMap` *false* の場合、現在の位置はマップを表示せずにフェッチされます。 `showMap``allowChooseLocation` *true* に設定されている場合は無視されます。

**位置情報機能** 
 ![ の Web アプリ エクスペリエンス位置情報機能の Web アプリ エクスペリエンス](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。 

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | INTERNAL_ERROR | 必要な操作の実行中に内部エラーが発生しました。|
| **1000** | PERMISSION_DENIED |Teams アプリまたは Web アプリに対するユーザーの場所のアクセス許可を拒否しました。|
| **4000** | INVALID_ARGUMENTS | API が、間違った、または不十分な必須引数で呼び出されます。|
| **8000** | USER_ABORT |ユーザーは操作をキャンセルしました。|
| **9000** | OLD_PLATFORM | ユーザーは、API の実装が存在しない古いプラットフォームビルドに存在します。 ビルドをアップグレードすると、問題が解決するはずです。|

## <a name="code-snippets"></a>コード スニペット

**API を呼び出 `getLocation` して場所を取得する:**

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

**API を呼び出 `showLocation` して場所を表示します。**

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

* [Teamsでのメディア機能の統合](mobile-camera-image-permissions.md)
* [qr コードまたはバーコード スキャナー機能をTeamsに統合](qr-barcode-scanner-capability.md)
