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
# <a name="integrate-location-capabilities"></a><span data-ttu-id="fccf3-104">場所機能を統合する</span><span class="sxs-lookup"><span data-stu-id="fccf3-104">Integrate location capabilities</span></span> 

<span data-ttu-id="fccf3-105">このドキュメントでは、ネイティブ デバイスの位置情報機能をTeams アプリに統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-105">This document guides you on how to integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="fccf3-106">[JavaScript クライアント SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)使用すると、アプリがユーザーのネイティブ[デバイス機能](native-device-permissions.md)にアクセスするために必要なツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="fccf3-107">[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)や[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true)などの場所 API を使用して、アプリ内の機能を統合します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="fccf3-108">ロケーション機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="fccf3-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="fccf3-109">Teams アプリに位置情報機能を統合する主な利点は、Teams プラットフォーム上の Web アプリ開発者が、Microsoft Teams JavaScript クライアント SDK を使用して位置情報機能を活用できることです。</span><span class="sxs-lookup"><span data-stu-id="fccf3-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="fccf3-110">次の例は、さまざまなシナリオで場所機能の統合がどのように使用されているかを示しています。</span><span class="sxs-lookup"><span data-stu-id="fccf3-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="fccf3-111">工場では、スーパーバイザーは、工場の近くで自分撮りを取り、指定されたアプリを介してそれを共有するように求めることによって、労働者の出席を追跡することができます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="fccf3-112">ロケーションデータもキャプチャされ、画像と一緒に送信されます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="fccf3-113">位置情報機能により、サービス プロバイダーの保守スタッフは、携帯電話塔の本物の正常性データを管理と共有できます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="fccf3-114">管理は、キャプチャされた位置情報とメンテナンス スタッフが送信したデータの不一致を比較できます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="fccf3-115">位置情報機能を統合するには、アプリ マニフェスト ファイルを更新して API を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="fccf3-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="fccf3-116">効果的な統合を行うには、場所 API を呼び出す [コード スニペット](#code-snippets) をよく理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="fccf3-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="fccf3-117">Teamsアプリのエラーを処理するには[、API 応答エラー](#error-handling)を理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="fccf3-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="fccf3-118">現在、位置情報の機能のMicrosoft Teamsサポートは、モバイル クライアントでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-118">Currently, Microsoft Teams support for location capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="fccf3-119">マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="fccf3-119">Update manifest</span></span>

<span data-ttu-id="fccf3-120">Teamsアプリ[のmanifest.js](../../resources/schema/manifest-schema.md#devicepermissions)を更新するには、プロパティを追加 `devicePermissions` して `geolocation` を指定します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="fccf3-121">これにより、位置情報機能を使用する前に、アプリがユーザーに必要なアクセス許可を要求できます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="fccf3-122">関連するTeams API が開始されると、[**アクセス許可の要求**] プロンプトが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-122">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="fccf3-123">詳細については、 [デバイスのアクセス許可の要求](native-device-permissions.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fccf3-123">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="fccf3-124">ロケーション API</span><span class="sxs-lookup"><span data-stu-id="fccf3-124">Location APIs</span></span>

<span data-ttu-id="fccf3-125">デバイスの位置情報機能を有効にするには、次の API セットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fccf3-125">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="fccf3-126">API</span><span class="sxs-lookup"><span data-stu-id="fccf3-126">API</span></span>      | <span data-ttu-id="fccf3-127">説明</span><span class="sxs-lookup"><span data-stu-id="fccf3-127">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="fccf3-128">場所を取得します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-128">getLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="fccf3-129">ユーザーの現在のデバイスの場所を指定するか、ネイティブの場所ピッカーを開き、ユーザーが選択した場所を返します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-129">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="fccf3-130">ショーロケーション</span><span class="sxs-lookup"><span data-stu-id="fccf3-130">showLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | <span data-ttu-id="fccf3-131">地図上に場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-131">Shows location on map.</span></span> |

> [!NOTE]

> <span data-ttu-id="fccf3-132">`getLocation()`API は、次の[入力構成](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true) `allowChooseLocation` と 、 と共に提供されます `showMap` 。</span><span class="sxs-lookup"><span data-stu-id="fccf3-132">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="fccf3-133">の値が `allowChooseLocation` *true* の場合、ユーザーは任意の場所を選択できます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-133">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="fccf3-134">値が *false* の場合、ユーザーは現在の場所を変更できません。</span><span class="sxs-lookup"><span data-stu-id="fccf3-134">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="fccf3-135">の値が `showMap` *false* の場合、現在の位置はマップを表示せずにフェッチされます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-135">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="fccf3-136">`showMap``allowChooseLocation` *true* に設定されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-136">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="fccf3-137">**位置情報機能** 
 ![ の Web アプリ エクスペリエンス位置情報機能の Web アプリ エクスペリエンス](../../assets/images/tabs/location-capability.png)</span><span class="sxs-lookup"><span data-stu-id="fccf3-137">**Web app experience for location capabilities**
![web app experience for location capabilities](../../assets/images/tabs/location-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="fccf3-138">エラー処理</span><span class="sxs-lookup"><span data-stu-id="fccf3-138">Error handling</span></span>

<span data-ttu-id="fccf3-139">Teams アプリでこれらのエラーを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fccf3-139">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="fccf3-140">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-140">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="fccf3-141">エラー コード</span><span class="sxs-lookup"><span data-stu-id="fccf3-141">Error code</span></span> |  <span data-ttu-id="fccf3-142">エラー名</span><span class="sxs-lookup"><span data-stu-id="fccf3-142">Error name</span></span>     | <span data-ttu-id="fccf3-143">条件</span><span class="sxs-lookup"><span data-stu-id="fccf3-143">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="fccf3-144">**100**</span><span class="sxs-lookup"><span data-stu-id="fccf3-144">**100**</span></span> | <span data-ttu-id="fccf3-145">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fccf3-145">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="fccf3-146">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="fccf3-146">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="fccf3-147">**500**</span><span class="sxs-lookup"><span data-stu-id="fccf3-147">**500**</span></span> | <span data-ttu-id="fccf3-148">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="fccf3-148">INTERNAL_ERROR</span></span> | <span data-ttu-id="fccf3-149">必要な操作の実行中に内部エラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="fccf3-149">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="fccf3-150">**1000**</span><span class="sxs-lookup"><span data-stu-id="fccf3-150">**1000**</span></span> | <span data-ttu-id="fccf3-151">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="fccf3-151">PERMISSION_DENIED</span></span> |<span data-ttu-id="fccf3-152">Teams アプリまたは Web アプリに対するユーザーの場所のアクセス許可を拒否しました。</span><span class="sxs-lookup"><span data-stu-id="fccf3-152">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="fccf3-153">**4000**</span><span class="sxs-lookup"><span data-stu-id="fccf3-153">**4000**</span></span> | <span data-ttu-id="fccf3-154">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="fccf3-154">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="fccf3-155">API が、間違った、または不十分な必須引数で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="fccf3-155">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="fccf3-156">**8000**</span><span class="sxs-lookup"><span data-stu-id="fccf3-156">**8000**</span></span> | <span data-ttu-id="fccf3-157">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="fccf3-157">USER_ABORT</span></span> |<span data-ttu-id="fccf3-158">ユーザーは操作をキャンセルしました。</span><span class="sxs-lookup"><span data-stu-id="fccf3-158">User cancelled the operation.</span></span>|
| <span data-ttu-id="fccf3-159">**9000**</span><span class="sxs-lookup"><span data-stu-id="fccf3-159">**9000**</span></span> | <span data-ttu-id="fccf3-160">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fccf3-160">OLD_PLATFORM</span></span> | <span data-ttu-id="fccf3-161">ユーザーは、API の実装が存在しない古いプラットフォームビルドに存在します。</span><span class="sxs-lookup"><span data-stu-id="fccf3-161">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="fccf3-162">ビルドをアップグレードすると、問題が解決するはずです。</span><span class="sxs-lookup"><span data-stu-id="fccf3-162">Upgrading the build should resolve the issue.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="fccf3-163">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="fccf3-163">Code snippets</span></span>

<span data-ttu-id="fccf3-164">**API を呼び出 `getLocation` して場所を取得する:**</span><span class="sxs-lookup"><span data-stu-id="fccf3-164">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="fccf3-165">**API を呼び出 `showLocation` して場所を表示します。**</span><span class="sxs-lookup"><span data-stu-id="fccf3-165">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="see-also"></a><span data-ttu-id="fccf3-166">関連項目</span><span class="sxs-lookup"><span data-stu-id="fccf3-166">See also</span></span>

* [<span data-ttu-id="fccf3-167">Teamsでのメディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="fccf3-167">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="fccf3-168">qr コードまたはバーコード スキャナー機能をTeamsに統合</span><span class="sxs-lookup"><span data-stu-id="fccf3-168">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
