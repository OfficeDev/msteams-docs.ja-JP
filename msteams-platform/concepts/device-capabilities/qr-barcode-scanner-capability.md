---
title: QR コードまたはバーコード スキャナー機能を統合する
author: Rajeshwari-v
description: JavaScript クライアント SDK Teams QR またはバーコード スキャナー機能を活用する方法
keywords: カメラ メディア QR コード qrcode バーコード バーコード スキャナー スキャン機能ネイティブ デバイスのアクセス許可
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: c21408ccbca6cd12d37d2066cf50f3468b669012
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888000"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>QR コードまたはバーコード スキャナー機能を統合する

バーコードは、視覚的で機械で読み取り可能な形式でデータを表す方法です。 バーコードには、バーとスペースの形式で、種類、サイズ、製造元、発生国などの製品に関する情報が含まれます。 コードは、ネイティブ デバイス カメラの光学スキャナーを使用して読み取ります。 より豊富な共同作業エクスペリエンスを実現するには、Teams プラットフォームで提供される QR またはバーコード スキャナー機能をアプリTeamsできます。   

JavaScript クライアント[SDK Microsoft Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)できます。これは、アプリがユーザーのネイティブ デバイス機能にアクセスするために必要なツール[を提供します](native-device-permissions.md)。 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API を使用して、スキャナー機能をアプリ内に統合します。

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>QR またはバーコード スキャナー機能を統合する利点

QR またはバーコード スキャナー機能の統合の利点は次のとおりです。 

* この統合により、Web アプリ開発者は、Teams JavaScript クライアント SDK で QR またはバーコードスキャン機能Teams活用できます。
* この機能を使用すると、ユーザーはスキャナー UI の中央にあるフレーム内の QR またはバーコードのみを配置する必要があります。コードは自動的にスキャンされます。 保存されたデータは、呼び出し元の Web アプリと共有されます。 これにより、長い製品コードや他の関連情報を手動で入力する際の不便や人的ミスを回避できます。

QR またはバーコード スキャナー機能を統合するには、アプリ マニフェスト ファイルを更新し [、scanBarCode API を呼び出す必要](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) があります。 統合を効果的に行う場合は、ネイティブ[](#code-snippet)QR またはバーコード スキャナー機能を使用できる[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API を呼び出すコード スニペットについて理解している必要があります。 API では、サポートされていないバーコード標準に対してエラーが発生します。
API 応答エラーを理解して、アプリ[](#error-handling)内のエラーを処理することがTeamsです。

> [!NOTE] 
> 現在、qr Microsoft Teamsバーコード スキャナー機能のサポートは、モバイル クライアントでのみ利用できます。

## <a name="update-manifest"></a>マニフェストの更新

プロパティをTeams指定して、[アプリ manifest.json](../../resources/schema/manifest-schema.md#devicepermissions)ファイル `devicePermissions` を更新します `media` 。 これにより、QR またはバーコード スキャナー機能の使用を開始する前に、アプリでユーザーに必要なアクセス許可を求めできます。 アプリ マニフェストの更新プログラムは次のとおりです。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 要求 **のアクセス許可のプロンプト** は、関連する API が開始されるとTeams表示されます。 詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。

## <a name="scanbarcode-api"></a>ScanBarCode API

[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API は、ユーザーがさまざまな種類のバーコードをスキャンできるスキャナー コントロールを呼び出し、結果を文字列として返します。

バーコードスキャンエクスペリエンスをカスタマイズするために、オプションの [バーコード構成](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) が [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API に入力として渡されます。 を使用して、スキャンのタイム アウト間隔を秒で指定できます `timeOutIntervalInSec` 。 既定値は 30 秒で、最大値は 60 秒です。

**scanBarCode()** API は、次のバーコードの種類をサポートしています。

| バーコードの種類 | Android でサポートされる | iOS でサポート |
| ---------- | ---------- | ------------ |
| Codebar | はい | 不要 |
| コード 39 | はい | はい | 
| コード 93 | はい | はい |
| コード 128 | はい | はい |
| EAN-13 | はい | はい |
| EAN-8 | はい | はい |
| ITF | 不要 | はい |
| QR コード | はい | はい |
| RSS の展開 | はい | 不要 |
| RSS-14 | はい | 不要 |
| UPC-A | はい | はい |
| UPC-E | はい | はい |

次の図は、QR またはバーコード スキャナー機能の Web アプリ エクスペリエンスを示しています。

![Qr またはバーコード スキャナー機能の Web アプリ エクスペリエンス](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>エラー処理

これらのエラーは、アプリで適切に処理Teamsがあります。 次の表に、エラー コードとエラーが生成される条件を示します。 

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | INTERNAL_ERROR | 必要な操作の実行中に内部エラーが発生します。|
| **1000** | PERMISSION_DENIED |アクセス許可は、ユーザーによって拒否されます。|
| **3000** | NO_HW_SUPPORT | 基になるハードウェアでは、この機能はサポートされていません。|
| **4000** | INVALID_ARGUMENTS | いくつかの引数は無効です。|
| **8000** | USER_ABORT |ユーザーは操作を中止します。|
| **8001** | OPERATION_TIMED_OUT | 指定された時間間隔でバーコードを検出できない。|
| **9000** | OLD_PLATFORM | プラットフォーム コードは古く、この API は実装されません。|

## <a name="code-snippet"></a>コード スニペット

**通話 `ScanBarCode()` カメラを** 使用して QR またはバーコードをスキャンする API:

```javascript
const config: microsoftTeams.media.BarCodeConfig = {
  timeOutIntervalInSec: 30};
microsoftTeams.media.scanBarCode((error: microsoftTeams.SdkError, decodedText: string) => {
  if (error) {
    if (error.message) {
      output(" ErrorCode: " + error.errorCode + error.message);
    } else {
      output(" ErrorCode: " + error.errorCode);
    }
  } else if (decodedText) {
    output(decodedText);
  }
}, config);
```

## <a name="see-also"></a>関連項目

* [メディア機能を統合Teams](mobile-camera-image-permissions.md)
* [場所の機能を統合Teams](location-capability.md)
* [[ユーザー選択] を [ユーザー選択] Teams](people-picker-capability.md)
