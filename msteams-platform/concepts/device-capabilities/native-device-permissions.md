---
title: Microsoft Teams アプリのデバイスのアクセス許可を要求する
keywords: チーム アプリの機能のアクセス許可
description: 通常はユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 34f84285dc883cc474cf1720c42b1699f76c6653
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566181"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのデバイスのアクセス許可を要求する

カメラ、マイク、位置情報などのネイティブデバイス機能を使用して、Teamsアプリを強化できます。 このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法について説明します。

> [!NOTE]
> * Microsoft Teamsモバイル アプリ内でメディア機能を統合するには、「[メディア](mobile-camera-image-permissions.md)機能の統合」を参照してください。
> * Microsoft Teamsモバイル アプリ内で QR またはバーコード スキャナー機能を統合するには[、qr またはバーコード スキャナーの機能を Teams に統合](qr-barcode-scanner-capability.md)するを参照してください。
> * Microsoft Teamsモバイルアプリ内で位置情報機能を統合するには、「[位置情報機能の統合](location-capability.md)」を参照してください。

## <a name="native-device-permissions"></a>ネイティブ デバイスのアクセス許可

ネイティブ デバイス機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。 デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリコンストラクトで同様に機能します。 ユーザーは、デバイスのアクセス許可を管理するために、Teams設定のアクセス許可ページに移動する必要があります。
デバイス機能にアクセスすることで、Teams プラットフォームで次のような豊富なエクスペリエンスを構築できます。
* 画像をキャプチャして表示します。
* QRまたはバーコードをスキャンします。
* 短い動画を録画して共有する。
* オーディオメモを録音し、後で使用するためにそれらを保存します。
* ユーザーの位置情報を使用して、関連情報を表示します。

## <a name="access-device-permissions"></a>デバイスのアクセス許可にアクセスする

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)には、Teamsモバイル アプリがユーザーの[デバイスのアクセス許可](#manage-permissions)にアクセスし、より充実したエクスペリエンスを構築するために必要なツールが用意されています。

これらの機能へのアクセスは、最新の Web ブラウザーでは標準的ですが、アプリ マニフェストを更新して、使用する機能についてTeamsに通知する必要があります。 この更新プログラムを使用すると、アプリがTeams デスクトップ クライアントで実行されている間にアクセス許可を要求できます。

> [!NOTE] 
> 現在、メディア機能とQRバーコードスキャナ機能のMicrosoft Teamsサポートは、モバイルクライアントでのみ利用できます。

## <a name="manage-permissions"></a>権限の管理

ユーザーは、特定のアプリに対するアクセス許可を **許可** または **拒否** を選択して、Teams設定でデバイスのアクセス許可を管理できます。
 
# <a name="desktop"></a>[デスクトップ](#tab/desktop)

1. Teams アプリを開きます。
1. ウィンドウの右上隅にあるプロフィールアイコンを選択します。
1. ドロップダウン メニューから **[**  >  **権限** 設定]を選択します。
1. 希望の設定を選択します。

   ![デバイスのアクセス許可デスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

1. Teamsを開きます。
1.   >  **[アプリのアクセス許可設定] に** 移動します。
1. 設定を選択する必要があるアプリを選択します。
1. 希望の設定を選択します。

    ![デバイスのアクセス許可 モバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>アクセス許可の指定

`manifest.json`アプリケーションで使用する 5 `devicePermissions` つのプロパティのうち、どれを追加して指定してアプリを更新します。

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

各プロパティを使用すると、ユーザーに同意を求めるよう求めることができます。

| プロパティ      | 説明   |
| --- | --- |
| media         | カメラ、マイク、スピーカー、およびアクセス メディア ギャラリーを使用する権限。 |
| 地理位置情報   | ユーザーの場所を返すアクセス許可。      |
| 通知 | ユーザー通知を送信する権限。      |
| ミディ          | デジタル楽器から楽器デジタルインターフェイス(MIDI)情報を送受信する権限。   |
| オープン外部  | 外部アプリケーションでリンクを開く権限。  |

## <a name="check-permissions-from-your-app"></a>アプリからアクセス許可を確認する

アプリ `devicePermissions` マニフェストに追加した後、プロンプトを表示せずに **HTML5 アクセス許可 API** を使用してアクセス許可を確認します。

``` Javascript
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

適切な HTML5 またはTeams API を活用して、デバイスのアクセス許可へのアクセスに同意するためのプロンプトを表示します。

> [!IMPORTANT]
> * のサポート `camera` `gallery` 、 および `microphone` は [**、 [メディア API] を選択**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)して有効にします。 1 つのイメージ キャプチャに [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。
> * のサポート `location` は [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)を通じて有効になります。 `getLocation API`HTML5 地理位置情報 API は現在、デスクトップ クライアントでは完全にサポートされていないので、この場所Teams使用する必要があります。

例:
 * ユーザーに自分の場所にアクセスするよう求めるには、 を呼び出す必要があります `getCurrentPosition()` 。

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * デスクトップまたは Web 上でカメラにアクセスするようユーザーに求めるには、 を呼び出す必要があります `getUserMedia()` 。

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * モバイルで画像をキャプチャするには、モバイルTeams電話時に許可を求めます `captureImage()` 。

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * お問い合いの際に、通知を受け取るとユーザーにメッセージが表示 `requestPermission()` されます。

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* カメラを使用したり、フォトギャラリーにアクセスするには、モバイルTeamsあなたが呼び出すときに許可を求めます `selectMedia()` :

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* マイクを使用するには、携帯電話Teams電話時に許可を求めます `selectMedia()` :

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* マップ インターフェイスで場所を共有するようにユーザーに確認するには、モバイルTeams、電話時に許可を求めます `getLocation()` 。

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[デスクトップ](#tab/desktop)

   ![タブ デスクトップ デバイスのアクセス許可のプロンプト](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

   ![タブ モバイル デバイスのアクセス許可のプロンプト](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>ログイン セッション間でのアクセス許可の動作

デバイスのアクセス許可は、ログイン セッションごとに保存されます。 つまり、Teamsの別のインスタンス (たとえば、別のコンピューター) にサインインした場合、以前のセッションからのデバイスのアクセス許可は利用できません。 したがって、新しいセッションのデバイスのアクセス許可に再同意する必要があります。 また、TeamsでTeamsからサインアウトしたりテナントを切り替えたりすると、デバイスのアクセス許可は前回のログイン セッションから削除されます。  

> [!NOTE]
> ネイティブデバイスのアクセス許可に同意すると、 _現在_ のログインセッションでのみ有効です。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Teamsでのメディア機能の統合](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [TeamsでQRまたはバーコードスキャナ機能を統合](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Teamsでの位置情報機能の統合](location-capability.md)
