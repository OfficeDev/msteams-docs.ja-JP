---
title: Teams のカメラおよび画像の機能
description: Teams Javascript クライアント SDK を使用して、ネイティブのカメラおよびイメージ機能を有効にする方法
keywords: カメラの画像機能ネイティブデバイスのアクセス許可
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d0ca4dc9c289ec525aa99ea0e156a9f91f5b5d4a
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576884"
---
# <a name="camera-and-image-capabilities-in-teams"></a><span data-ttu-id="fbfcb-104">Teams のカメラおよび画像の機能</span><span class="sxs-lookup"><span data-stu-id="fbfcb-104">Camera and image capabilities in Teams</span></span>

>[!IMPORTANT]
>
> * <span data-ttu-id="fbfcb-105">現時点では、チームのカメラおよびイメージ機能のサポートは、モバイルクライアントでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-105">At present, Teams support for camera and image capabilities is only available for mobile clients.</span></span>
>* <span data-ttu-id="fbfcb-106">、 `selectMedia` 、 `getMedia` および api は、 `viewImages` タスクモジュール、タブ、個人用アプリなどの複数の Teams の表面から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-106">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="fbfcb-107">詳細については、「 [Teams アプリのエントリポイント](../extensibility-points.md) _」を参照してください_。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-107">For more details, _see_ [Entry points for Teams apps](../extensibility-points.md)</span></span>

<span data-ttu-id="fbfcb-108">Microsoft  [teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用すると、microsoft teams モバイルアプリ内でカメラとイメージの機能を簡単に統合できます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-108">You can use the  [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), to easily integrate camera and image capabilities within your Microsoft Teams mobile app.</span></span> <span data-ttu-id="fbfcb-109">SDK は、ユーザーの [デバイスのアクセス許可](native-device-permissions.md?tabs=desktop#device-permissions) にアクセスし、より充実した操作性を構築するためにアプリに必要なツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-109">The SDK provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md?tabs=desktop#device-permissions) and build a richer experience.</span></span>

<span data-ttu-id="fbfcb-110">[Selectmedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)、 [getmedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)、および[viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) api を使用すると、次のようにネイティブのカメラ/イメージ機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-110">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native camera/image capabilities as follows:</span></span>

* <span data-ttu-id="fbfcb-111">ネイティブ **カメラコントロール** を使用して、ユーザーが **画像を取り込ん** で移動できるようにします。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-111">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="fbfcb-112">ネイティブな **ギャラリーサポート** を使用して、ユーザーが **デバイス画像を** 添付ファイルとして選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-112">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="fbfcb-113">ネイティブ **イメージビューアーコントロール** を使用して、一度に **複数の画像をプレビュー** します。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-113">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="fbfcb-114">SDK ブリッジを使用した **大規模画像転送** (最大 50 MB) のサポート</span><span class="sxs-lookup"><span data-stu-id="fbfcb-114">Support **large image transfer** (up to 50 MB) via the SDK bridge</span></span>
* <span data-ttu-id="fbfcb-115">ユーザーがイメージをプレビューおよび編集できる **高度なイメージ機能** をサポートします。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-115">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="fbfcb-116">ドキュメント、ホワイトボード、名刺などのスキャンをカメラから行います。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-116">Scan document, whiteboard, business cards, etc., through the camera.</span></span>
  * <span data-ttu-id="fbfcb-117">画像をトリミングして回転させます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-117">Crop and rotate the images.</span></span>
  * <span data-ttu-id="fbfcb-118">画像にテキスト、インク、またはフリーハンドの注釈を追加します。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-118">Add text, ink, or freehand annotation to the image.</span></span>

## <a name="get-started"></a><span data-ttu-id="fbfcb-119">作業の開始</span><span class="sxs-lookup"><span data-stu-id="fbfcb-119">Get started</span></span>

<span data-ttu-id="fbfcb-120">プロパティを追加し、を指定することによって、Teams アプリ [manifest.jsをファイルで](../../resources/schema/manifest-schema.md#devicepermissions) 更新し `devicePermissions` `media` ます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions`  property and specifying `media`.</span></span> <span data-ttu-id="fbfcb-121">これにより、アプリは、カメラを使用して画像を取得したり、ギャラリーを開いて添付ファイルとして提出する画像を選択したりする前に、エンドユーザーから必要なアクセス許可を要求することができます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-121">This allows your app to ask for requisite permissions from end-users before they use the camera to capture the image or open the gallery to select an image to submit as an attachment.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="fbfcb-122">関連する Teams API が開始されると、 _要求アクセス許可_ のプロンプトが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-122">The _Request Permissions_ prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="fbfcb-123">詳細については、「[要求デバイスのアクセス許可](native-device-permissions.md) *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-123">For more details, *see* [Request device permissions](native-device-permissions.md).</span></span>

## <a name="using-camera-and-image-capability-apis"></a><span data-ttu-id="fbfcb-124">カメラおよびイメージ機能 Api の使用</span><span class="sxs-lookup"><span data-stu-id="fbfcb-124">Using camera and image capability APIs</span></span>

<span data-ttu-id="fbfcb-125">次の Api セットを使用して、カメラおよびイメージデバイスの機能を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-125">You can use the following set of APIs to enable camera and image device capabilities:</span></span>

| <span data-ttu-id="fbfcb-126">API</span><span class="sxs-lookup"><span data-stu-id="fbfcb-126">API</span></span>      | <span data-ttu-id="fbfcb-127">説明</span><span class="sxs-lookup"><span data-stu-id="fbfcb-127">Description</span></span>   |
| --- | --- |
| [<span data-ttu-id="fbfcb-128">**selectMedia**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-128">**selectMedia**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| <span data-ttu-id="fbfcb-129">この API を使用すると、ユーザーは **ネイティブデバイスからメディアをキャプチャまたは選択** して、web アプリに戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-129">This API allows users to **capture or select media from a native device** and return to the web-app.</span></span> <span data-ttu-id="fbfcb-130">ユーザーは、送信前に画像の編集、トリミング、回転、注釈、描画を選択できます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-130">Users may choose to edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="fbfcb-131">**Selectmedia** への応答として、web アプリは選択した画像のメディア id を受け取り、選択されたメディアのサムネイルを受信することがあります。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-131">In response to **selectMedia**, the web-app will receive media ids of selected images and may receive a thumbnail of the selected media.</span></span> |
| [<span data-ttu-id="fbfcb-132">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-132">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="fbfcb-133">この API は、サイズに関係なくチャンク内のメディアを取得します。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-133">This API retrieves the media in chunks irrespective of size.</span></span> <span data-ttu-id="fbfcb-134">これらのチャンクはアセンブルされ、ファイル/blob として web アプリに返されます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-134">These chunks are assembled and sent back to the web app as a file/blob.</span></span> <span data-ttu-id="fbfcb-135">この API を使用すると、画像が小さいチャンクに分割されて大きな画像転送が容易になります。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-135">With this API an image is broken into smaller chunks to facilitate large image transfer.</span></span> |
| [<span data-ttu-id="fbfcb-136">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-136">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="fbfcb-137">この API を使用すると、画像の全画面表示モードをスクロール可能なリストとして表示できます。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-137">This API enables the user to view images full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="fbfcb-138">**SelectMedia API** 
 ![ の Web アプリの使用感Teams でのデバイスカメラおよびイメージの利用感](../../assets/images/tabs/image-capability-screenshot.jpg)</span><span class="sxs-lookup"><span data-stu-id="fbfcb-138">**Web app experience for selectMedia API**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span></span>

## <a name="error-handling"></a><span data-ttu-id="fbfcb-139">エラー処理</span><span class="sxs-lookup"><span data-stu-id="fbfcb-139">Error handling</span></span>

<span data-ttu-id="fbfcb-140">API 応答エラーコードを理解し、それらを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-140">You should understand the API response error codes and handle them appropriately.</span></span> <span data-ttu-id="fbfcb-141">プラットフォームによって返される可能性のあるエラーコードの一覧を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-141">Below is a list of error codes that may be returned by the platform:</span></span>

|<span data-ttu-id="fbfcb-142">エラー コード</span><span class="sxs-lookup"><span data-stu-id="fbfcb-142">Error code</span></span> |  <span data-ttu-id="fbfcb-143">エラー名</span><span class="sxs-lookup"><span data-stu-id="fbfcb-143">Error Name</span></span>     | <span data-ttu-id="fbfcb-144">Condition</span><span class="sxs-lookup"><span data-stu-id="fbfcb-144">Condition</span></span>|
| --- | --- | --- |
| <span data-ttu-id="fbfcb-145">**100**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-145">**100**</span></span> | <span data-ttu-id="fbfcb-146">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fbfcb-146">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="fbfcb-147">API は現在のプラットフォームではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-147">API not supported in the current platform.</span></span>|
| <span data-ttu-id="fbfcb-148">**404**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-148">**404**</span></span> | <span data-ttu-id="fbfcb-149">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="fbfcb-149">FILE_NOT_FOUND</span></span> | <span data-ttu-id="fbfcb-150">指定したファイルが指定した場所に見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-150">The file specified was not found on the given location.</span></span>|
| <span data-ttu-id="fbfcb-151">**500**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-151">**500**</span></span> | <span data-ttu-id="fbfcb-152">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="fbfcb-152">INTERNAL_ERROR</span></span> | <span data-ttu-id="fbfcb-153">必要な操作の実行中に内部エラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-153">Internal error encountered while performing the required operation.</span></span>|
| <span data-ttu-id="fbfcb-154">**1000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-154">**1000**</span></span> | <span data-ttu-id="fbfcb-155">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="fbfcb-155">PERMISSION_DENIED</span></span> |<span data-ttu-id="fbfcb-156">ユーザーによって拒否されたアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-156">Permissions denied by the user.</span></span>|
| <span data-ttu-id="fbfcb-157">**2000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-157">**2000**</span></span> |<span data-ttu-id="fbfcb-158">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="fbfcb-158">NETWORK_ERROR</span></span> | <span data-ttu-id="fbfcb-159">ネットワークの問題。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-159">Network issue.</span></span>|
| <span data-ttu-id="fbfcb-160">**3000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-160">**3000**</span></span> | <span data-ttu-id="fbfcb-161">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="fbfcb-161">NO_HW_SUPPORT</span></span> | <span data-ttu-id="fbfcb-162">基礎となるハードウェアは、機能をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-162">Underlying hardware doesn't support the capability.</span></span>|
| <span data-ttu-id="fbfcb-163">**4000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-163">**4000**</span></span>| <span data-ttu-id="fbfcb-164">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="fbfcb-164">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="fbfcb-165">1つ以上の引数が無効です。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-165">One or more arguments is invalid.</span></span>|
| <span data-ttu-id="fbfcb-166">**5000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-166">**5000**</span></span> | <span data-ttu-id="fbfcb-167">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="fbfcb-167">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="fbfcb-168">ユーザーがこの操作を完了する権限がありません。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-168">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="fbfcb-169">**6000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-169">**6000**</span></span> |<span data-ttu-id="fbfcb-170">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="fbfcb-170">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="fbfcb-171">リソースが不足しているため、操作を完了できませんでした。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-171">The operation couldn't be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="fbfcb-172">**7000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-172">**7000**</span></span> | <span data-ttu-id="fbfcb-173">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="fbfcb-173">THROTTLE</span></span> | <span data-ttu-id="fbfcb-174">API が頻繁に呼び出されていないため、要求が調整されました。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-174">The platform throttled the request because the API was invoked too frequently.</span></span>|
|  <span data-ttu-id="fbfcb-175">**8000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-175">**8000**</span></span> | <span data-ttu-id="fbfcb-176">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="fbfcb-176">USER_ABORT</span></span> |<span data-ttu-id="fbfcb-177">ユーザーが操作を中止しました。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-177">User aborted the operation.</span></span>|
| <span data-ttu-id="fbfcb-178">**9000**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-178">**9000**</span></span>| <span data-ttu-id="fbfcb-179">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fbfcb-179">OLD_PLATFORM</span></span> | <span data-ttu-id="fbfcb-180">プラットフォームコードは古く、この API は実装されていません。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-180">The platform code is outdated and doesn't implement this API.</span></span>|
| <span data-ttu-id="fbfcb-181">**1万**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-181">**10000**</span></span>| <span data-ttu-id="fbfcb-182">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="fbfcb-182">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="fbfcb-183">戻り値が大きすぎて、プラットフォームのサイズ境界を超えています。</span><span class="sxs-lookup"><span data-stu-id="fbfcb-183">The return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="sample-code-snippets"></a><span data-ttu-id="fbfcb-184">サンプルコードスニペット</span><span class="sxs-lookup"><span data-stu-id="fbfcb-184">Sample code snippets</span></span>

<span data-ttu-id="fbfcb-185">**呼び出し元 `selectMedia` API**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-185">**Calling `selectMedia` API**</span></span>

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

<span data-ttu-id="fbfcb-186">**呼び出し元 `getMedia` API**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-186">**Calling `getMedia` API**</span></span>

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

<span data-ttu-id="fbfcb-187">**`viewImages`ID による呼び出し API**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-187">**Calling `viewImages`  API by ID**</span></span>

```javascript
view images by id:
    assumption: attachmentArray = select Media API Outputlet uriList = [];
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

<span data-ttu-id="fbfcb-188">**URL による viewImages API の呼び出し**</span><span class="sxs-lookup"><span data-stu-id="fbfcb-188">**Calling viewImages API by URL**</span></span>

```javascript
View Images by URL:
    // Assumption 2 urls, url1 and url2let uriList = [];
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
}
```
