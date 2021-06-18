---
title: メディア機能を統合する
author: Rajeshwari-v
description: JavaScript クライアント SDK Teamsメディア機能を有効にする方法
keywords: カメラ イメージ マイク機能ネイティブ デバイスのアクセス許可メディア
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: e2d3c6e4b9e80d5b09cf597a29e7f3ba67355715
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994379"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="02e4e-104">メディア機能を統合する</span><span class="sxs-lookup"><span data-stu-id="02e4e-104">Integrate media capabilities</span></span> 

<span data-ttu-id="02e4e-105">このドキュメントでは、メディア機能を統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-105">This document guides you on how to integrate media capabilities.</span></span> <span data-ttu-id="02e4e-106">この統合により、カメラやマイクなどのネイティブ デバイス機能と、新しいプラットフォームTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-106">This integration combines the native device capabilities, such as the **camera** and **microphone** with the Teams platform.</span></span>  

<span data-ttu-id="02e4e-107">ユーザーのデバイス[Microsoft Teamsアクセス](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)するためにアプリに必要なツールを提供する JavaScript クライアント SDK を使用[できます](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="02e4e-107">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="02e4e-108">適切なメディア機能 API を使用して、カメラやマイクなどのネイティブデバイス機能を Microsoft Teams モバイル アプリ内の Teams プラットフォームに統合し、より豊富なエクスペリエンスを構築します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-108">Use suitable  media capability APIs to integrate the native device capabilities, such as the **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="02e4e-109">メディア機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="02e4e-109">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="02e4e-110">Teams アプリにデバイス機能を統合する主な利点は、ネイティブ Teams コントロールを活用して、ユーザーに豊富で没入感のあるエクスペリエンスを提供する方法です。</span><span class="sxs-lookup"><span data-stu-id="02e4e-110">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="02e4e-111">メディア機能を統合するには、アプリ マニフェスト ファイルを更新し、メディア機能 API を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="02e4e-111">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="02e4e-112">効果的な統合を行う場合は、それぞれの[](#code-snippets)API を呼び出すコード スニペットについて理解している必要があります。ネイティブ メディア機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-112">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="02e4e-113">API 応答エラーを理解して、アプリ[](#error-handling)内のエラーを処理することがTeamsです。</span><span class="sxs-lookup"><span data-stu-id="02e4e-113">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> * <span data-ttu-id="02e4e-114">現在、Microsoft Teams機能のサポートはモバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-114">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>    
> * <span data-ttu-id="02e4e-115">現在、Teamsは、マルチ ウィンドウ アプリ、タブ、および会議のサイドパネルに対するデバイスのアクセス許可をサポートしていない。</span><span class="sxs-lookup"><span data-stu-id="02e4e-115">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span> 

## <a name="update-manifest"></a><span data-ttu-id="02e4e-116">マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="02e4e-116">Update manifest</span></span>

<span data-ttu-id="02e4e-117">プロパティを追加Teamsを[manifest.jsして](../../resources/schema/manifest-schema.md#devicepermissions)、ファイル上のアプリ `devicePermissions` のアプリを更新します `media` 。</span><span class="sxs-lookup"><span data-stu-id="02e4e-117">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="02e4e-118">これにより、ユーザーがカメラを使用して画像をキャプチャし始める前、ギャラリーを開いて添付ファイルとして送信する画像を選択するか、マイクを使用して会話を録音する前に、ユーザーに必要なアクセス許可を求めできます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-118">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="02e4e-119">要求 **のアクセス許可のプロンプト** は、関連する API が開始されるとTeams表示されます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-119">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="02e4e-120">詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="02e4e-120">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="02e4e-121">メディア機能 API</span><span class="sxs-lookup"><span data-stu-id="02e4e-121">Media capability APIs</span></span>

<span data-ttu-id="02e4e-122">[selectMedia、getMedia、](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)[](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)および[viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API を使用すると、ネイティブ メディア機能を次のように使用できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-122">The [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="02e4e-123">ネイティブ マイクを **使用して** 、ユーザーがデバイス **からオーディオ** (10 分の会話を録音) を録音できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-123">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="02e4e-124">ネイティブ カメラ コントロール **を使用** して、ユーザーが移動 **中に** 画像をキャプチャして添付できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-124">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="02e4e-125">ネイティブ ギャラリー **のサポートを使用** して、ユーザーが添付ファイル **としてデバイス イメージを選択** できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-125">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="02e4e-126">ネイティブ イメージ **ビューアー コントロールを使用して、\*\*\*\*一度に複数の画像** をプレビューします。</span><span class="sxs-lookup"><span data-stu-id="02e4e-126">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="02e4e-127">SDK **ブリッジを介した** 大規模なイメージ転送 (1 MB から 50 MB) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="02e4e-127">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="02e4e-128">ユーザーが **画像をプレビューおよび** 編集できる高度な画像機能をサポートします。</span><span class="sxs-lookup"><span data-stu-id="02e4e-128">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="02e4e-129">カメラを介してドキュメント、ホワイトボード、名刺をスキャンします。</span><span class="sxs-lookup"><span data-stu-id="02e4e-129">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="02e4e-130">タスク モジュール、タブ、個人用アプリなど、Teams、API を複数のサーフェス `selectMedia` `getMedia` `viewImages` から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-130">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="02e4e-131">詳細については、「アプリの[エントリ ポイント」をTeamsしてください](../extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="02e4e-131">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="02e4e-132">`selectMedia` マイクとオーディオのプロパティをサポートするために API が拡張されました。</span><span class="sxs-lookup"><span data-stu-id="02e4e-132">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="02e4e-133">デバイスのメディア機能を有効にするには、次の API セットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02e4e-133">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="02e4e-134">API</span><span class="sxs-lookup"><span data-stu-id="02e4e-134">API</span></span>      | <span data-ttu-id="02e4e-135">説明</span><span class="sxs-lookup"><span data-stu-id="02e4e-135">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="02e4e-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span><span class="sxs-lookup"><span data-stu-id="02e4e-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="02e4e-137">この API を使用すると、 **ユーザーはデバイス** カメラからメディアをキャプチャまたは選択し、Web アプリに戻します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-137">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="02e4e-138">ユーザーは、申請前に画像を編集、トリミング、回転、注釈、または描画できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-138">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="02e4e-139">に応答して、Web アプリは、選択した画像のメディアの ID と、選択したメディアのサムネイル `selectMedia` を受信します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-139">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="02e4e-140">この API は [、ImageProps 構成を使用してさらに構成](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-140">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="02e4e-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**マイク**)</span><span class="sxs-lookup"><span data-stu-id="02e4e-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="02e4e-142">マイク機能 [にアクセスするために](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` `selectMedia` 、mediaType を API で設定します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-142">Set the [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="02e4e-143">また、この API を使用すると、ユーザーはデバイスのマイクからオーディオを録音し、記録されたクリップを Web アプリに戻す機能も使用できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-143">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="02e4e-144">ユーザーは、申請前に録音プレビューを一時停止、再録音、再生できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-144">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="02e4e-145"> *\*selectMedia に応答して*\*、Web アプリは選択したオーディオ録音のメディアの ID を受信します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-145">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="02e4e-146">会話 `maxDuration` を記録するために時間を分単位で構成する必要がある場合は、使用します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-146">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="02e4e-147">現在の記録時間は 10 分で、その後、記録は終了します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-147">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="02e4e-148">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="02e4e-148">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="02e4e-149">この API は、メディア サイズに関係なく、API によってキャプチャされたメディアをチャンク `selectMedia` 単位で取得します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-149">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="02e4e-150">これらのチャンクはアセンブルされ、ファイルまたは BLOB として Web アプリに返されます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-150">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="02e4e-151">メディアを小さなチャンクに分割すると、大きなファイル転送が容易です。</span><span class="sxs-lookup"><span data-stu-id="02e4e-151">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="02e4e-152">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="02e4e-152">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="02e4e-153">この API を使用すると、ユーザーはスクロール可能なリストとしてフルスクリーン モードで画像を表示できます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-153">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|


<span data-ttu-id="02e4e-154">**画像機能用の selectMedia API の Web アプリ エクスペリエンス** 
 ![デバイス カメラとイメージ エクスペリエンス (Teams](../../assets/images/tabs/image-capability.png)</span><span class="sxs-lookup"><span data-stu-id="02e4e-154">**Web app experience for selectMedia API for image capability**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability.png)</span></span>

<span data-ttu-id="02e4e-155">**selectMedia API 用の Web アプリ エクスペリエンス (マイク機能用)** 
 ![マイク機能用の Web アプリ エクスペリエンス](../../assets/images/tabs/microphone-capability.png)</span><span class="sxs-lookup"><span data-stu-id="02e4e-155">**Web app experience for selectMedia API for microphone capability**
![web app experience for microphone capability](../../assets/images/tabs/microphone-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="02e4e-156">エラー処理</span><span class="sxs-lookup"><span data-stu-id="02e4e-156">Error handling</span></span>

<span data-ttu-id="02e4e-157">これらのエラーは、アプリで適切に処理Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="02e4e-157">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="02e4e-158">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-158">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 


|<span data-ttu-id="02e4e-159">エラー コード</span><span class="sxs-lookup"><span data-stu-id="02e4e-159">Error code</span></span> |  <span data-ttu-id="02e4e-160">エラー名</span><span class="sxs-lookup"><span data-stu-id="02e4e-160">Error name</span></span>     | <span data-ttu-id="02e4e-161">条件</span><span class="sxs-lookup"><span data-stu-id="02e4e-161">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="02e4e-162">**100**</span><span class="sxs-lookup"><span data-stu-id="02e4e-162">**100**</span></span> | <span data-ttu-id="02e4e-163">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="02e4e-163">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="02e4e-164">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="02e4e-164">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="02e4e-165">**404**</span><span class="sxs-lookup"><span data-stu-id="02e4e-165">**404**</span></span> | <span data-ttu-id="02e4e-166">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="02e4e-166">FILE_NOT_FOUND</span></span> | <span data-ttu-id="02e4e-167">指定されたファイルが指定された場所に見つかりません。</span><span class="sxs-lookup"><span data-stu-id="02e4e-167">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="02e4e-168">**500**</span><span class="sxs-lookup"><span data-stu-id="02e4e-168">**500**</span></span> | <span data-ttu-id="02e4e-169">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="02e4e-169">INTERNAL_ERROR</span></span> | <span data-ttu-id="02e4e-170">必要な操作の実行中に内部エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-170">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="02e4e-171">**1000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-171">**1000**</span></span> | <span data-ttu-id="02e4e-172">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="02e4e-172">PERMISSION_DENIED</span></span> |<span data-ttu-id="02e4e-173">アクセス許可は、ユーザーによって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="02e4e-173">Permission is denied by the user.</span></span>|
| <span data-ttu-id="02e4e-174">**2000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-174">**2000**</span></span> |<span data-ttu-id="02e4e-175">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="02e4e-175">NETWORK_ERROR</span></span> | <span data-ttu-id="02e4e-176">ネットワークの問題。</span><span class="sxs-lookup"><span data-stu-id="02e4e-176">Network issue.</span></span>|
| <span data-ttu-id="02e4e-177">**3000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-177">**3000**</span></span> | <span data-ttu-id="02e4e-178">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="02e4e-178">NO_HW_SUPPORT</span></span> | <span data-ttu-id="02e4e-179">基になるハードウェアでは、この機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="02e4e-179">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="02e4e-180">**4000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-180">**4000**</span></span>| <span data-ttu-id="02e4e-181">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="02e4e-181">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="02e4e-182">いくつかの引数は無効です。</span><span class="sxs-lookup"><span data-stu-id="02e4e-182">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="02e4e-183">**5000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-183">**5000**</span></span> | <span data-ttu-id="02e4e-184">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="02e4e-184">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="02e4e-185">ユーザーは、この操作を完了する権限を持てない。</span><span class="sxs-lookup"><span data-stu-id="02e4e-185">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="02e4e-186">**6000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-186">**6000**</span></span> |<span data-ttu-id="02e4e-187">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="02e4e-187">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="02e4e-188">リソース不足のため、操作を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02e4e-188">Operation could not be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="02e4e-189">**7000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-189">**7000**</span></span> | <span data-ttu-id="02e4e-190">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="02e4e-190">THROTTLE</span></span> | <span data-ttu-id="02e4e-191">API が頻繁に呼び出されると、プラットフォームは要求を調整しました。</span><span class="sxs-lookup"><span data-stu-id="02e4e-191">Platform throttled the request as the API was invoked frequently.</span></span>|
|  <span data-ttu-id="02e4e-192">**8000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-192">**8000**</span></span> | <span data-ttu-id="02e4e-193">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="02e4e-193">USER_ABORT</span></span> |<span data-ttu-id="02e4e-194">ユーザーは操作を中止します。</span><span class="sxs-lookup"><span data-stu-id="02e4e-194">User aborts the operation.</span></span>|
| <span data-ttu-id="02e4e-195">**9000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-195">**9000**</span></span>| <span data-ttu-id="02e4e-196">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="02e4e-196">OLD_PLATFORM</span></span> | <span data-ttu-id="02e4e-197">プラットフォーム コードは古く、この API は実装されません。</span><span class="sxs-lookup"><span data-stu-id="02e4e-197">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="02e4e-198">**10000**</span><span class="sxs-lookup"><span data-stu-id="02e4e-198">**10000**</span></span>| <span data-ttu-id="02e4e-199">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="02e4e-199">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="02e4e-200">戻り値が大きすぎて、プラットフォーム サイズの境界を超えました。</span><span class="sxs-lookup"><span data-stu-id="02e4e-200">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="02e4e-201">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="02e4e-201">Code snippets</span></span>

<span data-ttu-id="02e4e-202">**通話 `selectMedia` カメラを** 使用して画像をキャプチャするための API:</span><span class="sxs-lookup"><span data-stu-id="02e4e-202">**Calling `selectMedia` API** for capturing images using camera:</span></span>

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

<span data-ttu-id="02e4e-203">**通話 `getMedia` 大きな** メディアをチャンクで取得する API:</span><span class="sxs-lookup"><span data-stu-id="02e4e-203">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

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

<span data-ttu-id="02e4e-204">**通話 `viewImages` API によって返される `selectMedia` ID** による API:</span><span class="sxs-lookup"><span data-stu-id="02e4e-204">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

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

<span data-ttu-id="02e4e-205">**通話 `viewImages` URL による API**:</span><span class="sxs-lookup"><span data-stu-id="02e4e-205">**Calling `viewImages` API by URL**:</span></span>

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

<span data-ttu-id="02e4e-206">**マイク `selectMedia` を介 `getMedia` してオーディオを録音する呼び出しと API:**</span><span class="sxs-lookup"><span data-stu-id="02e4e-206">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="02e4e-207">関連項目</span><span class="sxs-lookup"><span data-stu-id="02e4e-207">See also</span></span>

* [<span data-ttu-id="02e4e-208">QR スキャナーまたはバーコード スキャナー機能をアプリに統合Teams</span><span class="sxs-lookup"><span data-stu-id="02e4e-208">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="02e4e-209">場所の機能を統合Teams</span><span class="sxs-lookup"><span data-stu-id="02e4e-209">Integrate location capabilities in Teams</span></span>](location-capability.md)
