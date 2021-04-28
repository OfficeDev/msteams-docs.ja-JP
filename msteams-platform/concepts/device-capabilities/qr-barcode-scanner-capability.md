---
title: QR コードまたはバーコード スキャナー機能を統合する
author: Rajeshwari-v
description: Teams JavaScript クライアント SDK を使用して QR またはバーコード スキャナー機能を活用する方法
keywords: カメラ メディア QR コード qrcode バーコード バーコード スキャナー スキャン機能ネイティブ デバイスのアクセス許可
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: ede791a6cd566a0fc725a04e0b615ae1b8eeb0eb
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058342"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>QR コードまたはバーコード スキャナー機能を統合する 

このドキュメントでは、QR またはバーコード スキャナー機能を統合する方法についてガイドします。 

バーコードは、視覚的で機械で読み取り可能な形式でデータを表す方法です。 バーコードには、バーとスペースの形式で、種類、サイズ、製造元、発生国などの製品に関する情報が含まれます。 コードは、ネイティブ デバイス カメラの光学スキャナーを使用して読み取ります。 より豊富な共同作業エクスペリエンスを実現するには、Teams プラットフォームで提供される QR またはバーコード スキャナー機能を Teams アプリと統合できます。   

[アプリがユーザーのネイティブ デバイス](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)機能にアクセスするために必要なツールを提供する Microsoft Teams JavaScript クライアント SDK[を使用できます](native-device-permissions.md)。 API を `scanBarCode` 使用して、スキャナー機能をアプリ内に統合します。 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>QR またはバーコード スキャナー機能を統合する利点

QR またはバーコード スキャナー機能の統合の利点は次のとおりです。 

* この統合により、Teams プラットフォーム上の Web アプリ開発者は、Teams JavaScript クライアント SDK で QR またはバーコードスキャン機能を利用できます。
* この機能を使用すると、ユーザーはスキャナー UI の中央にあるフレーム内の QR またはバーコードのみを配置する必要があります。コードは自動的にスキャンされます。 保存されたデータは、呼び出し元の Web アプリと共有されます。 これにより、長い製品コードや他の関連情報を手動で入力する際の不便や人的ミスを回避できます。

QR またはバーコード スキャナー機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要 `scanBarCode` があります。 統合を効果的に行う場合は、ネイティブ[](#code-snippet)QR またはバーコード スキャナー機能を使用できる API を呼び出すコード スニペットについて理解している `scanBarCode` 必要があります。 API では、サポートされていないバーコード標準に対してエラーが発生します。
Teams アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。

> [!NOTE] 
> 現在、Microsoft Teams の QR またはバーコード スキャナー機能のサポートは、モバイル クライアントでのみ使用できます。

## <a name="update-manifest"></a>マニフェストの更新

プロパティを追加し [ 、manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions) Teams アプリを更新 `devicePermissions` します `media` 。 これにより、QR またはバーコード スキャナー機能の使用を開始する前に、アプリでユーザーに必要なアクセス許可を求めできます。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 関連 **する Teams** API が開始されると、[アクセス許可の要求] プロンプトが自動的に表示されます。 詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。

## <a name="scanbarcode-api"></a>ScanBarCode API

API は、ユーザーがさまざまな種類のバーコードをスキャンできるスキャナー コントロールを呼び出し、結果を `ScanBarCode` 文字列として返します。

バーコードスキャンエクスペリエンスをカスタマイズするために、オプションのバーコード構成が API への入力として渡 `ScanBarCode` されます。 を使用して、スキャンのタイム アウト間隔を秒で指定できます `timeOutIntervalInSec` 。 既定値は 30 秒で、最大値は 60 秒です。

**scanBarCode()** API は、次のバーコードの種類をサポートしています。

| バーコードの種類 | Android でサポートされる | iOS でサポート |
| ---------- | ---------- | ------------ |
| Codebar | はい | いいえ |
| コード 39 | はい | はい | 
| コード 93 | はい | はい |
| コード 128 | はい | はい |
| EAN-13 | はい | はい |
| EAN-8 | はい | はい |
| ITF | いいえ | はい |
| QR コード | はい | はい |
| RSS の展開 | はい | いいえ |
| RSS-14 | はい | いいえ |
| UPC-A | はい | はい |
| UPC-E | はい | はい |

**Web アプリエクスペリエンス `ScanBarCode`QR またはバーコード スキャナー機能の API QR** またはバーコード スキャナー機能の 
 ![ Web アプリ エクスペリエンス](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。 

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

- [Teams でのメディア機能の統合](mobile-camera-image-permissions.md)

- [Teams での場所機能の統合](location-capability.md)
