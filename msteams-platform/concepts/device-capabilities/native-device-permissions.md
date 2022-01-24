---
title: Microsoft Teams アプリのデバイスアクセス許可を要求する
keywords: Teams アプリ 機能 アクセス許可 デバイス ネイティブ スキャン qr バーコード画像 オーディオ ビデオ
description: スキャン QR、バーコード、画像、オーディオ、ビデオ機能など、通常はユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: e6ee04f47c87df8be7a424993a4f0c916b5a69f3
ms.sourcegitcommit: 55d4b4b721a33bacfe503bc646b412f0e3b0203e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2022
ms.locfileid: "62185457"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのデバイスアクセス許可を要求する

カメラ、マイク、位置情報などのネイティブ デバイス機能を使用して Teams アプリを充実させることができます。 このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法について説明します。

> [!NOTE]
> * Microsoft Teams モバイル アプリ内にメディア機能を統合するには、「[メディア機能を統合する](mobile-camera-image-permissions.md)」を参照してください。
> * QR またはバーコード スキャナー機能を Microsoft Teams モバイル アプリに統合するには、「[QR またはバーコード スキャナー機能を Teams に統合する](qr-barcode-scanner-capability.md)」を参照してください。
> * Microsoft Teams モバイル アプリ内にメディア機能を統合するには、「[メディア機能を統合する](location-capability.md)」を参照してください。

## <a name="native-device-permissions"></a>ネイティブ デバイスのアクセス許可

ネイティブ デバイスの機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。 デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリ構成で同様に機能します。 ユーザーは、デバイスのアクセス許可を管理するために、Teams 設定のアクセス許可ページに移動する必要があります。
デバイスの機能にアクセスすることで、次のような Teams プラットフォームでより豊かなエクスペリエンスを構築できます。

* 画像をキャプチャして表示する。
* QR コードまたはバーコードをスキャンする。
* 短いビデオを録画して共有する。
* オーディオ メモを録音し、後で使用できるように保存する。
* ユーザーの位置情報を使用して、関連情報を表示する。

> [!NOTE]
> * 現在のところ Teams は、マルチウィンドウ アプリ、タブ、および会議のサイド パネルへのデバイスのアクセス許可をサポートしていません。    
> * デバイスのアクセス許可はブラウザーによって異なります。 詳細については、「[ブラウザー デバイスのアクセス許可](browser-device-permissions.md)」を参照してください。

## <a name="access-device-permissions"></a>デバイス アクセス許可へのアクセス

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) は、Teams モバイル アプリがユーザーの[デバイス アクセス許可](#manage-permissions)にアクセスし、より豊かなエクスペリエンスを構築するために必要なツールを提供します。

これらの機能へのアクセスは最新の Web ブラウザーでは標準になっていますが、アプリ マニフェストを更新して、使用する機能について Teams に通知する必要があります。 この更新プログラムを使用すると、アプリが Teams デスクトップ クライアントで実行されているときにアクセス許可を要求できます。

> [!NOTE]
> 現在、Microsoft Teams によるメディア機能と QR バーコード スキャナー機能のサポートは、モバイル クライアントでのみ利用できます。

## <a name="manage-permissions"></a>権限の管理

ユーザーは、特定のアプリへのアクセス許可を **許可** または **拒否** することにより、チーム設定でデバイスのアクセス許可を管理できます。

# <a name="mobile"></a>[モバイル](#tab/mobile)

1. Teams を開きます。
1. [**設定**]  >  [**アプリのアクセス許可**] の順にクリックします。
1. 設定を選択する必要があるアプリを選択します。
1. ご希望の設定を選択します。

    ![デバイスのアクセス許可モバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

1. Teams アプリを開きます。
1. ウィンドウの右上隅にあるプロフィール アイコンを選択します。
1. ドロップダウンメニューから **[設定]** > **[アクセス許可]** を選択します。
1. ご希望の設定を選択します。

   ![デバイスのアクセス許可デスクトップ設定画面](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>アクセス許可を指定する

`devicePermissions` を追加し、アプリケーションで使用する次の 5 つのプロパティのどれかを指定することで、アプリの `manifest.json` を更新します。

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

各プロパティを使用すると、ユーザーに同意を求めるようにダイアログを表示することができます。

| プロパティ      | 説明   |
| --- | --- |
| メディア         | カメラ、マイク、スピーカーの使用、およびメディア ギャラリーへのアクセスの許可。 |
| 位置情報   | ユーザーの位置情報を返すためのアクセス許可。      |
| 通知 | ユーザー通知を送信するためのアクセス許可。      |
| midi          | デジタル楽器との間で MIDI (Musical Instrument Digital Interface) 情報を送受信するための許可。   |
| openExternal  | 外部アプリケーションのリンクを開くためのアクセス許可。  |

## <a name="check-permissions-from-your-app"></a>アプリからアクセス許可を確認する

アプリ マニフェストに `devicePermissions` を追加した後、プロンプトを表示せずに **HTML5 アクセス許可 API** を使用してアクセス許可のチェックを行います。

``` JavaScript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="use-teams-apis-to-get-device-permissions"></a>Teams API を使用してデバイスのアクセス許可を取得する

適切な HTML5 または Teams API を利用して、デバイスのアクセス許可へのアクセスに同意するためのプロンプトを表示します。

> [!IMPORTANT]
> * `camera`、`gallery`、および `microphone`の サポートは、[**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) を介して有効になります。 単一の画像キャプチャには [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。
> * `location` のサポートは、[**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) を介して有効になります。 HTML5 位置情報 API は現在 Teams デスクトップ クライアントで完全にはサポートされていないため、位置情報にはこの `getLocation API` を使用する必要があります。

例:
 * ユーザーに自分の場所にアクセスするように促すには、`getCurrentPosition()` を呼び出す必要があります。

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * デスクトップまたは Web でカメラにアクセスするようにユーザーに促すには、`getUserMedia()` を呼び出す必要があります。

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * モバイルで画像をキャプチャするために、Teams mobile は、`captureImage()` を呼び出すときに許可を求めます。

    ```JavaScript
            function captureImage() {
            microsoftTeams.media.captureImage((error, files) => {
                // If there's any error, an alert shows the error message/code
                if (error) {
                    if (error.message) {
                        alert(" ErrorCode: " + error.errorCode + error.message);
                    } else {
                        alert(" ErrorCode: " + error.errorCode);
                    }
                } else if (files) {
                    image = files[0].content;
                    // Adding this image string in src attr of image tag will display the image on web page.
                    let imageString = "data:" + item.mimeType + ";base64," + image;
                }
            });
        } 
    ```

 * `requestPermission()` を呼び出すと、通知によってユーザーにプロンプトが表示されます。

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* カメラを使用したり、フォト ギャラリーにアクセスしたりするために、`selectMedia()` を呼び出すときに Teams mobile が許可を求めます。

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia(mediaInput, (error, attachments) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         } else if (attachments) {
             // creating image array which contains image string for all attached images. 
             const imageArray = attachments.map((item, index) => {
                 return ("data:" + item.mimeType + ";base64," + item.preview)
             })
         }
     });
    } 
  ```

* マイクを使用するために、Teams mobile は、`selectMedia()` を呼び出すときに許可を求めます。

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         }

         if (attachments) {
             // taking the first attachment  
             let audioResult = attachments[0];

             // setting audio string which can be used in Video tag
             let audioData = "data:" + audioResult.mimeType + ";base64," + audioResult.preview
         }
     });
     }
    ```

* マップ インターフェイスで場所を共有するようユーザーに促すために、Teams mobile は、`getLocation()` を呼び出すときに許可を求めます。

    ```JavaScript 
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[モバイル](#tab/mobile)

   ![タブ モバイル デバイスのアクセス許可プロンプト](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

   ![タブ デスクトップ デバイスのアクセス許可プロンプト](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>ログイン セッション全体でのアクセス許可の動作

デバイスのアクセス許可は、ログイン セッションごとに保存されます。 これは、たとえば別のコンピューターでチームの別のインスタンスにサインインした場合、以前のセッションからのデバイスのアクセス許可が利用できないことを意味します。 したがって、新しいセッションのデバイス権限に再同意する必要があります。 また、Teams からサインアウトするか、Teams のテナントを切り替えると、デバイスのアクセス許可が前回のログイン セッションから削除されることも意味します。  

> [!NOTE]
> ネイティブ デバイスのアクセス許可に同意すると、_現在の_ ログイン セッションでのみ有効になります。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Node.js** |
|---------------|--------------|--------|
|デバイス アクセス許可 | Microsoft Teams タブのサンプル アプリを使用して、デバイスのアクセス許可を示します |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>関連項目

* [ブラウザーのデバイスのアクセス許可](browser-device-permissions.md)
* [Teams でメディア機能を統合する](mobile-camera-image-permissions.md)
* [Teams で QR コードまたはバーコード スキャナー機能を統合する](qr-barcode-scanner-capability.md)
* [Teams で位置情報機能を統合する](location-capability.md)
