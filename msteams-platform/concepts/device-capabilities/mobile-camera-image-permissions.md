---
title: メディア機能の統合
description: Teams JavaScript クライアント SDK を使用してメディア機能を有効にする方法
keywords: カメラ イメージマイク機能ネイティブ デバイスアクセス許可メディア
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4126551858116343689e08c4b4f385eb0bbc7ed1
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231598"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="842b6-104">メディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="842b6-104">Integrate media capabilities</span></span> 

<span data-ttu-id="842b6-105">このドキュメントでは、メディア機能を統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="842b6-105">This document guides you on how to integrate media capabilities.</span></span> <span data-ttu-id="842b6-106">この統合は、カメラやマイクなどのネイティブ デバイス機能と Teams **プラットフォームを組** み合わせた機能です。</span><span class="sxs-lookup"><span data-stu-id="842b6-106">This integration combines the native device capabilities, such as the **camera** and **microphone** with the Teams platform.</span></span>  

<span data-ttu-id="842b6-107">アプリがユーザーの [デバイスのアクセス](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)許可にアクセスするために必要なツールを提供する Microsoft Teams JavaScript クライアント SDK を [使用できます](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="842b6-107">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="842b6-108">適切な **メディア機能 API** を使用して、Microsoft Teams モバイルアプリ内の Teams プラットフォームにカメラやマイクなどのネイティブ デバイス機能を統合し、より充実したエクスペリエンスを構築します。</span><span class="sxs-lookup"><span data-stu-id="842b6-108">Use suitable  **media capability APIs** to integrate the native device capabilities, such as the **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="842b6-109">メディア機能を統合する利点</span><span class="sxs-lookup"><span data-stu-id="842b6-109">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="842b6-110">Teams アプリにデバイス機能を統合する主な利点は、ネイティブの Teams コントロールを活用して、ユーザーに充実した没入型のエクスペリエンスを提供する方法です。</span><span class="sxs-lookup"><span data-stu-id="842b6-110">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="842b6-111">メディア機能を統合するには、アプリ マニフェスト ファイルを更新し、メディア機能 API を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="842b6-111">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="842b6-112">効果的に統合するには、ネイティブ メディア機能を使用[](#code-snippets)できる各 API を呼び出すコード スニペットについて理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="842b6-112">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="842b6-113">Teams アプリでエラーを処理するには [、API 応答エラー](#error-handling) について理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="842b6-113">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="842b6-114">現在、メディア機能に対する Microsoft Teams のサポートはモバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="842b6-114">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="842b6-115">マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="842b6-115">Update manifest</span></span>

<span data-ttu-id="842b6-116">プロパティを追加し [ 、manifest.jsして、ファイル](../../resources/schema/manifest-schema.md#devicepermissions) に対する Teams アプリの `devicePermissions` 更新を行います `media` 。</span><span class="sxs-lookup"><span data-stu-id="842b6-116">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="842b6-117">これにより、アプリでは、ユーザーがカメラを使って画像をキャプチャする前に必要なアクセス許可をユーザーに要求したり、ギャラリーを開いて添付ファイルとして送信する画像を選択したり、マイクを使って会話を録音することができます。</span><span class="sxs-lookup"><span data-stu-id="842b6-117">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="842b6-118">関連 **する** Teams API が開始されると、アクセス許可の要求プロンプトが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="842b6-118">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="842b6-119">詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="842b6-119">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="842b6-120">メディア機能 API</span><span class="sxs-lookup"><span data-stu-id="842b6-120">Media capability APIs</span></span>

<span data-ttu-id="842b6-121">[selectMedia、getMedia、](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)および[viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) API を使用すると、次のようにネイティブ メディア機能を使用できます。 [](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="842b6-121">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="842b6-122">ネイティブ マイクを **使って** 、ユーザーがデバイスから **音声を録音** (会話の 10 分を録音) できます。</span><span class="sxs-lookup"><span data-stu-id="842b6-122">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="842b6-123">ネイティブ カメラ コントロール **を使** って、ユーザーが移動 **中に画像を** キャプチャしてアタッチできます。</span><span class="sxs-lookup"><span data-stu-id="842b6-123">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="842b6-124">ネイティブ ギャラリー の **サポートを使用** して、ユーザーが添付ファイル **としてデバイス イメージを** 選択できます。</span><span class="sxs-lookup"><span data-stu-id="842b6-124">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="842b6-125">ネイティブイメージ **ビューアー コントロールを使用して、\*\*\*\*複数の画像を** 一度にプレビューします。</span><span class="sxs-lookup"><span data-stu-id="842b6-125">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="842b6-126">SDK **ブリッジを介した** 大きなイメージ転送 (1 MB ~ 50 MB) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="842b6-126">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="842b6-127">ユーザー **が画像をプレビューおよび編集** できる高度な画像機能をサポートします。</span><span class="sxs-lookup"><span data-stu-id="842b6-127">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="842b6-128">カメラを介してドキュメント、ホワイトボード、名刺をスキャンします。</span><span class="sxs-lookup"><span data-stu-id="842b6-128">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
>*   <span data-ttu-id="842b6-129">タスク モジュール、タブ、個人用アプリなど、複数の Teams サーフェスから API `selectMedia` `getMedia` `viewImages` を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="842b6-129">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="842b6-130">詳細については [、「Teams アプリのエントリ ポイント」を参照してください](../extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="842b6-130">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
>* <span data-ttu-id="842b6-131">`selectMedia` マイクとオーディオのプロパティをサポートするために API が拡張されました。</span><span class="sxs-lookup"><span data-stu-id="842b6-131">`selectMedia` API has been extended to support mic and audio properties.</span></span>

<span data-ttu-id="842b6-132">デバイスのメディア機能を有効にするには、次の API のセットを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="842b6-132">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="842b6-133">API</span><span class="sxs-lookup"><span data-stu-id="842b6-133">API</span></span>      | <span data-ttu-id="842b6-134">説明</span><span class="sxs-lookup"><span data-stu-id="842b6-134">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="842b6-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**</span><span class="sxs-lookup"><span data-stu-id="842b6-135">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="842b6-136">この API を使用すると、ユーザーはデバイス **カメラからメディア** をキャプチャまたは選択し、それを Web アプリに返します。</span><span class="sxs-lookup"><span data-stu-id="842b6-136">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="842b6-137">ユーザーは、申請前に画像を編集、トリミング、回転、注釈付け、または描画できます。</span><span class="sxs-lookup"><span data-stu-id="842b6-137">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="842b6-138">**selectMedia** への応答として、Web アプリは選択した画像のメディア ID と、選択したメディアのサムネイルを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="842b6-138">In response to **selectMedia**, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="842b6-139">この API は [、ImageProps](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) 構成を使用してさらに構成できます。</span><span class="sxs-lookup"><span data-stu-id="842b6-139">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="842b6-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)</span><span class="sxs-lookup"><span data-stu-id="842b6-140">[**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="842b6-141">selectMedia API [でマイク機能](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) `4` に **アクセスするために mediaType** を設定します。</span><span class="sxs-lookup"><span data-stu-id="842b6-141">Set the [mediaType](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in **selectMedia** API for accessing microphone  capability.</span></span> <span data-ttu-id="842b6-142">また、この API を使用すると、ユーザーはデバイスのマイクからオーディオを録音し、録音したクリップを Web アプリに返します。</span><span class="sxs-lookup"><span data-stu-id="842b6-142">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="842b6-143">ユーザーは、提出前に一時停止、再レコーディング、レコーディングプレビューを再生できます。</span><span class="sxs-lookup"><span data-stu-id="842b6-143">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="842b6-144"> *\*selectMedia** への応答として、Web アプリは選択したオーディオ録音のメディア ID を受信します。</span><span class="sxs-lookup"><span data-stu-id="842b6-144">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="842b6-145">会話 `maxDuration` の録音時間を分単位で構成する必要がある場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="842b6-145">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="842b6-146">現在のレコーディング時間は 10 分で、その後でレコーディングが終了します。</span><span class="sxs-lookup"><span data-stu-id="842b6-146">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="842b6-147">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="842b6-147">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="842b6-148">この API は、メディア サイズに関係なく **、selectMedia** API によってキャプチャされたメディアをチャンクで取得します。</span><span class="sxs-lookup"><span data-stu-id="842b6-148">This API retrieves the media captured by **selectMedia** API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="842b6-149">これらのチャンクはアセンブルされ、ファイルまたは BLOB として Web アプリに送り返されます。</span><span class="sxs-lookup"><span data-stu-id="842b6-149">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="842b6-150">メディアを小さなチャンクに分割すると、大きなファイル転送が容易です。</span><span class="sxs-lookup"><span data-stu-id="842b6-150">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="842b6-151">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="842b6-151">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="842b6-152">この API を使用すると、ユーザーは画像をスクロール可能なリストとして全画面モードで表示できます。</span><span class="sxs-lookup"><span data-stu-id="842b6-152">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|


<span data-ttu-id="842b6-153">**画像機能用の selectMedia API の Web アプリ エクスペリエンス** 
 ![Teams でのデバイスのカメラと画像のエクスペリエンス](../../assets/images/tabs/image-capability.png)</span><span class="sxs-lookup"><span data-stu-id="842b6-153">**Web app experience for selectMedia API for image capability**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability.png)</span></span>

<span data-ttu-id="842b6-154">**マイク機能用の selectMedia API の Web アプリ エクスペリエンス** 
 ![マイク機能用の Web アプリ エクスペリエンス](../../assets/images/tabs/microphone-capability.png)</span><span class="sxs-lookup"><span data-stu-id="842b6-154">**Web app experience for selectMedia API for microphone capability**
![web app experience for microphone capability](../../assets/images/tabs/microphone-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="842b6-155">エラー処理</span><span class="sxs-lookup"><span data-stu-id="842b6-155">Error handling</span></span>

<span data-ttu-id="842b6-156">Teams アプリでこれらのエラーを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="842b6-156">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="842b6-157">次の表に、エラー コードとエラーが生成される条件を示します。</span><span class="sxs-lookup"><span data-stu-id="842b6-157">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 


|<span data-ttu-id="842b6-158">エラー コード</span><span class="sxs-lookup"><span data-stu-id="842b6-158">Error code</span></span> |  <span data-ttu-id="842b6-159">エラー名</span><span class="sxs-lookup"><span data-stu-id="842b6-159">Error name</span></span>     | <span data-ttu-id="842b6-160">Condition</span><span class="sxs-lookup"><span data-stu-id="842b6-160">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="842b6-161">**100**</span><span class="sxs-lookup"><span data-stu-id="842b6-161">**100**</span></span> | <span data-ttu-id="842b6-162">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="842b6-162">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="842b6-163">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="842b6-163">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="842b6-164">**404**</span><span class="sxs-lookup"><span data-stu-id="842b6-164">**404**</span></span> | <span data-ttu-id="842b6-165">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="842b6-165">FILE_NOT_FOUND</span></span> | <span data-ttu-id="842b6-166">指定されたファイルが特定の場所に見つかりません。</span><span class="sxs-lookup"><span data-stu-id="842b6-166">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="842b6-167">**500**</span><span class="sxs-lookup"><span data-stu-id="842b6-167">**500**</span></span> | <span data-ttu-id="842b6-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="842b6-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="842b6-169">必要な操作の実行中に内部エラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="842b6-169">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="842b6-170">**1000**</span><span class="sxs-lookup"><span data-stu-id="842b6-170">**1000**</span></span> | <span data-ttu-id="842b6-171">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="842b6-171">PERMISSION_DENIED</span></span> |<span data-ttu-id="842b6-172">アクセス許可はユーザーによって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="842b6-172">Permission is denied by the user.</span></span>|
| <span data-ttu-id="842b6-173">**2000**</span><span class="sxs-lookup"><span data-stu-id="842b6-173">**2000**</span></span> |<span data-ttu-id="842b6-174">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="842b6-174">NETWORK_ERROR</span></span> | <span data-ttu-id="842b6-175">ネットワークの問題。</span><span class="sxs-lookup"><span data-stu-id="842b6-175">Network issue.</span></span>|
| <span data-ttu-id="842b6-176">**3000**</span><span class="sxs-lookup"><span data-stu-id="842b6-176">**3000**</span></span> | <span data-ttu-id="842b6-177">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="842b6-177">NO_HW_SUPPORT</span></span> | <span data-ttu-id="842b6-178">基になるハードウェアは、この機能をサポートしていない。</span><span class="sxs-lookup"><span data-stu-id="842b6-178">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="842b6-179">**4000**</span><span class="sxs-lookup"><span data-stu-id="842b6-179">**4000**</span></span>| <span data-ttu-id="842b6-180">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="842b6-180">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="842b6-181">いくつかの引数は無効です。</span><span class="sxs-lookup"><span data-stu-id="842b6-181">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="842b6-182">**5000**</span><span class="sxs-lookup"><span data-stu-id="842b6-182">**5000**</span></span> | <span data-ttu-id="842b6-183">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="842b6-183">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="842b6-184">ユーザーは、この操作を完了する権限を持てない。</span><span class="sxs-lookup"><span data-stu-id="842b6-184">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="842b6-185">**6000**</span><span class="sxs-lookup"><span data-stu-id="842b6-185">**6000**</span></span> |<span data-ttu-id="842b6-186">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="842b6-186">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="842b6-187">リソースが不足していたので、操作を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="842b6-187">Operation could not be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="842b6-188">**7000**</span><span class="sxs-lookup"><span data-stu-id="842b6-188">**7000**</span></span> | <span data-ttu-id="842b6-189">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="842b6-189">THROTTLE</span></span> | <span data-ttu-id="842b6-190">API が頻繁に呼び出されたので、プラットフォームは要求を調整しました。</span><span class="sxs-lookup"><span data-stu-id="842b6-190">Platform throttled the request as the API was invoked frequently.</span></span>|
|  <span data-ttu-id="842b6-191">**8000**</span><span class="sxs-lookup"><span data-stu-id="842b6-191">**8000**</span></span> | <span data-ttu-id="842b6-192">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="842b6-192">USER_ABORT</span></span> |<span data-ttu-id="842b6-193">ユーザーが操作を中止しました。</span><span class="sxs-lookup"><span data-stu-id="842b6-193">User aborts the operation.</span></span>|
| <span data-ttu-id="842b6-194">**9000**</span><span class="sxs-lookup"><span data-stu-id="842b6-194">**9000**</span></span>| <span data-ttu-id="842b6-195">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="842b6-195">OLD_PLATFORM</span></span> | <span data-ttu-id="842b6-196">プラットフォーム コードは古く、この API は実装されません。</span><span class="sxs-lookup"><span data-stu-id="842b6-196">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="842b6-197">**10000**</span><span class="sxs-lookup"><span data-stu-id="842b6-197">**10000**</span></span>| <span data-ttu-id="842b6-198">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="842b6-198">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="842b6-199">戻り値が大きすぎるので、プラットフォーム サイズの境界を超えました。</span><span class="sxs-lookup"><span data-stu-id="842b6-199">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="842b6-200">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="842b6-200">Code snippets</span></span>

<span data-ttu-id="842b6-201">**通話 `selectMedia` カメラを** 使用して画像をキャプチャするための API:</span><span class="sxs-lookup"><span data-stu-id="842b6-201">**Calling `selectMedia` API** for capturing images using camera:</span></span>

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

<span data-ttu-id="842b6-202">**通話 `getMedia` 大きな** メディアをチャンクで取得する API:</span><span class="sxs-lookup"><span data-stu-id="842b6-202">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

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

<span data-ttu-id="842b6-203">**通話 `viewImages`API によって返される ID による `selectMedia` API:**</span><span class="sxs-lookup"><span data-stu-id="842b6-203">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

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

<span data-ttu-id="842b6-204">**通話 `viewImages`URL 別 API:**</span><span class="sxs-lookup"><span data-stu-id="842b6-204">**Calling `viewImages` API by URL**:</span></span>

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

<span data-ttu-id="842b6-205">**マイク `selectMedia` を `getMedia` 介してオーディオを録音する呼び出しと API:**</span><span class="sxs-lookup"><span data-stu-id="842b6-205">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

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
