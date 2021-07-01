---
title: 場所機能を統合する
author: Rajeshwari-v
description: JavaScript クライアント SDK Teamsを使用して場所の機能を活用する方法
keywords: 場所マップ機能ネイティブ デバイスのアクセス許可
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 3e6c4bda9a1a0024380cb295cd280db1d630f019
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211612"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="56347-104">場所機能を統合する</span><span class="sxs-lookup"><span data-stu-id="56347-104">Integrate location capabilities</span></span> 

<span data-ttu-id="56347-105">ネイティブ デバイスの位置情報機能は、アプリと統合Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="56347-105">You can integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="56347-106">JavaScript クライアント[SDK Microsoft Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)できます。これは、アプリがユーザーのネイティブ デバイス機能にアクセスするために必要なツール[を提供します](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="56347-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="56347-107">[getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)や[showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true)などの場所 API を使用して、アプリ内の機能を統合します。</span><span class="sxs-lookup"><span data-stu-id="56347-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="56347-108">場所機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="56347-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="56347-109">Teams アプリに場所の機能を統合する主な利点は、Teams プラットフォーム上の Web アプリ開発者が、Microsoft Teams JavaScript クライアント SDK で位置情報機能を活用できるという利点です。</span><span class="sxs-lookup"><span data-stu-id="56347-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="56347-110">次の例は、場所機能の統合がさまざまなシナリオでどのように使用されるのか示しています。</span><span class="sxs-lookup"><span data-stu-id="56347-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="56347-111">工場では、監督者は、工場の近くで自分撮りを取得し、指定されたアプリを介して共有を求め、労働者の出席を追跡できます。</span><span class="sxs-lookup"><span data-stu-id="56347-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="56347-112">場所データもキャプチャされ、画像と共に送信されます。</span><span class="sxs-lookup"><span data-stu-id="56347-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="56347-113">位置情報機能を使用すると、サービス プロバイダーの保守スタッフは、携帯電話の塔の本物の正常性データを管理と共有できます。</span><span class="sxs-lookup"><span data-stu-id="56347-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="56347-114">管理は、キャプチャされた位置情報とメンテナンス スタッフが提出したデータの不一致を比較できます。</span><span class="sxs-lookup"><span data-stu-id="56347-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="56347-115">場所の機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="56347-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="56347-116">効果的な統合を行う場合は、場所[](#code-snippets)API を呼び出すコード スニペットについて理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="56347-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="56347-117">API 応答エラーを理解して、アプリ[](#error-handling)内のエラーを処理することがTeamsです。</span><span class="sxs-lookup"><span data-stu-id="56347-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="56347-118">現在、Microsoft Teams機能のサポートはモバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="56347-118">Currently, Microsoft Teams support for location capabilities is available for mobile clients only.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="56347-119">マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="56347-119">Update manifest</span></span>

<span data-ttu-id="56347-120">プロパティを追加Teamsを[manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions)、ファイル上のアプリ `devicePermissions` のアプリを更新します `geolocation` 。</span><span class="sxs-lookup"><span data-stu-id="56347-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="56347-121">これにより、アプリは場所機能の使用を開始する前に、ユーザーに必要なアクセス許可を求めできます。</span><span class="sxs-lookup"><span data-stu-id="56347-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span> <span data-ttu-id="56347-122">アプリ マニフェストの更新プログラムは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="56347-122">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="56347-123">要求 **のアクセス許可のプロンプト** は、関連する API が開始されるとTeams表示されます。</span><span class="sxs-lookup"><span data-stu-id="56347-123">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="56347-124">詳細については、「デバイスのアクセス [許可を要求する」を参照してください](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="56347-124">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="56347-125">場所 API</span><span class="sxs-lookup"><span data-stu-id="56347-125">Location APIs</span></span>

<span data-ttu-id="56347-126">デバイスの位置情報機能を有効にするには、次の API セットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56347-126">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="56347-127">API</span><span class="sxs-lookup"><span data-stu-id="56347-127">API</span></span>      | <span data-ttu-id="56347-128">説明</span><span class="sxs-lookup"><span data-stu-id="56347-128">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="56347-129">getLocation</span><span class="sxs-lookup"><span data-stu-id="56347-129">getLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="56347-130">ユーザーの現在のデバイスの場所を指定するか、ネイティブの場所ピッカーを開き、ユーザーが選択した場所を返します。</span><span class="sxs-lookup"><span data-stu-id="56347-130">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="56347-131">showLocation</span><span class="sxs-lookup"><span data-stu-id="56347-131">showLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | <span data-ttu-id="56347-132">地図上の場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="56347-132">Shows location on map.</span></span> |

> [!NOTE]
> <span data-ttu-id="56347-133">`getLocation()`API は、次の入力[構成](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)と共に `allowChooseLocation` 提供されます `showMap` 。</span><span class="sxs-lookup"><span data-stu-id="56347-133">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="56347-134">値が true `allowChooseLocation` の *場合*、ユーザーは任意の場所を選択できます。</span><span class="sxs-lookup"><span data-stu-id="56347-134">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="56347-135">値が false の *場合*、ユーザーは現在の場所を変更できません。</span><span class="sxs-lookup"><span data-stu-id="56347-135">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="56347-136">値が false の `showMap` *場合*、現在の場所はマップを表示せずにフェッチされます。</span><span class="sxs-lookup"><span data-stu-id="56347-136">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="56347-137">`showMap` true に設定 `allowChooseLocation` されている場合は無視 *されます*。</span><span class="sxs-lookup"><span data-stu-id="56347-137">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="56347-138">次の図は、場所機能の Web アプリ エクスペリエンスを示しています。</span><span class="sxs-lookup"><span data-stu-id="56347-138">The following image depicts web app experience of location capabilities:</span></span>

![場所機能の Web アプリ エクスペリエンス](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a><span data-ttu-id="56347-140">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="56347-140">Code snippets</span></span>

<span data-ttu-id="56347-141">**`getLocation`場所を取得する API の呼び出し:**</span><span class="sxs-lookup"><span data-stu-id="56347-141">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="56347-142">**`showLocation`場所を表示する API の呼び出し:**</span><span class="sxs-lookup"><span data-stu-id="56347-142">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="error-handling"></a><span data-ttu-id="56347-143">エラー処理</span><span class="sxs-lookup"><span data-stu-id="56347-143">Error handling</span></span>

<span data-ttu-id="56347-144">これらのエラーは、アプリで適切に処理Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="56347-144">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="56347-145">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="56347-145">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="56347-146">エラー コード</span><span class="sxs-lookup"><span data-stu-id="56347-146">Error code</span></span> |  <span data-ttu-id="56347-147">エラー名</span><span class="sxs-lookup"><span data-stu-id="56347-147">Error name</span></span>     | <span data-ttu-id="56347-148">Condition</span><span class="sxs-lookup"><span data-stu-id="56347-148">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="56347-149">**100**</span><span class="sxs-lookup"><span data-stu-id="56347-149">**100**</span></span> | <span data-ttu-id="56347-150">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="56347-150">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="56347-151">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="56347-151">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="56347-152">**500**</span><span class="sxs-lookup"><span data-stu-id="56347-152">**500**</span></span> | <span data-ttu-id="56347-153">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="56347-153">INTERNAL_ERROR</span></span> | <span data-ttu-id="56347-154">必要な操作の実行中に内部エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="56347-154">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="56347-155">**1000**</span><span class="sxs-lookup"><span data-stu-id="56347-155">**1000**</span></span> | <span data-ttu-id="56347-156">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="56347-156">PERMISSION_DENIED</span></span> |<span data-ttu-id="56347-157">ユーザーは、アプリまたは web アプリTeams場所のアクセス許可を拒否しました。</span><span class="sxs-lookup"><span data-stu-id="56347-157">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="56347-158">**4000**</span><span class="sxs-lookup"><span data-stu-id="56347-158">**4000**</span></span> | <span data-ttu-id="56347-159">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="56347-159">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="56347-160">API は、間違った引数または不十分な必須引数を使用して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="56347-160">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="56347-161">**8000**</span><span class="sxs-lookup"><span data-stu-id="56347-161">**8000**</span></span> | <span data-ttu-id="56347-162">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="56347-162">USER_ABORT</span></span> |<span data-ttu-id="56347-163">ユーザーが操作を取り消しました。</span><span class="sxs-lookup"><span data-stu-id="56347-163">User cancelled the operation.</span></span>|
| <span data-ttu-id="56347-164">**9000**</span><span class="sxs-lookup"><span data-stu-id="56347-164">**9000**</span></span> | <span data-ttu-id="56347-165">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="56347-165">OLD_PLATFORM</span></span> | <span data-ttu-id="56347-166">ユーザーは、API の実装が存在しない古いプラットフォーム ビルドに存在します。</span><span class="sxs-lookup"><span data-stu-id="56347-166">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="56347-167">ビルドをアップグレードすると、問題が解決します。</span><span class="sxs-lookup"><span data-stu-id="56347-167">Upgrading the build should resolve the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="56347-168">関連項目</span><span class="sxs-lookup"><span data-stu-id="56347-168">See also</span></span>

* [<span data-ttu-id="56347-169">メディア機能を統合Teams</span><span class="sxs-lookup"><span data-stu-id="56347-169">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="56347-170">QR コードまたはバーコード スキャナー機能をアプリに統合Teams</span><span class="sxs-lookup"><span data-stu-id="56347-170">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="56347-171">ユーザー選択機能をユーザー選択機能にTeams</span><span class="sxs-lookup"><span data-stu-id="56347-171">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)
