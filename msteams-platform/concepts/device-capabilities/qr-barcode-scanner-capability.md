---
title: QR またはバーコード スキャナーの機能を統合する
description: Teams JavaScript クライアント SDK を使用して QR またはバーコード スキャナー機能を活用する方法
keywords: カメラ メディア QR コード qrcode バーコード バーコード スキャナー スキャン機能ネイティブ デバイスのアクセス許可
ms.author: lajanuar
ms.openlocfilehash: 048c6b58fc126d1dd08867605784b6a150737195
ms.sourcegitcommit: 0bb6efb3003a1949288e4601e3301b69e67d4c26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2021
ms.locfileid: "50295090"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="46dc5-104">QR またはバーコード スキャナーの機能を統合する</span><span class="sxs-lookup"><span data-stu-id="46dc5-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="46dc5-105">バーコードは、視覚的で機械で読み取り可能な形式でデータを表す方法です。</span><span class="sxs-lookup"><span data-stu-id="46dc5-105">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="46dc5-106">バーコードには、バーとスペースの形式で、種類、サイズ、製造元、発生国などの製品に関する情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-106">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="46dc5-107">コードは、ネイティブ デバイス カメラの光学スキャナーを使用して読み取ります。</span><span class="sxs-lookup"><span data-stu-id="46dc5-107">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="46dc5-108">より豊富な共同作業エクスペリエンスを実現するには、Teams プラットフォームで提供される QR またはバーコード スキャナー機能を Teams アプリと統合できます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-108">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span> <span data-ttu-id="46dc5-109">このドキュメントでは、機能を統合する方法についてガイドします。</span><span class="sxs-lookup"><span data-stu-id="46dc5-109">This document guides you on how to integrate the capability.</span></span>  

<span data-ttu-id="46dc5-110">[アプリがユーザーのネイティブ デバイス](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)機能にアクセスするために必要なツールを提供する Microsoft Teams JavaScript クライアント SDK[を使用できます](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="46dc5-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="46dc5-111">API を `scanBarCode` 使用して、スキャナー機能をアプリ内に統合します。</span><span class="sxs-lookup"><span data-stu-id="46dc5-111">Use the `scanBarCode` API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="46dc5-112">QR またはバーコード スキャナー機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="46dc5-112">Advantage of integrating QR or barcode scanner capability</span></span>

* <span data-ttu-id="46dc5-113">この統合により、Teams プラットフォーム上の Web アプリ開発者は、Teams JavaScript クライアント SDK で QR またはバーコードスキャン機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-113">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="46dc5-114">この機能を使用すると、ユーザーはスキャナー UI の中央にあるフレーム内の QR またはバーコードのみを配置する必要があります。コードは自動的にスキャンされます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-114">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="46dc5-115">保存されたデータは、呼び出し元の Web アプリと共有されます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-115">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="46dc5-116">これにより、長い製品コードや他の関連情報を手動で入力する際の不便や人的ミスを回避できます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-116">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="46dc5-117">QR またはバーコード スキャナー機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要 `scanBarCode` があります。</span><span class="sxs-lookup"><span data-stu-id="46dc5-117">To integrate QR or barcode scanner capability, you must update the app manifest file and call the `scanBarCode` API.</span></span> <span data-ttu-id="46dc5-118">統合を効果的に行う場合は、ネイティブ[](#code-snippet)QR またはバーコード スキャナー機能を使用できる API を呼び出すコード スニペットについて理解している `scanBarCode` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="46dc5-118">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the `scanBarCode` API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="46dc5-119">API では、サポートされていないバーコード標準に対してエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="46dc5-119">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="46dc5-120">Teams アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="46dc5-120">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="46dc5-121">現在、Microsoft Teams の QR またはバーコード スキャナー機能のサポートは、モバイル クライアントでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-121">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="46dc5-122">マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="46dc5-122">Update manifest</span></span>

<span data-ttu-id="46dc5-123">プロパティを追加し [ 、manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions) Teams アプリを更新 `devicePermissions` します `media` 。</span><span class="sxs-lookup"><span data-stu-id="46dc5-123">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="46dc5-124">これにより、QR またはバーコード スキャナー機能の使用を開始する前に、アプリでユーザーに必要なアクセス許可を求めできます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-124">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="46dc5-125">関連 **する Teams** API が開始されると、[アクセス許可の要求] プロンプトが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-125">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="46dc5-126">詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="46dc5-126">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="46dc5-127">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="46dc5-127">ScanBarCode API</span></span>

<span data-ttu-id="46dc5-128">API は、ユーザーがさまざまな種類のバーコードをスキャンできるスキャナー コントロールを呼び出し、結果を `ScanBarCode` 文字列として返します。</span><span class="sxs-lookup"><span data-stu-id="46dc5-128">The `ScanBarCode` API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="46dc5-129">バーコードスキャンエクスペリエンスをカスタマイズするために、オプションのバーコード構成が API への入力として渡 `ScanBarCode` されます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-129">To customize the barcode scanning experience, optional barcode configuration is passed as input to `ScanBarCode` API.</span></span> <span data-ttu-id="46dc5-130">を使用して、スキャンのタイム アウト間隔を秒で指定できます `timeOutIntervalInSec` 。</span><span class="sxs-lookup"><span data-stu-id="46dc5-130">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="46dc5-131">既定値は 30 秒で、最大値は 60 秒です。</span><span class="sxs-lookup"><span data-stu-id="46dc5-131">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="46dc5-132">**scanBarCode()** API は、次のバーコードの種類をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="46dc5-132">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="46dc5-133">バーコードの種類</span><span class="sxs-lookup"><span data-stu-id="46dc5-133">Barcode Type</span></span> | <span data-ttu-id="46dc5-134">Android でサポート</span><span class="sxs-lookup"><span data-stu-id="46dc5-134">Supported on Android</span></span> | <span data-ttu-id="46dc5-135">iOS でサポート</span><span class="sxs-lookup"><span data-stu-id="46dc5-135">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="46dc5-136">Codebar</span><span class="sxs-lookup"><span data-stu-id="46dc5-136">Codebar</span></span> | <span data-ttu-id="46dc5-137">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-137">Yes</span></span> | <span data-ttu-id="46dc5-138">いいえ</span><span class="sxs-lookup"><span data-stu-id="46dc5-138">No</span></span> |
| <span data-ttu-id="46dc5-139">コード 39</span><span class="sxs-lookup"><span data-stu-id="46dc5-139">Code 39</span></span> | <span data-ttu-id="46dc5-140">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-140">Yes</span></span> | <span data-ttu-id="46dc5-141">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-141">Yes</span></span> | 
| <span data-ttu-id="46dc5-142">コード 93</span><span class="sxs-lookup"><span data-stu-id="46dc5-142">Code 93</span></span> | <span data-ttu-id="46dc5-143">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-143">Yes</span></span> | <span data-ttu-id="46dc5-144">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-144">Yes</span></span> |
| <span data-ttu-id="46dc5-145">コード 128</span><span class="sxs-lookup"><span data-stu-id="46dc5-145">Code 128</span></span> | <span data-ttu-id="46dc5-146">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-146">Yes</span></span> | <span data-ttu-id="46dc5-147">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-147">Yes</span></span> |
| <span data-ttu-id="46dc5-148">EAN-13</span><span class="sxs-lookup"><span data-stu-id="46dc5-148">EAN-13</span></span> | <span data-ttu-id="46dc5-149">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-149">Yes</span></span> | <span data-ttu-id="46dc5-150">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-150">Yes</span></span> |
| <span data-ttu-id="46dc5-151">EAN-8</span><span class="sxs-lookup"><span data-stu-id="46dc5-151">EAN-8</span></span> | <span data-ttu-id="46dc5-152">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-152">Yes</span></span> | <span data-ttu-id="46dc5-153">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-153">Yes</span></span> |
| <span data-ttu-id="46dc5-154">ITF</span><span class="sxs-lookup"><span data-stu-id="46dc5-154">ITF</span></span> | <span data-ttu-id="46dc5-155">いいえ</span><span class="sxs-lookup"><span data-stu-id="46dc5-155">No</span></span> | <span data-ttu-id="46dc5-156">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-156">Yes</span></span> |
| <span data-ttu-id="46dc5-157">QR コード</span><span class="sxs-lookup"><span data-stu-id="46dc5-157">QR Code</span></span> | <span data-ttu-id="46dc5-158">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-158">Yes</span></span> | <span data-ttu-id="46dc5-159">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-159">Yes</span></span> |
| <span data-ttu-id="46dc5-160">RSS の展開</span><span class="sxs-lookup"><span data-stu-id="46dc5-160">RSS Expanded</span></span> | <span data-ttu-id="46dc5-161">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-161">Yes</span></span> | <span data-ttu-id="46dc5-162">いいえ</span><span class="sxs-lookup"><span data-stu-id="46dc5-162">No</span></span> |
| <span data-ttu-id="46dc5-163">RSS-14</span><span class="sxs-lookup"><span data-stu-id="46dc5-163">RSS-14</span></span> | <span data-ttu-id="46dc5-164">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-164">Yes</span></span> | <span data-ttu-id="46dc5-165">いいえ</span><span class="sxs-lookup"><span data-stu-id="46dc5-165">No</span></span> |
| <span data-ttu-id="46dc5-166">UPC-A</span><span class="sxs-lookup"><span data-stu-id="46dc5-166">UPC-A</span></span> | <span data-ttu-id="46dc5-167">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-167">Yes</span></span> | <span data-ttu-id="46dc5-168">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-168">Yes</span></span> |
| <span data-ttu-id="46dc5-169">UPC-E</span><span class="sxs-lookup"><span data-stu-id="46dc5-169">UPC-E</span></span> | <span data-ttu-id="46dc5-170">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-170">Yes</span></span> | <span data-ttu-id="46dc5-171">はい</span><span class="sxs-lookup"><span data-stu-id="46dc5-171">Yes</span></span> |

<span data-ttu-id="46dc5-172">**Web アプリエクスペリエンス `ScanBarCode`QR またはバーコード スキャナー機能の API QR** またはバーコード スキャナー機能の 
 ![ Web アプリ エクスペリエンス](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="46dc5-172">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="46dc5-173">エラー処理</span><span class="sxs-lookup"><span data-stu-id="46dc5-173">Error handling</span></span>

<span data-ttu-id="46dc5-174">Teams アプリでこれらのエラーを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="46dc5-174">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="46dc5-175">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="46dc5-175">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="46dc5-176">エラー コード</span><span class="sxs-lookup"><span data-stu-id="46dc5-176">Error code</span></span> |  <span data-ttu-id="46dc5-177">エラー名</span><span class="sxs-lookup"><span data-stu-id="46dc5-177">Error name</span></span>     | <span data-ttu-id="46dc5-178">Condition</span><span class="sxs-lookup"><span data-stu-id="46dc5-178">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="46dc5-179">**100**</span><span class="sxs-lookup"><span data-stu-id="46dc5-179">**100**</span></span> | <span data-ttu-id="46dc5-180">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="46dc5-180">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="46dc5-181">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="46dc5-181">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="46dc5-182">**500**</span><span class="sxs-lookup"><span data-stu-id="46dc5-182">**500**</span></span> | <span data-ttu-id="46dc5-183">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="46dc5-183">INTERNAL_ERROR</span></span> | <span data-ttu-id="46dc5-184">必要な操作の実行中に内部エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="46dc5-184">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="46dc5-185">**1000**</span><span class="sxs-lookup"><span data-stu-id="46dc5-185">**1000**</span></span> | <span data-ttu-id="46dc5-186">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="46dc5-186">PERMISSION_DENIED</span></span> |<span data-ttu-id="46dc5-187">アクセス許可は、ユーザーによって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="46dc5-187">Permission is denied by the user.</span></span>|
| <span data-ttu-id="46dc5-188">**3000**</span><span class="sxs-lookup"><span data-stu-id="46dc5-188">**3000**</span></span> | <span data-ttu-id="46dc5-189">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="46dc5-189">NO_HW_SUPPORT</span></span> | <span data-ttu-id="46dc5-190">基になるハードウェアでは、この機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="46dc5-190">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="46dc5-191">**4000**</span><span class="sxs-lookup"><span data-stu-id="46dc5-191">**4000**</span></span> | <span data-ttu-id="46dc5-192">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="46dc5-192">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="46dc5-193">いくつかの引数は無効です。</span><span class="sxs-lookup"><span data-stu-id="46dc5-193">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="46dc5-194">**8000**</span><span class="sxs-lookup"><span data-stu-id="46dc5-194">**8000**</span></span> | <span data-ttu-id="46dc5-195">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="46dc5-195">USER_ABORT</span></span> |<span data-ttu-id="46dc5-196">ユーザーは操作を中止します。</span><span class="sxs-lookup"><span data-stu-id="46dc5-196">User aborts the operation.</span></span>|
| <span data-ttu-id="46dc5-197">**8001**</span><span class="sxs-lookup"><span data-stu-id="46dc5-197">**8001**</span></span> | <span data-ttu-id="46dc5-198">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="46dc5-198">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="46dc5-199">指定された時間間隔でバーコードを検出できない。</span><span class="sxs-lookup"><span data-stu-id="46dc5-199">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="46dc5-200">**9000**</span><span class="sxs-lookup"><span data-stu-id="46dc5-200">**9000**</span></span> | <span data-ttu-id="46dc5-201">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="46dc5-201">OLD_PLATFORM</span></span> | <span data-ttu-id="46dc5-202">プラットフォーム コードは古く、この API は実装されません。</span><span class="sxs-lookup"><span data-stu-id="46dc5-202">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="46dc5-203">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="46dc5-203">Code snippet</span></span>

<span data-ttu-id="46dc5-204">**通話 `ScanBarCode()` カメラを** 使用して QR またはバーコードをスキャンする API:</span><span class="sxs-lookup"><span data-stu-id="46dc5-204">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="46dc5-205">関連項目</span><span class="sxs-lookup"><span data-stu-id="46dc5-205">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46dc5-206">Teams でのメディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="46dc5-206">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
