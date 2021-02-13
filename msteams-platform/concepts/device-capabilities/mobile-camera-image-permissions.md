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
# <a name="integrate-media-capabilities"></a>メディア機能の統合 

このドキュメントでは、メディア機能を統合する方法について説明します。 この統合は、カメラやマイクなどのネイティブ デバイス機能と Teams **プラットフォームを組** み合わせた機能です。  

アプリがユーザーの [デバイスのアクセス](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)許可にアクセスするために必要なツールを提供する Microsoft Teams JavaScript クライアント SDK を [使用できます](native-device-permissions.md)。 適切な **メディア機能 API** を使用して、Microsoft Teams モバイルアプリ内の Teams プラットフォームにカメラやマイクなどのネイティブ デバイス機能を統合し、より充実したエクスペリエンスを構築します。 

## <a name="advantage-of-integrating-media-capabilities"></a>メディア機能を統合する利点

Teams アプリにデバイス機能を統合する主な利点は、ネイティブの Teams コントロールを活用して、ユーザーに充実した没入型のエクスペリエンスを提供する方法です。
メディア機能を統合するには、アプリ マニフェスト ファイルを更新し、メディア機能 API を呼び出す必要があります。 

効果的に統合するには、ネイティブ メディア機能を使用[](#code-snippets)できる各 API を呼び出すコード スニペットについて理解している必要があります。

Teams アプリでエラーを処理するには [、API 応答エラー](#error-handling) について理解することが重要です。

> [!NOTE] 
> 現在、メディア機能に対する Microsoft Teams のサポートはモバイル クライアントでのみ利用できます。

## <a name="update-manifest"></a>マニフェストを更新する

プロパティを追加し [ 、manifest.jsして、ファイル](../../resources/schema/manifest-schema.md#devicepermissions) に対する Teams アプリの `devicePermissions` 更新を行います `media` 。 これにより、アプリでは、ユーザーがカメラを使って画像をキャプチャする前に必要なアクセス許可をユーザーに要求したり、ギャラリーを開いて添付ファイルとして送信する画像を選択したり、マイクを使って会話を録音することができます。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 関連 **する** Teams API が開始されると、アクセス許可の要求プロンプトが自動的に表示されます。 詳細については、「デバイスのアクセス許可 [を要求する」を参照してください](native-device-permissions.md)。

## <a name="media-capability-apis"></a>メディア機能 API

[selectMedia、getMedia、](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)および[viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) API を使用すると、次のようにネイティブ メディア機能を使用できます。 [](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)

* ネイティブ マイクを **使って** 、ユーザーがデバイスから **音声を録音** (会話の 10 分を録音) できます。
* ネイティブ カメラ コントロール **を使** って、ユーザーが移動 **中に画像を** キャプチャしてアタッチできます。
* ネイティブ ギャラリー の **サポートを使用** して、ユーザーが添付ファイル **としてデバイス イメージを** 選択できます。
* ネイティブイメージ **ビューアー コントロールを使用して、****複数の画像を** 一度にプレビューします。
* SDK **ブリッジを介した** 大きなイメージ転送 (1 MB ~ 50 MB) をサポートします。
* ユーザー **が画像をプレビューおよび編集** できる高度な画像機能をサポートします。
  * カメラを介してドキュメント、ホワイトボード、名刺をスキャンします。
  
> [!IMPORTANT]
>*   タスク モジュール、タブ、個人用アプリなど、複数の Teams サーフェスから API `selectMedia` `getMedia` `viewImages` を呼び出すことができます。 詳細については [、「Teams アプリのエントリ ポイント」を参照してください](../extensibility-points.md)。
>* `selectMedia` マイクとオーディオのプロパティをサポートするために API が拡張されました。

デバイスのメディア機能を有効にするには、次の API のセットを使用する必要があります。

| API      | 説明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Camera)**| この API を使用すると、ユーザーはデバイス **カメラからメディア** をキャプチャまたは選択し、それを Web アプリに返します。 ユーザーは、申請前に画像を編集、トリミング、回転、注釈付け、または描画できます。 **selectMedia** への応答として、Web アプリは選択した画像のメディア ID と、選択したメディアのサムネイルを受け取ります。 この API は [、ImageProps](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) 構成を使用してさらに構成できます。 |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)| selectMedia API [でマイク機能](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) `4` に **アクセスするために mediaType** を設定します。 また、この API を使用すると、ユーザーはデバイスのマイクからオーディオを録音し、録音したクリップを Web アプリに返します。 ユーザーは、提出前に一時停止、再レコーディング、レコーディングプレビューを再生できます。  **selectMedia** への応答として、Web アプリは選択したオーディオ録音のメディア ID を受信します。 <br/> 会話 `maxDuration` の録音時間を分単位で構成する必要がある場合に使用します。 現在のレコーディング時間は 10 分で、その後でレコーディングが終了します。  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| この API は、メディア サイズに関係なく **、selectMedia** API によってキャプチャされたメディアをチャンクで取得します。 これらのチャンクはアセンブルされ、ファイルまたは BLOB として Web アプリに送り返されます。 メディアを小さなチャンクに分割すると、大きなファイル転送が容易です。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| この API を使用すると、ユーザーは画像をスクロール可能なリストとして全画面モードで表示できます。|


**画像機能用の selectMedia API の Web アプリ エクスペリエンス** 
 ![Teams でのデバイスのカメラと画像のエクスペリエンス](../../assets/images/tabs/image-capability.png)

**マイク機能用の selectMedia API の Web アプリ エクスペリエンス** 
 ![マイク機能用の Web アプリ エクスペリエンス](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。 


|エラー コード |  エラー名     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **404** | FILE_NOT_FOUND | 指定されたファイルが特定の場所に見つかりません。|
| **500** | INTERNAL_ERROR | 必要な操作の実行中に内部エラーが発生しました。|
| **1000** | PERMISSION_DENIED |アクセス許可はユーザーによって拒否されます。|
| **2000** |NETWORK_ERROR | ネットワークの問題。|
| **3000** | NO_HW_SUPPORT | 基になるハードウェアは、この機能をサポートしていない。|
| **4000**| INVALID_ARGUMENTS | いくつかの引数は無効です。|
| **5000** | UNAUTHORIZED_USER_OPERATION | ユーザーは、この操作を完了する権限を持てない。|
| **6000** |INSUFFICIENT_RESOURCES | リソースが不足していたので、操作を完了する必要があります。|
|**7000** | THROTTLE | API が頻繁に呼び出されたので、プラットフォームは要求を調整しました。|
|  **8000** | USER_ABORT |ユーザーが操作を中止しました。|
| **9000**| OLD_PLATFORM | プラットフォーム コードは古く、この API は実装されません。|
| **10000**| SIZE_EXCEEDED |  戻り値が大きすぎるので、プラットフォーム サイズの境界を超えました。|

## <a name="code-snippets"></a>コード スニペット

**通話 `selectMedia` カメラを** 使用して画像をキャプチャするための API:

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

**通話 `getMedia` 大きな** メディアをチャンクで取得する API:

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

**通話 `viewImages`API によって返される ID による `selectMedia` API:**

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

**通話 `viewImages`URL 別 API:**

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

**マイク `selectMedia` を `getMedia` 介してオーディオを録音する呼び出しと API:**

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
