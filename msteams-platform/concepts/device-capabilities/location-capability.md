---
title: 場所の機能を統合する
description: Teams JavaScript クライアント SDK を使用して場所の機能を活用する方法
keywords: 場所マップ機能ネイティブ デバイスのアクセス許可
ms.author: lajanuar
ms.openlocfilehash: fccf39c37c785be716bfff26907f9184c0d9beec
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449642"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="10448-104">場所の機能を統合する</span><span class="sxs-lookup"><span data-stu-id="10448-104">Integrate location capabilities</span></span> 

<span data-ttu-id="10448-105">このドキュメントでは、ネイティブ デバイスの位置情報機能を Teams アプリに統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="10448-105">This document guides you on how to integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="10448-106">[アプリがユーザーのネイティブ デバイス](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)機能にアクセスするために必要なツールを提供する Microsoft Teams JavaScript クライアント SDK[を使用できます](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="10448-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="10448-107">[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_)や[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_)などの場所 API を使用して、アプリ内の機能を統合します。</span><span class="sxs-lookup"><span data-stu-id="10448-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) and [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="10448-108">場所機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="10448-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="10448-109">Teams アプリに場所機能を統合する主な利点は、Teams プラットフォーム上の Web アプリ開発者が Microsoft Teams JavaScript クライアント SDK で位置情報機能を活用できるという利点です。</span><span class="sxs-lookup"><span data-stu-id="10448-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="10448-110">次の例は、場所機能の統合がさまざまなシナリオでどのように使用されるのか示しています。</span><span class="sxs-lookup"><span data-stu-id="10448-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="10448-111">工場では、監督者は、工場の近くで自分撮りを取得し、指定されたアプリを介して共有を求め、労働者の出席を追跡できます。</span><span class="sxs-lookup"><span data-stu-id="10448-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="10448-112">場所データもキャプチャされ、画像と共に送信されます。</span><span class="sxs-lookup"><span data-stu-id="10448-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="10448-113">位置情報機能を使用すると、サービス プロバイダーの保守スタッフは、携帯電話の塔の本物の正常性データを管理と共有できます。</span><span class="sxs-lookup"><span data-stu-id="10448-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="10448-114">管理は、キャプチャされた位置情報とメンテナンス スタッフが提出したデータの不一致を比較できます。</span><span class="sxs-lookup"><span data-stu-id="10448-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="10448-115">場所の機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="10448-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="10448-116">効果的な統合を行う場合は、場所[](#code-snippets)API を呼び出すコード スニペットについて理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="10448-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="10448-117">Teams アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="10448-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="10448-118">現在、場所の機能に対する Microsoft Teams のサポートは、モバイル クライアントでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="10448-118">Currently, Microsoft Teams support for location capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="10448-119">マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="10448-119">Update manifest</span></span>

<span data-ttu-id="10448-120">プロパティを追加し [ 、manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions) Teams アプリを更新 `devicePermissions` します `geolocation` 。</span><span class="sxs-lookup"><span data-stu-id="10448-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="10448-121">これにより、アプリは場所機能の使用を開始する前に、ユーザーに必要なアクセス許可を求めできます。</span><span class="sxs-lookup"><span data-stu-id="10448-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="10448-122">関連 **する Teams** API が開始されると、[アクセス許可の要求] プロンプトが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="10448-122">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="10448-123">詳細については、「デバイスのアクセス [許可を要求する」を参照してください](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="10448-123">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="10448-124">場所 API</span><span class="sxs-lookup"><span data-stu-id="10448-124">Location APIs</span></span>

<span data-ttu-id="10448-125">デバイスの位置情報機能を有効にするには、次の API セットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10448-125">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="10448-126">API</span><span class="sxs-lookup"><span data-stu-id="10448-126">API</span></span>      | <span data-ttu-id="10448-127">説明</span><span class="sxs-lookup"><span data-stu-id="10448-127">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="10448-128">getLocation</span><span class="sxs-lookup"><span data-stu-id="10448-128">getLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) | <span data-ttu-id="10448-129">ユーザーの現在のデバイスの場所を指定するか、ネイティブの場所ピッカーを開き、ユーザーが選択した場所を返します。</span><span class="sxs-lookup"><span data-stu-id="10448-129">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="10448-130">showLocation</span><span class="sxs-lookup"><span data-stu-id="10448-130">showLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation) | <span data-ttu-id="10448-131">地図上の場所を表示する</span><span class="sxs-lookup"><span data-stu-id="10448-131">Shows location on map</span></span> |

> [!NOTE]

> <span data-ttu-id="10448-132">`getLocation()`API は、次の入力[構成](https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest)と共に `allowChooseLocation` 提供されます `showMap` 。</span><span class="sxs-lookup"><span data-stu-id="10448-132">The `getLocation()` API comes along with following [input configurations](https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="10448-133">値が true `allowChooseLocation` の *場合*、ユーザーは任意の場所を選択できます。</span><span class="sxs-lookup"><span data-stu-id="10448-133">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="10448-134">値が false の *場合*、ユーザーは現在の場所を変更できません。</span><span class="sxs-lookup"><span data-stu-id="10448-134">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="10448-135">値が false の `showMap` *場合*、現在の場所はマップを表示せずにフェッチされます。</span><span class="sxs-lookup"><span data-stu-id="10448-135">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="10448-136">`showMap` true に設定 `allowChooseLocation` されている場合は無視 *されます*。</span><span class="sxs-lookup"><span data-stu-id="10448-136">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span> 

<span data-ttu-id="10448-137">**場所機能用の Web アプリ エクスペリエンス** 
 ![場所機能の Web アプリ エクスペリエンス](../../assets/images/tabs/location-capability.png)</span><span class="sxs-lookup"><span data-stu-id="10448-137">**Web app experience for location capabilities**
![web app experience for location capabilities](../../assets/images/tabs/location-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="10448-138">エラー処理</span><span class="sxs-lookup"><span data-stu-id="10448-138">Error handling</span></span>

<span data-ttu-id="10448-139">Teams アプリでこれらのエラーを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10448-139">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="10448-140">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="10448-140">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="10448-141">エラー コード</span><span class="sxs-lookup"><span data-stu-id="10448-141">Error code</span></span> |  <span data-ttu-id="10448-142">エラー名</span><span class="sxs-lookup"><span data-stu-id="10448-142">Error name</span></span>     | <span data-ttu-id="10448-143">Condition</span><span class="sxs-lookup"><span data-stu-id="10448-143">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="10448-144">**100**</span><span class="sxs-lookup"><span data-stu-id="10448-144">**100**</span></span> | <span data-ttu-id="10448-145">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="10448-145">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="10448-146">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="10448-146">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="10448-147">**500**</span><span class="sxs-lookup"><span data-stu-id="10448-147">**500**</span></span> | <span data-ttu-id="10448-148">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="10448-148">INTERNAL_ERROR</span></span> | <span data-ttu-id="10448-149">必要な操作の実行中に内部エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="10448-149">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="10448-150">**1000**</span><span class="sxs-lookup"><span data-stu-id="10448-150">**1000**</span></span> | <span data-ttu-id="10448-151">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="10448-151">PERMISSION_DENIED</span></span> |<span data-ttu-id="10448-152">ユーザーが Teams アプリまたは Web アプリに対する場所のアクセス許可を拒否しました。</span><span class="sxs-lookup"><span data-stu-id="10448-152">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="10448-153">**4000**</span><span class="sxs-lookup"><span data-stu-id="10448-153">**4000**</span></span> | <span data-ttu-id="10448-154">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="10448-154">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="10448-155">API は、間違った引数または不十分な必須引数を使用して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="10448-155">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="10448-156">**8000**</span><span class="sxs-lookup"><span data-stu-id="10448-156">**8000**</span></span> | <span data-ttu-id="10448-157">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="10448-157">USER_ABORT</span></span> |<span data-ttu-id="10448-158">ユーザーが操作を取り消しました。</span><span class="sxs-lookup"><span data-stu-id="10448-158">User cancelled the operation.</span></span>|
| <span data-ttu-id="10448-159">**9000**</span><span class="sxs-lookup"><span data-stu-id="10448-159">**9000**</span></span> | <span data-ttu-id="10448-160">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="10448-160">OLD_PLATFORM</span></span> | <span data-ttu-id="10448-161">ユーザーは、API の実装が存在しない古いプラットフォーム ビルドに存在します。</span><span class="sxs-lookup"><span data-stu-id="10448-161">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="10448-162">ビルドをアップグレードすると、問題が解決します。</span><span class="sxs-lookup"><span data-stu-id="10448-162">Upgrading the build should resolve the issue.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="10448-163">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="10448-163">Code snippets</span></span>

<span data-ttu-id="10448-164">**`getLocation`場所を取得する API の呼び出し:**</span><span class="sxs-lookup"><span data-stu-id="10448-164">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="10448-165">**`showLocation`場所を表示する API の呼び出し:**</span><span class="sxs-lookup"><span data-stu-id="10448-165">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="see-also"></a><span data-ttu-id="10448-166">関連項目</span><span class="sxs-lookup"><span data-stu-id="10448-166">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="10448-167">Teams でのメディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="10448-167">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="10448-168">Teams に QR またはバーコード スキャナー機能を統合する</span><span class="sxs-lookup"><span data-stu-id="10448-168">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)