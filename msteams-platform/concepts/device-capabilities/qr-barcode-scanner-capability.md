---
title: QR コードまたはバーコード スキャナー機能を統合する
author: Rajeshwari-v
description: JavaScript クライアント SDK Teams QR またはバーコード スキャナー機能を活用する方法
keywords: カメラ メディア QR コード qrcode バーコード バーコード スキャナー スキャン機能ネイティブ デバイスのアクセス許可
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 9b85de05bea8c9f704f4d8138b041b90e159b10f
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646564"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="a291f-104">QR コードまたはバーコード スキャナー機能を統合する</span><span class="sxs-lookup"><span data-stu-id="a291f-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="a291f-105">このドキュメントでは、QR またはバーコード スキャナー機能を統合する方法についてガイドします。</span><span class="sxs-lookup"><span data-stu-id="a291f-105">This document guides you on how to integrate the QR or barcode scanner capability.</span></span> 

<span data-ttu-id="a291f-106">バーコードは、視覚的で機械で読み取り可能な形式でデータを表す方法です。</span><span class="sxs-lookup"><span data-stu-id="a291f-106">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="a291f-107">バーコードには、バーとスペースの形式で、種類、サイズ、製造元、発生国などの製品に関する情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a291f-107">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="a291f-108">コードは、ネイティブ デバイス カメラの光学スキャナーを使用して読み取ります。</span><span class="sxs-lookup"><span data-stu-id="a291f-108">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="a291f-109">より豊富な共同作業エクスペリエンスを実現するには、Teams プラットフォームで提供される QR またはバーコード スキャナー機能をアプリTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="a291f-109">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span>   

<span data-ttu-id="a291f-110">JavaScript クライアント[SDK Microsoft Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)できます。これは、アプリがユーザーのネイティブ デバイス機能にアクセスするために必要なツール[を提供します](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="a291f-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="a291f-111">[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API を使用して、スキャナー機能をアプリ内に統合します。</span><span class="sxs-lookup"><span data-stu-id="a291f-111">Use the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="a291f-112">QR またはバーコード スキャナー機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="a291f-112">Advantage of integrating QR or barcode scanner capability</span></span>

<span data-ttu-id="a291f-113">QR またはバーコード スキャナー機能の統合の利点は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a291f-113">Following are the advantages of integration of QR or barcode scanner capabilities:</span></span> 

* <span data-ttu-id="a291f-114">この統合により、Web アプリ開発者は、Teams JavaScript クライアント SDK で QR またはバーコードスキャン機能Teams活用できます。</span><span class="sxs-lookup"><span data-stu-id="a291f-114">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="a291f-115">この機能を使用すると、ユーザーはスキャナー UI の中央にあるフレーム内の QR またはバーコードのみを配置する必要があります。コードは自動的にスキャンされます。</span><span class="sxs-lookup"><span data-stu-id="a291f-115">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="a291f-116">保存されたデータは、呼び出し元の Web アプリと共有されます。</span><span class="sxs-lookup"><span data-stu-id="a291f-116">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="a291f-117">これにより、長い製品コードや他の関連情報を手動で入力する際の不便や人的ミスを回避できます。</span><span class="sxs-lookup"><span data-stu-id="a291f-117">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="a291f-118">QR またはバーコード スキャナー機能を統合するには、アプリ マニフェスト ファイルを更新し [、scanBarCode API を呼び出す必要](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) があります。</span><span class="sxs-lookup"><span data-stu-id="a291f-118">To integrate QR or barcode scanner capability, you must update the app manifest file and call the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API.</span></span> <span data-ttu-id="a291f-119">統合を効果的に行う場合は、ネイティブ[](#code-snippet)QR またはバーコード スキャナー機能を使用できる[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API を呼び出すコード スニペットについて理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="a291f-119">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="a291f-120">API では、サポートされていないバーコード標準に対してエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="a291f-120">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="a291f-121">API 応答エラーを理解して、アプリ[](#error-handling)内のエラーを処理することがTeamsです。</span><span class="sxs-lookup"><span data-stu-id="a291f-121">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="a291f-122">現在、qr Microsoft Teamsバーコード スキャナー機能のサポートは、モバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="a291f-122">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="a291f-123">マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="a291f-123">Update manifest</span></span>

<span data-ttu-id="a291f-124">プロパティを追加Teamsを[manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions)、ファイル上のアプリ `devicePermissions` のアプリを更新します `media` 。</span><span class="sxs-lookup"><span data-stu-id="a291f-124">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="a291f-125">これにより、QR またはバーコード スキャナー機能の使用を開始する前に、アプリでユーザーに必要なアクセス許可を求めできます。</span><span class="sxs-lookup"><span data-stu-id="a291f-125">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="a291f-126">要求 **のアクセス許可のプロンプト** は、関連する API が開始されるとTeams表示されます。</span><span class="sxs-lookup"><span data-stu-id="a291f-126">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="a291f-127">詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="a291f-127">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="a291f-128">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="a291f-128">ScanBarCode API</span></span>

<span data-ttu-id="a291f-129">[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API は、ユーザーがさまざまな種類のバーコードをスキャンできるスキャナー コントロールを呼び出し、結果を文字列として返します。</span><span class="sxs-lookup"><span data-stu-id="a291f-129">The [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="a291f-130">バーコードスキャンエクスペリエンスをカスタマイズするために、オプションの [バーコード構成](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) が [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API に入力として渡されます。</span><span class="sxs-lookup"><span data-stu-id="a291f-130">To customize the barcode scanning experience, optional [barcode configuration](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) is passed as input to [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API.</span></span> <span data-ttu-id="a291f-131">を使用して、スキャンのタイム アウト間隔を秒で指定できます `timeOutIntervalInSec` 。</span><span class="sxs-lookup"><span data-stu-id="a291f-131">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="a291f-132">既定値は 30 秒で、最大値は 60 秒です。</span><span class="sxs-lookup"><span data-stu-id="a291f-132">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="a291f-133">**scanBarCode()** API は、次のバーコードの種類をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a291f-133">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="a291f-134">バーコードの種類</span><span class="sxs-lookup"><span data-stu-id="a291f-134">Barcode Type</span></span> | <span data-ttu-id="a291f-135">Android でサポートされる</span><span class="sxs-lookup"><span data-stu-id="a291f-135">Supported on Android</span></span> | <span data-ttu-id="a291f-136">iOS でサポート</span><span class="sxs-lookup"><span data-stu-id="a291f-136">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="a291f-137">Codebar</span><span class="sxs-lookup"><span data-stu-id="a291f-137">Codebar</span></span> | <span data-ttu-id="a291f-138">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-138">Yes</span></span> | <span data-ttu-id="a291f-139">いいえ</span><span class="sxs-lookup"><span data-stu-id="a291f-139">No</span></span> |
| <span data-ttu-id="a291f-140">コード 39</span><span class="sxs-lookup"><span data-stu-id="a291f-140">Code 39</span></span> | <span data-ttu-id="a291f-141">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-141">Yes</span></span> | <span data-ttu-id="a291f-142">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-142">Yes</span></span> | 
| <span data-ttu-id="a291f-143">コード 93</span><span class="sxs-lookup"><span data-stu-id="a291f-143">Code 93</span></span> | <span data-ttu-id="a291f-144">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-144">Yes</span></span> | <span data-ttu-id="a291f-145">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-145">Yes</span></span> |
| <span data-ttu-id="a291f-146">コード 128</span><span class="sxs-lookup"><span data-stu-id="a291f-146">Code 128</span></span> | <span data-ttu-id="a291f-147">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-147">Yes</span></span> | <span data-ttu-id="a291f-148">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-148">Yes</span></span> |
| <span data-ttu-id="a291f-149">EAN-13</span><span class="sxs-lookup"><span data-stu-id="a291f-149">EAN-13</span></span> | <span data-ttu-id="a291f-150">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-150">Yes</span></span> | <span data-ttu-id="a291f-151">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-151">Yes</span></span> |
| <span data-ttu-id="a291f-152">EAN-8</span><span class="sxs-lookup"><span data-stu-id="a291f-152">EAN-8</span></span> | <span data-ttu-id="a291f-153">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-153">Yes</span></span> | <span data-ttu-id="a291f-154">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-154">Yes</span></span> |
| <span data-ttu-id="a291f-155">ITF</span><span class="sxs-lookup"><span data-stu-id="a291f-155">ITF</span></span> | <span data-ttu-id="a291f-156">いいえ</span><span class="sxs-lookup"><span data-stu-id="a291f-156">No</span></span> | <span data-ttu-id="a291f-157">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-157">Yes</span></span> |
| <span data-ttu-id="a291f-158">QR コード</span><span class="sxs-lookup"><span data-stu-id="a291f-158">QR Code</span></span> | <span data-ttu-id="a291f-159">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-159">Yes</span></span> | <span data-ttu-id="a291f-160">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-160">Yes</span></span> |
| <span data-ttu-id="a291f-161">RSS の展開</span><span class="sxs-lookup"><span data-stu-id="a291f-161">RSS Expanded</span></span> | <span data-ttu-id="a291f-162">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-162">Yes</span></span> | <span data-ttu-id="a291f-163">いいえ</span><span class="sxs-lookup"><span data-stu-id="a291f-163">No</span></span> |
| <span data-ttu-id="a291f-164">RSS-14</span><span class="sxs-lookup"><span data-stu-id="a291f-164">RSS-14</span></span> | <span data-ttu-id="a291f-165">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-165">Yes</span></span> | <span data-ttu-id="a291f-166">いいえ</span><span class="sxs-lookup"><span data-stu-id="a291f-166">No</span></span> |
| <span data-ttu-id="a291f-167">UPC-A</span><span class="sxs-lookup"><span data-stu-id="a291f-167">UPC-A</span></span> | <span data-ttu-id="a291f-168">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-168">Yes</span></span> | <span data-ttu-id="a291f-169">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-169">Yes</span></span> |
| <span data-ttu-id="a291f-170">UPC-E</span><span class="sxs-lookup"><span data-stu-id="a291f-170">UPC-E</span></span> | <span data-ttu-id="a291f-171">はい</span><span class="sxs-lookup"><span data-stu-id="a291f-171">Yes</span></span> | <span data-ttu-id="a291f-172">必要</span><span class="sxs-lookup"><span data-stu-id="a291f-172">Yes</span></span> |

<span data-ttu-id="a291f-173">**Web アプリエクスペリエンス `ScanBarCode`QR またはバーコード スキャナー機能の API QR** またはバーコード スキャナー機能の 
 ![ Web アプリ エクスペリエンス](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="a291f-173">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="a291f-174">エラー処理</span><span class="sxs-lookup"><span data-stu-id="a291f-174">Error handling</span></span>

<span data-ttu-id="a291f-175">これらのエラーは、アプリで適切に処理Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="a291f-175">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="a291f-176">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="a291f-176">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="a291f-177">エラー コード</span><span class="sxs-lookup"><span data-stu-id="a291f-177">Error code</span></span> |  <span data-ttu-id="a291f-178">エラー名</span><span class="sxs-lookup"><span data-stu-id="a291f-178">Error name</span></span>     | <span data-ttu-id="a291f-179">条件</span><span class="sxs-lookup"><span data-stu-id="a291f-179">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="a291f-180">**100**</span><span class="sxs-lookup"><span data-stu-id="a291f-180">**100**</span></span> | <span data-ttu-id="a291f-181">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="a291f-181">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="a291f-182">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a291f-182">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="a291f-183">**500**</span><span class="sxs-lookup"><span data-stu-id="a291f-183">**500**</span></span> | <span data-ttu-id="a291f-184">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="a291f-184">INTERNAL_ERROR</span></span> | <span data-ttu-id="a291f-185">必要な操作の実行中に内部エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="a291f-185">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="a291f-186">**1000**</span><span class="sxs-lookup"><span data-stu-id="a291f-186">**1000**</span></span> | <span data-ttu-id="a291f-187">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="a291f-187">PERMISSION_DENIED</span></span> |<span data-ttu-id="a291f-188">アクセス許可は、ユーザーによって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="a291f-188">Permission is denied by the user.</span></span>|
| <span data-ttu-id="a291f-189">**3000**</span><span class="sxs-lookup"><span data-stu-id="a291f-189">**3000**</span></span> | <span data-ttu-id="a291f-190">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="a291f-190">NO_HW_SUPPORT</span></span> | <span data-ttu-id="a291f-191">基になるハードウェアでは、この機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a291f-191">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="a291f-192">**4000**</span><span class="sxs-lookup"><span data-stu-id="a291f-192">**4000**</span></span> | <span data-ttu-id="a291f-193">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="a291f-193">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="a291f-194">いくつかの引数は無効です。</span><span class="sxs-lookup"><span data-stu-id="a291f-194">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="a291f-195">**8000**</span><span class="sxs-lookup"><span data-stu-id="a291f-195">**8000**</span></span> | <span data-ttu-id="a291f-196">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="a291f-196">USER_ABORT</span></span> |<span data-ttu-id="a291f-197">ユーザーは操作を中止します。</span><span class="sxs-lookup"><span data-stu-id="a291f-197">User aborts the operation.</span></span>|
| <span data-ttu-id="a291f-198">**8001**</span><span class="sxs-lookup"><span data-stu-id="a291f-198">**8001**</span></span> | <span data-ttu-id="a291f-199">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="a291f-199">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="a291f-200">指定された時間間隔でバーコードを検出できない。</span><span class="sxs-lookup"><span data-stu-id="a291f-200">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="a291f-201">**9000**</span><span class="sxs-lookup"><span data-stu-id="a291f-201">**9000**</span></span> | <span data-ttu-id="a291f-202">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="a291f-202">OLD_PLATFORM</span></span> | <span data-ttu-id="a291f-203">プラットフォーム コードは古く、この API は実装されません。</span><span class="sxs-lookup"><span data-stu-id="a291f-203">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="a291f-204">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="a291f-204">Code snippet</span></span>

<span data-ttu-id="a291f-205">**通話 `ScanBarCode()` カメラを** 使用して QR またはバーコードをスキャンする API:</span><span class="sxs-lookup"><span data-stu-id="a291f-205">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="a291f-206">関連項目</span><span class="sxs-lookup"><span data-stu-id="a291f-206">See also</span></span>

* [<span data-ttu-id="a291f-207">メディア機能を統合Teams</span><span class="sxs-lookup"><span data-stu-id="a291f-207">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="a291f-208">場所の機能を統合Teams</span><span class="sxs-lookup"><span data-stu-id="a291f-208">Integrate location capabilities in Teams</span></span>](location-capability.md)
