---
title: Microsoft Teams アプリのデバイスアクセス許可を要求する
keywords: Teams アプリ機能のアクセス許可
description: 通常はユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
ms.topic: how-to
ms.openlocfilehash: 0343754eacbb6088a3e44fa5df8ec90e3b10b076
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231611"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのデバイスアクセス許可を要求する

カメラ、マイク、位置情報などのネイティブ デバイス機能を使用して、Teams アプリを強化できます。 このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法について示します。

> [!NOTE]
> Microsoft Teams モバイル アプリにメディア機能を統合するには、「メディア機能の統合 [」を参照してください](mobile-camera-image-permissions.md)。

## <a name="native-device-permissions"></a>ネイティブ デバイスのアクセス許可

ネイティブ デバイス機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。 デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリ構成で同様に動作します。 ユーザーがデバイスのアクセス許可を管理するには、Teams の設定の [アクセス許可] ページに移動する必要があります。
デバイスの機能にアクセスすることで、Teams プラットフォームで次のような豊富なエクスペリエンスを構築できます。
* 画像をキャプチャして表示します。
* 短いビデオを録画して共有します。
* オーディオ メモを録音し、後で使用するために保存します。
* ユーザーの場所情報を使用して、関連情報を表示します。

## <a name="access-device-permissions"></a>アクセス デバイスのアクセス許可

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)は、Teams モバイル アプリがユーザーのデバイス[](#manage-permissions)のアクセス許可にアクセスし、より豊富なエクスペリエンスを構築するために必要なツールを提供します。

これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用する機能について Teams に通知する必要があります。 この更新プログラムでは、アプリが Teams デスクトップ クライアントで実行されている間にアクセス許可を要求できます。

> [!NOTE] 
> 現在、メディア機能に対する Microsoft Teams のサポートはモバイル クライアントでのみ利用できます。

## <a name="manage-permissions"></a>権限の管理

ユーザーは、特定のアプリに対するアクセス許可を許可または拒否するを選択して、Teams の **設定でデバイス** のアクセス許可を管理できます。
 
# <a name="desktop"></a>[デスクトップ](#tab/desktop)

1. Teams アプリを開きます。
1. ウィンドウの右上隅にあるプロファイル アイコンを選択します。
1. ドロップダウン **メニュー**  >  **から [設定の** アクセス許可] を選択します。
1. 目的の設定を選択します。

   ![デバイスのアクセス許可のデスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

1. Teams を開きます。
1. [設定]**アプリの**  >  **アクセス許可に移動します**。
1. 設定を選択する必要があるアプリを選択します。
1. 目的の設定を選択します。

    ![デバイスのアクセス許可のモバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>アクセス許可を指定する

アプリケーションで使用する 5 つのプロパティの中から、次のプロパティを追加して指定することで、アプリ `manifest.json` `devicePermissions` を更新します。

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

各プロパティを使用すると、ユーザーに同意を求めるメッセージを表示できます。

| プロパティ      | 説明   |
| --- | --- |
| media         | カメラ、マイク、スピーカー、およびメディア ギャラリーへのアクセス許可。 |
| geolocation   | ユーザーの位置情報を返すアクセス許可。      |
| notifications | ユーザー通知を送信するアクセス許可。      |
| midi          | デジタル 音楽機器から、Instrument Instrument Digital Interface (MIDI) 情報を送受信するためのアクセス許可。   |
| openExternal  | 外部アプリケーションでリンクを開く権限。  |

## <a name="check-permissions-from-your-app"></a>アプリからアクセス許可を確認する

アプリ マニフェスト `devicePermissions` に追加した後、プロンプトを表示せずに **HTML5** アクセス許可 API を使用してアクセス許可を確認します。

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

適切な HTML5 または Teams API を利用して、デバイスのアクセス許可にアクセスするための同意を求めるプロンプトを表示します。

> [!IMPORTANT]
> * selectMedia `camera` `gallery` API を通じて `microphone` サポート [**され、有効になります**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。 1 [**つのイメージ キャプチャに captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。
> * getLocation `location` API を使用してサポート [**が有効になります**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。 HTML5 位置情報 API は現在 Teams デスクトップ クライアントで完全にはサポートされていないので、場所に使用する `getLocation API` 必要があります。

以下に例を示します。
 * ユーザーに位置情報へのアクセスを求めるメッセージを表示するには、次のコマンドを呼び出す必要があります `getCurrentPosition()` 。

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * デスクトップまたは Web 上のカメラにアクセスするようにユーザーに求めるには、次を呼び出す必要があります `getUserMedia()` 。

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * モバイルでイメージをキャプチャするために、Teams モバイルは、次を呼び出す際にアクセス許可を求めるメッセージを表示します `captureImage()` 。

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * 通知は、次の呼び出し時にユーザーに表示されます `requestPermission()` 。

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* カメラを使用するか、フォト ギャラリーにアクセスするために、Teams モバイルは次を呼び出す際にアクセス許可を求めるメッセージを表示します `selectMedia()` 。

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* マイクを使用するために、Teams モバイルは通話時にアクセス許可を求めるメッセージを表示します `selectMedia()` 。

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* マップ インターフェイス上の場所を共有するようにユーザーに求めるメッセージを表示するために、Teams モバイルは次を呼び出す際にアクセス許可を求めるメッセージを表示します `getLocation()` 。

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[デスクトップ](#tab/desktop)

   ![タブ デスクトップ デバイスのアクセス許可の確認メッセージ](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

   ![タブ モバイル デバイスのアクセス許可の確認メッセージ](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>ログイン セッション間のアクセス許可の動作

デバイスのアクセス許可は、ログイン セッションごとに格納されます。 つまり、たとえば別のコンピューターで Teams の別のインスタンスにサインインすると、以前のセッションからのデバイスのアクセス許可は使用できません。 したがって、新しいセッションのデバイスのアクセス許可に再同意する必要があります。 また、Teams からサインアウトするか、Teams でテナントを切り替える場合、デバイスのアクセス許可は以前のログイン セッションから削除されます。  

> [!NOTE]
> ネイティブ デバイスのアクセス許可に同意すると、現在のログイン _セッションでのみ有効_ です。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams でのメディア機能の統合](mobile-camera-image-permissions.md)
