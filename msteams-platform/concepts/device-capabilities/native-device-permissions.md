---
title: Microsoft Teams アプリのデバイスのアクセス許可を要求する
keywords: teams アプリの機能のアクセス許可
description: 通常、ユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
ms.topic: how-to
ms.openlocfilehash: e7c5f7ff477bc193924cdf11700c77ae620cd1c0
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449437"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのデバイスのアクセス許可を要求する

カメラ、マイク、場所などのネイティブ デバイス機能を使用して Teams アプリを強化できます。 このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法についてガイドします。

> [!NOTE]
> * Microsoft Teams モバイル アプリにメディア機能を統合するには、「メディア機能の統合 [」を参照してください](mobile-camera-image-permissions.md)。
> * Microsoft Teams モバイル アプリに QR またはバーコード スキャナー機能を統合するには、「Teams に QR またはバーコード スキャナー機能を統合する」 [を参照してください。](qr-barcode-scanner-capability.md)
> * 場所の機能を Microsoft Teams モバイル アプリに統合するには、「場所の機能を統合 [する」を参照してください](location-capability.md)。

## <a name="native-device-permissions"></a>ネイティブ デバイスのアクセス許可

ネイティブ デバイス機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。 デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリ構成で同様に機能します。 ユーザーは、デバイスのアクセス許可を管理するために Teams 設定の [アクセス許可] ページに移動する必要があります。
デバイス機能にアクセスすることで、Teams プラットフォームで次のような豊富なエクスペリエンスを構築できます。
* 画像をキャプチャして表示します。
* QR またはバーコードをスキャンします。
* 短いビデオを記録して共有します。
* オーディオ メモを録音し、後で使用するために保存します。
* ユーザーの位置情報を使用して、関連する情報を表示します。

## <a name="access-device-permissions"></a>デバイスのアクセス許可にアクセスする

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)には、Teams モバイル アプリがユーザーのデバイス[](#manage-permissions)アクセス許可にアクセスし、より豊富なエクスペリエンスを構築するために必要なツールが提供されています。

これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用する機能について Teams に通知する必要があります。 この更新プログラムを使用すると、アプリが Teams デスクトップ クライアントで実行されている間にアクセス許可を要求できます。

> [!NOTE] 
> 現在、Microsoft Teams はメディア機能をサポートし、QR バーコード スキャナー機能はモバイル クライアントでのみ利用できます。

## <a name="manage-permissions"></a>権限の管理

ユーザーは、特定のアプリに対するアクセス許可を許可または拒否を選択して、Teams 設定でデバイスのアクセス許可を管理できます。
 
# <a name="desktop"></a>[デスクトップ](#tab/desktop)

1. Teams アプリを開きます。
1. ウィンドウの右上隅にあるプロファイル アイコンを選択します。
1. ドロップダウン **メニュー**  >  **から [設定の** アクセス許可] を選択します。
1. 目的の設定を選択します。

   ![[デバイスのアクセス許可] デスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

1. Teams を開きます。
1. [設定] **[**  >  **アプリのアクセス許可] に移動します**。
1. 設定を選択する必要があるアプリを選択します。
1. 目的の設定を選択します。

    ![[デバイスのアクセス許可] モバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>アクセス許可を指定する

アプリケーションで使用する 5 つのプロパティのどちらを追加して指定して、アプリ `manifest.json` `devicePermissions` を更新します。

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

各プロパティを使用すると、ユーザーに同意を求めるプロンプトを表示できます。

| プロパティ      | 説明   |
| --- | --- |
| media         | カメラ、マイク、スピーカー、およびアクセス メディア ギャラリーを使用する権限。 |
| 地理位置情報   | ユーザーの場所を返すアクセス許可。      |
| 通知 | ユーザー通知を送信するアクセス許可。      |
| midi          | デジタル楽器から楽器デジタル インターフェイス (MIDI) 情報を送受信する権限。   |
| openExternal  | 外部アプリケーションでリンクを開くアクセス許可。  |

## <a name="check-permissions-from-your-app"></a>アプリからのアクセス許可を確認する

アプリ マニフェスト `devicePermissions` に追加した後、プロンプトを表示せずに **HTML5 アクセス** 許可 API を使用してアクセス許可を確認します。

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

適切な HTML5 または Teams API を活用して、デバイスのアクセス許可にアクセスする同意を得るプロンプトを表示します。

> [!IMPORTANT]
> * をサポート `camera` し `gallery` `microphone` 、selectMedia API を [**使用して有効になります**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。 1 [**つのイメージ キャプチャに captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。
> * getLocation `location` API を使用して [**サポートが有効になります**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。 HTML5 地理位置情報 API は現在 Teams デスクトップ クライアントで完全にサポートされていないので、場所に使用 `getLocation API` する必要があります。

次に例を示します。
 * ユーザーに自分の場所へのアクセスを求めるメッセージを表示するには、次のコマンドを呼び出す必要があります `getCurrentPosition()` 。

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * デスクトップまたは Web 上のカメラにアクセスするようにユーザーに求めるには、次のコマンドを呼び出す必要があります `getUserMedia()` 。

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * モバイルで画像をキャプチャするには、Teams モバイルから次の呼び出し時にアクセス許可を求めるメッセージが表示されます `captureImage()` 。

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * 次の呼び出し時に通知がユーザーに表示されます `requestPermission()` 。

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* カメラを使用するか、フォト ギャラリーにアクセスするには、Teams モバイルが次の呼び出し時にアクセス許可を求めるメッセージを表示します `selectMedia()` 。

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* マイクを使用するには、Teams モバイルから次の呼び出し時にアクセス許可を求めるメッセージが表示されます `selectMedia()` 。

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* マップ インターフェイス上の場所を共有するようにユーザーに求めるメッセージを表示するには、Teams モバイルは次の呼び出し時にアクセス許可を求めるメッセージを表示します `getLocation()` 。

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

## <a name="permission-behavior-across-login-sessions"></a>ログイン セッション間のアクセス許可の動作

デバイスのアクセス許可は、ログイン セッションごとに格納されます。 つまり、別のコンピューターなど、Teams の別のインスタンスにサインインすると、以前のセッションからのデバイスのアクセス許可は使用できません。 したがって、新しいセッションのデバイスのアクセス許可に再同意する必要があります。 また、Teams からサインアウトするか、Teams でテナントを切り替える場合、デバイスのアクセス許可は以前のログイン セッションから削除されます。  

> [!NOTE]
> ネイティブ デバイスのアクセス許可に同意すると、現在のログイン _セッションでのみ有効_ です。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Teams でのメディア機能の統合](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Teams に QR またはバーコード スキャナー機能を統合する](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Teams での場所機能の統合](location-capability.md)
