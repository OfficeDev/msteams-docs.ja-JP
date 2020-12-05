---
title: Microsoft Teams タブのデバイスへのアクセス許可を要求する
description: 通常、ユーザーの同意を必要とするネイティブ機能へのアクセスを要求するためにアプリのマニフェストを更新する方法
keywords: teams タブの開発
ms.openlocfilehash: d6c66525ab0e81f0632df5e2c323926279e38a8e
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576881"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Microsoft Teams タブのデバイスへのアクセス許可を要求する

次のような、ネイティブデバイスへのアクセスを必要とする機能を使用して、タブを充実させることができます。

> [!div class="checklist"]
>
> * デジタル
> * マイク
> * Location
> * 通知

> [!IMPORTANT]
>
> * 現時点では、Teams モバイルクライアント `camera` `location`  はネイティブデバイス機能のみをサポートしており、タブを含むすべてのアプリ構成要素で利用できます。 </br>
> * `camera`画像キャプチャのサポートは、 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)によって有効になります。
> * 現時点では、すべてのデスクトップクライアントで、 [**地理位置情報 API**](../../resources/schema/manifest-schema.md#devicepermissions) は完全にはサポートされていません。

## <a name="device-permissions"></a>デバイス アクセス許可

ユーザーのデバイスのアクセス許可にアクセスすると、次のように、より高度なエクスペリエンスを構築できます。

* 短いビデオを録音および共有する
* 短い音声メモを録音し、後で保存する
* ユーザーの場所情報を使用して関連情報を表示する

これらの機能へのアクセスは、ほとんどのモダン web ブラウザーで標準になっていますが、アプリマニフェストを更新することによって、使用する機能を Teams に知らせる必要があります。 これにより、アプリが Teams デスクトップクライアント上で実行されているときに、ブラウザーと同じ方法でアクセス許可を要求することができます。

## <a name="manage-permissions"></a>権限の管理

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

1. Teams を開きます。
1. ウィンドウの右上隅で、プロファイルアイコンを選択します。
1. **Settings**  ->  ドロップダウンメニューから [設定]**アクセス許可** を選択します。
1. 目的の設定を選択します。

![デバイスアクセス許可のデスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

1. Teams を開きます。
1. 画面の左上隅で、[&#9776;] メニューアイコンを選択します。
1. [**設定** デバイス] を選択し  ->  **Devices** ます。
1. 目的の設定を選択します。

![デバイスのアクセス許可のモバイル設定画面](../../assets/images/tabs/mobile-device-permissions-screen.png)

---

## <a name="properties"></a>プロパティ

`manifest.json` `devicePermissions` アプリケーションで使用する5つのプロパティを追加して指定することにより、アプリを更新します。

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```
> [!Note]
>
> メディアは、モバイルのカメラのアクセス許可にも使用されます。

各プロパティによって、ユーザーに同意を求めるように求めるメッセージを表示することができます。

| プロパティ      | 説明   |
| --- | --- |
| media         | カメラ、マイク、およびスピーカーを使用するためのアクセス許可 |
| 地理位置情報   | ユーザーの場所を返すためのアクセス許可      |
| 受け取る | ユーザー通知を送信するためのアクセス許可      |
| 次回          | デジタル音楽機器から midi 情報を送受信するためのアクセス許可   |
| openExternal  | 外部アプリケーションでリンクを開くためのアクセス許可  |

## <a name="checking-permissions-from-your-tab"></a>タブから権限を確認する

アプリマニフェストに追加した後 `devicePermissions` は、メッセージを表示せずに、HTML5 の "permissions" API を使用してアクセス許可を確認できます。

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

## <a name="prompting-the-user"></a>ユーザーに確認を求める

デバイスのアクセス許可にアクセスするための同意を得るためのプロンプトを表示するには、適切な HTML5 API または Teams API を利用する必要があります。 たとえば、ユーザーにカメラへのアクセスを要求するために、を呼び出す必要があります。 `getCurrentPosition`

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

デスクトップまたは web でカメラを使用するために、Teams は、getUserMedia を呼び出すときにアクセス許可を求めるメッセージを表示します。

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

モバイルで画像をキャプチャするために、Teams mobile は captureImage () を呼び出したときにアクセス許可を要求します。

```Typescript
function captureImage(callback: (error: SdkError, files: File[]) => void)
```

を呼び出したときに通知が表示されます。 `requestPermission`

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![タブのデバイスアクセス許可のプロンプト](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a>ログインセッション間でのアクセス許可の動作

ネイティブデバイスのアクセス許可は、ログインセッションごとに保存されます。 これは、別の Teams インスタンス (別のコンピューターでは、) にログインすると、以前のセッションからのデバイスのアクセス許可が使用できなくなることを意味します。 代わりに、新しいログインセッションのデバイスアクセス許可への同意を再度受ける必要があります。 これはつまり、Teams からログアウトした場合 (または Teams 内でテナントを切り替える場合)、その前回のログインセッションでデバイスのアクセス許可が削除されることを意味します。 ネイティブデバイスのアクセス許可を開発する場合は、次の点に注意してください。同意するネイティブの機能は、 _現在_ のログインセッションにのみ使用されます。
