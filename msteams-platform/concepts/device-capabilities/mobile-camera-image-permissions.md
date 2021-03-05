---
title: メディア機能を統合する
description: Teams JavaScript クライアント SDK を使用してメディア機能を有効にする方法
keywords: カメラ イメージ マイク機能ネイティブ デバイスのアクセス許可メディア
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 375d68c7c712b7a8d2f7114b47aae61c889b4197
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449582"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="3fe4c-104">メディア機能を統合する</span><span class="sxs-lookup"><span data-stu-id="3fe4c-104">Integrate media capabilities</span></span> 

<span data-ttu-id="3fe4c-105">このドキュメントでは、メディア機能を統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-105">This document guides you on how to integrate media capabilities.</span></span> <span data-ttu-id="3fe4c-106">この統合は、カメラやマイクなどのネイティブ デバイス機能と Teams **プラットフォームを** 組み合わせたものになります。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-106">This integration combines the native device capabilities, such as the **camera** and **microphone** with the Teams platform.</span></span>  

<span data-ttu-id="3fe4c-107">アプリが [ユーザーのデバイスの](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)アクセス許可にアクセスするために必要なツールを提供する Microsoft Teams JavaScript クライアント SDK を [使用できます](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-107">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="3fe4c-108">適切なメディア機能 API を使用して、カメラやマイクなどのネイティブデバイス機能を Microsoft Teams モバイル アプリ内の Teams プラットフォームに統合し、より豊富なエクスペリエンスを構築します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-108">Use suitable  media capability APIs to integrate the native device capabilities, such as the **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="3fe4c-109">メディア機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="3fe4c-109">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="3fe4c-110">Teams アプリにデバイス機能を統合する主な利点は、ネイティブの Teams コントロールを活用して、ユーザーに豊富で没入感のあるエクスペリエンスを提供する方法です。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-110">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="3fe4c-111">メディア機能を統合するには、アプリ マニフェスト ファイルを更新し、メディア機能 API を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-111">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="3fe4c-112">効果的な統合を行う場合は、それぞれの[](#code-snippets)API を呼び出すコード スニペットについて理解している必要があります。ネイティブ メディア機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-112">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="3fe4c-113">Teams アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-113">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="3fe4c-114">現在、メディア機能に対する Microsoft Teams のサポートは、モバイル クライアントでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-114">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="3fe4c-115">マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="3fe4c-115">Update manifest</span></span>

<span data-ttu-id="3fe4c-116">プロパティを追加し [ 、manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions) Teams アプリを更新 `devicePermissions` します `media` 。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-116">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="3fe4c-117">これにより、ユーザーがカメラを使用して画像をキャプチャし始める前、ギャラリーを開いて添付ファイルとして送信する画像を選択するか、マイクを使用して会話を録音する前に、ユーザーに必要なアクセス許可を求めできます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-117">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="3fe4c-118">関連 **する Teams** API が開始されると、[アクセス許可の要求] プロンプトが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-118">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="3fe4c-119">詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-119">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="3fe4c-120">メディア機能 API</span><span class="sxs-lookup"><span data-stu-id="3fe4c-120">Media capability APIs</span></span>

<span data-ttu-id="3fe4c-121">[selectMedia、getMedia、](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)[](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)および[viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) API を使用すると、ネイティブ メディア機能を次のように使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-121">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="3fe4c-122">ネイティブ マイクを **使用して** 、ユーザーがデバイス **からオーディオ** (10 分の会話を録音) を録音できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-122">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="3fe4c-123">ネイティブ カメラ コントロール **を使用** して、ユーザーが移動 **中に** 画像をキャプチャして添付できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-123">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="3fe4c-124">ネイティブ ギャラリー **のサポートを使用** して、ユーザーが添付ファイル **としてデバイス イメージを選択** できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-124">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="3fe4c-125">ネイティブ イメージ **ビューアー コントロールを使用して、\*\*\*\*一度に複数の画像** をプレビューします。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-125">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="3fe4c-126">SDK **ブリッジを介した** 大規模なイメージ転送 (1 MB から 50 MB) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-126">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="3fe4c-127">ユーザーが **画像をプレビューおよび** 編集できる高度な画像機能をサポートします。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-127">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="3fe4c-128">カメラを介してドキュメント、ホワイトボード、名刺をスキャンします。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-128">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="3fe4c-129">、および API は、タスク モジュール、タブ、個人用アプリなど、複数の Teams サーフェス `selectMedia` `getMedia` `viewImages` から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-129">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="3fe4c-130">詳細については [、「Teams アプリのエントリ ポイント」を参照してください](../extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-130">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="3fe4c-131">`selectMedia` マイクとオーディオのプロパティをサポートするために API が拡張されました。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-131">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="3fe4c-132">デバイスのメディア機能を有効にするには、次の API セットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-132">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="3fe4c-133">API</span><span class="sxs-lookup"><span data-stu-id="3fe4c-133">API</span></span>      | <span data-ttu-id="3fe4c-134">説明</span><span class="sxs-lookup"><span data-stu-id="3fe4c-134">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="3fe4c-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="3fe4c-136">この API を使用すると、 **ユーザーはデバイス** カメラからメディアをキャプチャまたは選択し、Web アプリに戻します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-136">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="3fe4c-137">ユーザーは、申請前に画像を編集、トリミング、回転、注釈、または描画できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-137">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="3fe4c-138">に応答して、Web アプリは、選択した画像のメディアの ID と、選択したメディアのサムネイル `selectMedia` を受信します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-138">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="3fe4c-139">この API は [、ImageProps 構成を使用してさらに構成](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-139">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="3fe4c-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**マイク**)</span><span class="sxs-lookup"><span data-stu-id="3fe4c-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="3fe4c-141">マイク機能 [にアクセスするために](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) `4` `selectMedia` 、mediaType を API で設定します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-141">Set the [mediaType](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="3fe4c-142">また、この API を使用すると、ユーザーはデバイスのマイクからオーディオを録音し、記録されたクリップを Web アプリに戻す機能も使用できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-142">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="3fe4c-143">ユーザーは、申請前に録音プレビューを一時停止、再録音、再生できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-143">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="3fe4c-144"> *\*selectMedia に応答して*\*、Web アプリは選択したオーディオ録音のメディアの ID を受信します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-144">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="3fe4c-145">会話 `maxDuration` を記録するために時間を分単位で構成する必要がある場合は、使用します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-145">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="3fe4c-146">現在の記録時間は 10 分で、その後、記録は終了します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-146">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="3fe4c-147">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-147">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="3fe4c-148">この API は、メディア サイズに関係なく、API によってキャプチャされたメディアをチャンク `selectMedia` 単位で取得します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-148">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="3fe4c-149">これらのチャンクはアセンブルされ、ファイルまたは BLOB として Web アプリに返されます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-149">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="3fe4c-150">メディアを小さなチャンクに分割すると、大きなファイル転送が容易です。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-150">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="3fe4c-151">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-151">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="3fe4c-152">この API を使用すると、ユーザーはスクロール可能なリストとしてフルスクリーン モードで画像を表示できます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-152">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|


<span data-ttu-id="3fe4c-153">**画像機能用の selectMedia API の Web アプリ エクスペリエンス** 
 ![Teams でのデバイス カメラとイメージのエクスペリエンス](../../assets/images/tabs/image-capability.png)</span><span class="sxs-lookup"><span data-stu-id="3fe4c-153">**Web app experience for selectMedia API for image capability**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability.png)</span></span>

<span data-ttu-id="3fe4c-154">**selectMedia API 用の Web アプリ エクスペリエンス (マイク機能用)** 
 ![マイク機能用の Web アプリ エクスペリエンス](../../assets/images/tabs/microphone-capability.png)</span><span class="sxs-lookup"><span data-stu-id="3fe4c-154">**Web app experience for selectMedia API for microphone capability**
![web app experience for microphone capability](../../assets/images/tabs/microphone-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="3fe4c-155">エラー処理</span><span class="sxs-lookup"><span data-stu-id="3fe4c-155">Error handling</span></span>

<span data-ttu-id="3fe4c-156">Teams アプリでこれらのエラーを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-156">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="3fe4c-157">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-157">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 


|<span data-ttu-id="3fe4c-158">エラー コード</span><span class="sxs-lookup"><span data-stu-id="3fe4c-158">Error code</span></span> |  <span data-ttu-id="3fe4c-159">エラー名</span><span class="sxs-lookup"><span data-stu-id="3fe4c-159">Error name</span></span>     | <span data-ttu-id="3fe4c-160">Condition</span><span class="sxs-lookup"><span data-stu-id="3fe4c-160">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="3fe4c-161">**100**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-161">**100**</span></span> | <span data-ttu-id="3fe4c-162">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="3fe4c-162">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="3fe4c-163">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-163">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="3fe4c-164">**404**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-164">**404**</span></span> | <span data-ttu-id="3fe4c-165">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="3fe4c-165">FILE_NOT_FOUND</span></span> | <span data-ttu-id="3fe4c-166">指定されたファイルが指定された場所に見つかりません。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-166">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="3fe4c-167">**500**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-167">**500**</span></span> | <span data-ttu-id="3fe4c-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="3fe4c-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="3fe4c-169">必要な操作の実行中に内部エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-169">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="3fe4c-170">**1000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-170">**1000**</span></span> | <span data-ttu-id="3fe4c-171">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="3fe4c-171">PERMISSION_DENIED</span></span> |<span data-ttu-id="3fe4c-172">アクセス許可は、ユーザーによって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-172">Permission is denied by the user.</span></span>|
| <span data-ttu-id="3fe4c-173">**2000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-173">**2000**</span></span> |<span data-ttu-id="3fe4c-174">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="3fe4c-174">NETWORK_ERROR</span></span> | <span data-ttu-id="3fe4c-175">ネットワークの問題。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-175">Network issue.</span></span>|
| <span data-ttu-id="3fe4c-176">**3000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-176">**3000**</span></span> | <span data-ttu-id="3fe4c-177">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="3fe4c-177">NO_HW_SUPPORT</span></span> | <span data-ttu-id="3fe4c-178">基になるハードウェアでは、この機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-178">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="3fe4c-179">**4000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-179">**4000**</span></span>| <span data-ttu-id="3fe4c-180">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="3fe4c-180">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="3fe4c-181">いくつかの引数は無効です。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-181">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="3fe4c-182">**5000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-182">**5000**</span></span> | <span data-ttu-id="3fe4c-183">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="3fe4c-183">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="3fe4c-184">ユーザーは、この操作を完了する権限を持てない。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-184">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="3fe4c-185">**6000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-185">**6000**</span></span> |<span data-ttu-id="3fe4c-186">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="3fe4c-186">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="3fe4c-187">リソース不足のため、操作を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-187">Operation could not be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="3fe4c-188">**7000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-188">**7000**</span></span> | <span data-ttu-id="3fe4c-189">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="3fe4c-189">THROTTLE</span></span> | <span data-ttu-id="3fe4c-190">API が頻繁に呼び出されると、プラットフォームは要求を調整しました。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-190">Platform throttled the request as the API was invoked frequently.</span></span>|
|  <span data-ttu-id="3fe4c-191">**8000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-191">**8000**</span></span> | <span data-ttu-id="3fe4c-192">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="3fe4c-192">USER_ABORT</span></span> |<span data-ttu-id="3fe4c-193">ユーザーは操作を中止します。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-193">User aborts the operation.</span></span>|
| <span data-ttu-id="3fe4c-194">**9000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-194">**9000**</span></span>| <span data-ttu-id="3fe4c-195">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="3fe4c-195">OLD_PLATFORM</span></span> | <span data-ttu-id="3fe4c-196">プラットフォーム コードは古く、この API は実装されません。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-196">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="3fe4c-197">**10000**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-197">**10000**</span></span>| <span data-ttu-id="3fe4c-198">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="3fe4c-198">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="3fe4c-199">戻り値が大きすぎて、プラットフォーム サイズの境界を超えました。</span><span class="sxs-lookup"><span data-stu-id="3fe4c-199">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="3fe4c-200">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="3fe4c-200">Code snippets</span></span>

<span data-ttu-id="3fe4c-201">**通話 `selectMedia` カメラを** 使用して画像をキャプチャするための API:</span><span class="sxs-lookup"><span data-stu-id="3fe4c-201">**Calling `selectMedia` API** for capturing images using camera:</span></span>

```javascript
let imageProp: microsoftTeams.media.ImageProps = {
    sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
    startMode: microsoftTeams.media.CameraStartMode.Photo,
    ink: false,
    cameraSwitcher: false,
    textSticker: false,
    enableFilter: true,
};
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Image,
    maxMediaCount: 10,
    imageProps: imageProp
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    if (attachments) {
        let y = attachments[0];
        img.src = ("data:" + y.mimeType + ";base64," + y.preview);
    }
});
```

<span data-ttu-id="3fe4c-202">**通話 `getMedia` 大きな** メディアをチャンクで取得する API:</span><span class="sxs-lookup"><span data-stu-id="3fe4c-202">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

```javascript
let media: microsoftTeams.media.Media = attachments[0]
media.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("image")) {
            img.src = (URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

<span data-ttu-id="3fe4c-203">**通話 `viewImages` API によって返される `selectMedia` ID** による API:</span><span class="sxs-lookup"><span data-stu-id="3fe4c-203">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

```javascript
// View images by id:
// Assumption: attachmentArray = select Media API Output
let uriList = [];
if (attachmentArray && attachmentArray.length > 0) {
    for (let i = 0; i < attachmentArray.length; i++) {
        let file = attachmentArray[i];
        if (file.mimeType.includes("image")) {
            let imageUri = {
                value: file.content,
                type: 1,
            }
            uriList.push(imageUri);
        } else {
            alert("File type is not image");
        }
    }
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

<span data-ttu-id="3fe4c-204">**通話 `viewImages` URL による API**:</span><span class="sxs-lookup"><span data-stu-id="3fe4c-204">**Calling `viewImages` API by URL**:</span></span>

```javascript
// View Images by URL:
// Assumption 2 urls, url1 and url2
let uriList = [];
if (URL1 != null && URL1.length > 0) {
    let imageUri = {
        value: URL1,
        type: 2,
    }
    uriList.push(imageUri);
}
if (URL2 != null && URL2.length > 0) {
    let imageUri = {
        value: URL2,
        type: 2,
    }
    uriList.push(imageUri);
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

<span data-ttu-id="3fe4c-205">**マイク `selectMedia` を介 `getMedia` してオーディオを録音する呼び出しと API:**</span><span class="sxs-lookup"><span data-stu-id="3fe4c-205">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

```javascript
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Audio,
    maxMediaCount: 1,
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    // If you want to directly use the audio file (for smaller file sizes (~4MB))    if (attachments) {
    let audioResult = attachments[0];
    var videoElement = document.createElement("video");
    videoElement.setAttribute("src", ("data:" + y.mimeType + ";base64," + y.preview));
    //To use the audio file via get Media API for bigger audio file sizes greater than 4MB        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("video")) {
            videoElement.setAttribute("src", URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

## <a name="see-also"></a><span data-ttu-id="3fe4c-206">関連項目</span><span class="sxs-lookup"><span data-stu-id="3fe4c-206">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fe4c-207">Teams に QR またはバーコード スキャナー機能を統合する</span><span class="sxs-lookup"><span data-stu-id="3fe4c-207">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fe4c-208">Teams での場所機能の統合</span><span class="sxs-lookup"><span data-stu-id="3fe4c-208">Integrate location capabilities in Teams</span></span>](location-capability.md)