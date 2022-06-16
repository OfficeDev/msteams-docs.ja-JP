---
title: QR コードまたはバーコード スキャナー機能を統合する
author: Rajeshwari-v
description: Teams JavaScript クライアント SDK を使用して QR またはバーコード スキャナー機能を活用する方法
keywords: カメラ メディア QR コード qrcode バー コード バーコード スキャナースキャン機能ネイティブ デバイスのアクセス許可
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 2dced2abc29ee21e50a3a37ccfed4811102cc8ce
ms.sourcegitcommit: b4986bf529c74444db67b7ce522b3b0d2c2a8e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66130502"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>QR コードまたはバーコード スキャナー機能を統合する

バーコードとは、視覚的でコンピューターが読み取り可能な形式でデータを表す方法です。 バーコードには、種類、サイズ、製造元、国などの製品に関する情報がバーとスペースの形式で含まれています。 コードは、ネイティブ デバイス カメラの光学スキャナーを使用して読み取られます。 より充実した共同作業エクスペリエンスを実現するために、Teams プラットフォームで提供される QR またはバーコード スキャナー機能を Teams アプリと統合できます。

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を使用できます。これは、アプリがユーザーの [ネイティブ デバイス機能](native-device-permissions.md) にアクセスするために必要なツールを提供します。 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API を使用して、スキャナー機能をアプリ内に統合します。

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>QR またはバーコード スキャナー機能を統合する利点

QR またはバーコード スキャナー機能の統合の利点を次に示します。

* この統合により、Teams プラットフォーム上の Web アプリ開発者は、Teams JavaScript クライアント SDK を使用して QR またはバーコード スキャン機能を利用できます。
* この機能を使用すると、ユーザーはスキャナー UI の中央にあるフレーム内の QR またはバーコードのみを配置する必要があり、コードは自動的にスキャンされます。 保存されたデータは、呼び出し元の Web アプリと共有されます。 これにより、長い製品コードやその他の関連情報を手動で入力する際の不便さと人的エラーを回避できます。

QR またはバーコード スキャナー機能を統合するには、アプリ マニフェスト ファイルを更新し、[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API を呼び出す必要があります。 効果的な統合を実現するには、ネイティブ QR またはバーコード スキャナー機能を使用できる [code スニペット](#code-snippet) で [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API を呼び出す方法をよく理解している必要があります。 API では、サポートされていないバーコード標準に対してエラーが発生します。
Teams アプリのエラーを処理するには、[API 応答エラー](#error-handling)を理解しておくことが重要です。

> [!NOTE]
> 現在、Microsoft Teams による QR バーコード スキャナー機能のサポートは、モバイル クライアントでのみ利用できます。

## <a name="update-manifest"></a>マニフェストを更新する

`devicePermissions` プロパティを追加して `media` を指定することにより、Teamsアプリの [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) ファイルを更新します。 これにより、アプリは QR またはバーコード スキャナー機能の使用を開始する前に、ユーザーに必要なアクセス許可を求めることができます。 アプリ マニフェストの更新プログラムは次のとおりです。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> **アクセス許可要求** プロンプトは、関連する Teams API が開始されると自動的に表示されます。 詳細については、「[デバイスのアクセス許可要求](native-device-permissions.md)」 を参照してください。

## <a name="scanbarcode-api"></a>ScanBarCode API

[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API は、ユーザーがさまざまな種類のバーコードをスキャンできるようにするスキャナー コントロールを呼び出し、結果を文字列として返します。

バーコード スキャン エクスペリエンスをカスタマイズするために、省略可能な [バーコード構成](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) が入力として [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API に渡されます。 `timeOutIntervalInSec` を使用して、スキャンタイムアウト間隔を秒単位で指定できます。 既定値は 30 秒で、最大値は 60 秒です。

**scanBarCode()** API では、次のバーコードの種類がサポートされています。

| バーコードの種類 | Android でサポートされています | iOS でサポート: |
| ---------- | ---------- | ------------ |
| コード バー | はい | 不要 |
| コード 39 | はい | はい |
| コード 93 | はい | はい |
| コード 128 | はい | はい |
| EAN-13 | はい | はい |
| EAN-8 | はい | はい |
| ITF | 不要 | はい |
| QR コード | はい | はい |
| RSS は展開されています | はい | 不要 |
| RSS-14 | はい | 不要 |
| UPC-A | はい | はい |
| UPC-E | はい | はい |

次の図は、QR またはバーコード スキャナー機能の Web アプリエクスペリエンスを示しています。

![QR またはバーコード スキャナー機能の Web アプリ エクスペリエンス](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | 内部エラーです(_E) | 必要な操作の実行中に内部エラーが発生しました。|
| **1000** | PERMISSION_DENIED |アクセス許可がユーザーによって拒否されました。|
| **3000** | NO_HW_SUPPORT | 基になるハードウェアでは、この機能はサポートされていません。|
| **4000** | 引数が無効です | いくつかの引数は無効です。|
| **8000** | USER_ABORT |ユーザーが操作を中止します。|
| **8001** | OPERATION_TIMED_OUT | 指定された時間間隔でバーコードを検出できませんでした。|
| **9000** | OLD_PLATFORM | プラットフォーム コードは古く、この API は実装されていません。|

## <a name="code-snippet"></a>コード スニペット

カメラを使用して QR またはバーコードをスキャンするため **で `ScanBarCode()`API** を呼び出しています。

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

* [メディア機能を統合する](media-capabilities.md)
* [Teams で位置情報機能を統合する](location-capability.md)
* [Teams でユーザー ピッカーを統合する](people-picker-capability.md)
