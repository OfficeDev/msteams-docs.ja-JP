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
# <a name="camera-and-image-capabilities-in-teams"></a>Teams のカメラおよび画像の機能

>[!IMPORTANT]
>
> * 現時点では、チームのカメラおよびイメージ機能のサポートは、モバイルクライアントでのみ使用できます。
>* 、 `selectMedia` 、 `getMedia` および api は、 `viewImages` タスクモジュール、タブ、個人用アプリなどの複数の Teams の表面から呼び出すことができます。 詳細については、「 [Teams アプリのエントリポイント](../extensibility-points.md) _」を参照してください_。

Microsoft  [teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用すると、microsoft teams モバイルアプリ内でカメラとイメージの機能を簡単に統合できます。 SDK は、ユーザーの [デバイスのアクセス許可](native-device-permissions.md?tabs=desktop#device-permissions) にアクセスし、より充実した操作性を構築するためにアプリに必要なツールを提供します。

[Selectmedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)、 [getmedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)、および[viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) api を使用すると、次のようにネイティブのカメラ/イメージ機能を使用できます。

* ネイティブ **カメラコントロール** を使用して、ユーザーが **画像を取り込ん** で移動できるようにします。
* ネイティブな **ギャラリーサポート** を使用して、ユーザーが **デバイス画像を** 添付ファイルとして選択できるようにします。
* ネイティブ **イメージビューアーコントロール** を使用して、一度に **複数の画像をプレビュー** します。
* SDK ブリッジを使用した **大規模画像転送** (最大 50 MB) のサポート
* ユーザーがイメージをプレビューおよび編集できる **高度なイメージ機能** をサポートします。
  * ドキュメント、ホワイトボード、名刺などのスキャンをカメラから行います。
  * 画像をトリミングして回転させます。
  * 画像にテキスト、インク、またはフリーハンドの注釈を追加します。

## <a name="get-started"></a>作業の開始

プロパティを追加し、を指定することによって、Teams アプリ [manifest.jsをファイルで](../../resources/schema/manifest-schema.md#devicepermissions) 更新し `devicePermissions` `media` ます。 これにより、アプリは、カメラを使用して画像を取得したり、ギャラリーを開いて添付ファイルとして提出する画像を選択したりする前に、エンドユーザーから必要なアクセス許可を要求することができます。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 関連する Teams API が開始されると、 _要求アクセス許可_ のプロンプトが自動的に表示されます。 詳細については、「[要求デバイスのアクセス許可](native-device-permissions.md) *」を参照してください*。

## <a name="using-camera-and-image-capability-apis"></a>カメラおよびイメージ機能 Api の使用

次の Api セットを使用して、カメラおよびイメージデバイスの機能を有効にすることができます。

| API      | 説明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| この API を使用すると、ユーザーは **ネイティブデバイスからメディアをキャプチャまたは選択** して、web アプリに戻ることができます。 ユーザーは、送信前に画像の編集、トリミング、回転、注釈、描画を選択できます。 **Selectmedia** への応答として、web アプリは選択した画像のメディア id を受け取り、選択されたメディアのサムネイルを受信することがあります。 |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| この API は、サイズに関係なくチャンク内のメディアを取得します。 これらのチャンクはアセンブルされ、ファイル/blob として web アプリに返されます。 この API を使用すると、画像が小さいチャンクに分割されて大きな画像転送が容易になります。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| この API を使用すると、画像の全画面表示モードをスクロール可能なリストとして表示できます。|

**SelectMedia API** 
 ![ の Web アプリの使用感Teams でのデバイスカメラおよびイメージの利用感](../../assets/images/tabs/image-capability-screenshot.jpg)

## <a name="error-handling"></a>エラー処理

API 応答エラーコードを理解し、それらを適切に処理する必要があります。 プラットフォームによって返される可能性のあるエラーコードの一覧を以下に示します。

|エラー コード |  エラー名     | Condition|
| --- | --- | --- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **404** | FILE_NOT_FOUND | 指定したファイルが指定した場所に見つかりませんでした。|
| **500** | INTERNAL_ERROR | 必要な操作の実行中に内部エラーが発生しました。|
| **1000** | PERMISSION_DENIED |ユーザーによって拒否されたアクセス許可。|
| **2000** |NETWORK_ERROR | ネットワークの問題。|
| **3000** | NO_HW_SUPPORT | 基礎となるハードウェアは、機能をサポートしていません。|
| **4000**| INVALID_ARGUMENTS | 1つ以上の引数が無効です。|
| **5000** | UNAUTHORIZED_USER_OPERATION | ユーザーがこの操作を完了する権限がありません。|
| **6000** |INSUFFICIENT_RESOURCES | リソースが不足しているため、操作を完了できませんでした。|
|**7000** | THROTTLE | API が頻繁に呼び出されていないため、要求が調整されました。|
|  **8000** | USER_ABORT |ユーザーが操作を中止しました。|
| **9000**| OLD_PLATFORM | プラットフォームコードは古く、この API は実装されていません。|
| **1万**| SIZE_EXCEEDED |  戻り値が大きすぎて、プラットフォームのサイズ境界を超えています。|

## <a name="sample-code-snippets"></a>サンプルコードスニペット

**呼び出し元 `selectMedia` API**

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

**呼び出し元 `getMedia` API**

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

**`viewImages`ID による呼び出し API**

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

**URL による viewImages API の呼び出し**

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
