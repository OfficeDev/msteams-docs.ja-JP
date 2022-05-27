---
title: メディア機能を統合する
author: Rajeshwari-v
description: コード例を使用して、Teams JavaScript クライアント SDK を使用してメディア機能を有効にする方法について説明します
keywords: カメラ イメージ マイク機能ネイティブ デバイスのアクセス許可メディア API
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: a65f39d3796bc0dacaa80f6badba7a011716edbf
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756759"
---
# <a name="integrate-media-capabilities"></a>メディア機能を統合する

**カメラ** や **マイク** など、Teams アプリと統合できるネイティブ デバイス機能。 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を使用できます。これは、アプリがユーザーの [ネイティブ デバイス機能](native-device-permissions.md) にアクセスするために必要なツールを提供します。 適切なメディア機能 API を使用して、**カメラ** や **マイク** などのデバイス機能を Microsoft Teams モバイル アプリ内の Teams プラットフォームと統合し、より豊富なエクスペリエンスを構築します。

## <a name="advantage-of-integrating-media-capabilities"></a>メディア機能を統合する利点

Teams アプリにデバイス機能を統合する主な利点は、ネイティブ Teams コントロールを利用して、ユーザーに豊富でイマーシブなエクスペリエンスを提供することです。
メディア機能を統合するには、アプリ マニフェスト ファイルを更新し、メディア機能 API を呼び出す必要があります。

効果的な統合を実現するには、ネイティブ メディア機能を使用できる、それぞれの API を呼び出すための [コード スニペット](#code-snippets) を十分に理解している必要があります。

Teams アプリのエラーを処理するには[、API 応答エラー](#error-handling)について理解しておくことが重要です。

> [!NOTE]
>
> * 現在、メディア機能のサポートMicrosoft Teamsは、モバイル クライアントでのみ使用できます。
> * 現在のところ Teams は、マルチウィンドウ アプリ、タブ、および会議のサイド パネルへのデバイスのアクセス許可をサポートしていません。
> * デバイスのアクセス許可はブラウザーによって異なります。 詳細については、「[ブラウザー デバイスのアクセス許可](browser-device-permissions.md)」を参照してください。

## <a name="update-manifest"></a>マニフェストを更新する

`devicePermissions` プロパティを追加して `media` を指定することにより、Teamsアプリの [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) ファイルを更新します。 これにより、アプリは、 **カメラ** を使用して画像をキャプチャする前にユーザーに必要なアクセス許可を要求したり、ギャラリーを開いて添付ファイルとして送信する画像を選択したり、 **マイク** を使用して会話を記録したりできます。 アプリ マニフェストの更新プログラムは次のとおりです。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> **アクセス許可要求** プロンプトは、関連する Teams API が開始されると自動的に表示されます。 詳細については、「[デバイスのアクセス許可要求](native-device-permissions.md)」 を参照してください。

## <a name="media-capability-apis"></a>メディア機能 API

[selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)、[getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)、[viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API を使用すると、ネイティブ メディア機能を次のように使用できます。

* ネイティブ **マイク** を使用して、ユーザーがデバイスから **オーディオを録音** (10 分間の会話を録音) できるようにします。
* ネイティブ **カメラ コントロール** を使用して、ユーザーが外出先で **画像をキャプチャおよびアタッチ** できるようにします。
* ネイティブ **ギャラリーのサポート** を使用して、ユーザーが添付ファイルとして **デバイス イメージを選択** できるようにします。
* ネイティブ **イメージ ビューアー コントロール** を使用して、一度に **複数のイメージをプレビュー** します。
* SDK ブリッジを介した **大規模なイメージ転送** (1 MB から 50 MB) をサポートします。
* **高度なイメージ機能** をサポートすると、ユーザーは画像をプレビューおよび編集できます。
  * カメラを使用してドキュメント、ホワイトボード、名刺をスキャンします。
  
> [!IMPORTANT]
>
> * `selectMedia`、`getMedia`、および `viewImages` API は、タスク モジュール、タブ、個人用アプリなど、複数の Teams サーフェスから呼び出すことができます。 詳細については、「[Teams アプリのエントリ ポイント](../extensibility-points.md)」を参照してください。
> * `selectMedia` マイクとオーディオのプロパティをサポートするように API が拡張されました。

デバイスのメディア機能を有効にするには、次の API セットを使用する必要があります。

| API      | 説明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**カメラ)**| この API を使用すると、ユーザーは **デバイス カメラからメディアをキャプチャまたは選択** し、それを Web アプリに返すことができます。 ユーザーは、送信前に画像の編集、トリミング、回転、注釈付け、または描画を行うことができます。 `selectMedia` に対応して、Web アプリは、選択した画像のメディア ID と、選択したメディアのサムネイルを受信します。 この API は、 [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) 構成を使用してさらに構成できます。 |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**マイク**)| マイク機能にアクセスするには、`selectMedia` API で [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) を `4` に設定します。 この API を使用すると、ユーザーはデバイスのマイクからオーディオを録音し、記録されたクリップを Web アプリに返すこともできます。 ユーザーは、送信前に記録プレビューを一時停止、再記録、再生できます。  **selectMedia** に応答して、Web アプリは選択されたオーディオ録音のメディア ID を受け取ります。 <br/> 会話を記録するための期間を分単位で構成する必要がある場合は、`maxDuration` を使用します。 現在の記録時間は 10 分です。その後、記録は終了します。  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| この API は、メディア サイズに関係なく、`selectMedia` API によってキャプチャされたメディアをチャンク単位で取得します。 これらのチャンクは、ファイルまたは BLOB として組み立てられ、Web アプリに送り返されます。 メディアを小さなチャンクに分割すると、大きなファイル転送が容易になります。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| この API を使用すると、ユーザーはスクロール可能なリストとして全画面表示モードで画像を表示できます。|

次の図は、イメージ機能用の `selectMedia` API の Web アプリ エクスペリエンスを示しています。

![Teams でのデバイス カメラと画像のエクスペリエンス](../../assets/images/tabs/image-capability.png)

次の図は、マイク機能に対する `selectMedia` API の Web アプリ エクスペリエンスを示しています。

![QR またはバーコード スキャナー機能の Web アプリ エクスペリエンス](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **404** | FileNotFound | 指定されたファイルが指定された場所に見つかりません。|
| **500** | 内部エラーです(_E) | 必要な操作の実行中に内部エラーが発生しました。|
| **1000** | PERMISSION_DENIED |アクセス許可がユーザーによって拒否されました。|
| **3000** | NO_HW_SUPPORT | 基になるハードウェアでは、この機能はサポートされていません。|
| **4000**| 引数が無効です | いくつかの引数は無効です。|
|  **8000** | USER_ABORT |ユーザーが操作を中止します。|
| **9000**| OLD_PLATFORM | プラットフォーム コードは古く、この API は実装されていません。|
| **10,000**| SIZE_EXCEEDED |  戻り値が大きすぎて、プラットフォーム サイズの境界を超えています。|

## <a name="code-snippets"></a>コード スニペット

**カメラを使用して画像をキャプチャするための `selectMedia`API** を呼び出す:

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

**大きなメディアをチャンクで取得するために `getMedia`API** を呼び出す:

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

**`selectMedia` API** によって返されたIDによる`viewImages`API を呼び出す:

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

**URL** による `viewImages` API を呼び出す:

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

**マイクを介して音声を録音するための `selectMedia` および `getMedia` API の呼び出し**:

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

## <a name="see-also"></a>関連項目

* [Teams で QR コードまたはバーコード スキャナー機能を統合する](qr-barcode-scanner-capability.md)
* [Teams で位置情報機能を統合する](location-capability.md)
* [Teams でユーザー ピッカーを統合する](people-picker-capability.md)
* [アプリケーションでホストされるメディア ボットの要件と考察](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
