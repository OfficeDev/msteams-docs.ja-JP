---
title: Microsoft Teams タブのデバイスへのアクセス許可を要求する
description: 通常、ユーザーの同意を必要とするネイティブ機能へのアクセスを要求するためにアプリのマニフェストを更新する方法
keywords: teams タブの開発
ms.openlocfilehash: f0e19c0ed716147c097137c4ef0bf3454783b2eb
ms.sourcegitcommit: c4a7bc638e848a702cce92798cba84917fcecc35
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "42928518"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Microsoft Teams タブのデバイスへのアクセス許可を要求する

次のような、ネイティブデバイスへのアクセスを必要とする機能を使用して、タブを充実させることができます。

* デジタル
* マイク
* 場所
* 通知

![デバイスアクセス許可の設定画面](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> ネイティブデバイスの機能は、現在、モバイルクライアントのタブではサポートされていませんが、完全なサポートは近日予定されています。 この変更を準備するには、タブを作成するときに[[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従ってください。 個人用アプリ (静的タブ) は現在、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。
>
> タブの完全なサポートがリリースされると、次のようになります。
>
> * すべてのタブがモバイルで常に使用できるようになります。
> * `contentUrl` **は、モバイル Teams クライアントにロードされ**ます。
> * [チャネル/グループ] タブでは、ユーザーは自分`websiteUrl`のを経由して別のブラウザーで`contentUrl`タブを開くことができます。ただし、は最初に読み込まれます。  

## <a name="device-permissions"></a>デバイス アクセス許可

ユーザーのデバイスのアクセス許可にアクセスすると、次のように、より高度なエクスペリエンスを構築できます。

* 短いビデオを録音および共有する
* 短い音声メモを録音し、後で保存する
* ユーザーの場所情報を使用して関連情報を表示する

これらの機能へのアクセスは、ほとんどのモダン web ブラウザーで標準になっていますが、アプリマニフェストを更新することによって、使用する機能を Teams に知らせる必要があります。 これにより、アプリが Teams デスクトップクライアント上で実行されているときに、ブラウザーと同じ方法でアクセス許可を要求することができます。

## <a name="properties"></a>プロパティ

アプリケーションで使用する`manifest.json` 5 つ`devicePermissions`のプロパティを追加して指定することにより、アプリを更新します。

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

各プロパティによって、ユーザーに同意を求めるように求めるメッセージを表示することができます。

| プロパティ      | 説明   |
| --- | --- |
| 書き込め         | カメラ、マイク、およびスピーカーを使用するためのアクセス許可 |
| 地理位置情報   | ユーザーの場所を返すためのアクセス許可      |
| 受け取る | ユーザー通知を送信するためのアクセス許可      |
| 次回          | デジタル音楽機器から midi 情報を送受信するためのアクセス許可   |
| openExternal  | 外部アプリケーションでリンクを開くためのアクセス許可  |

## <a name="checking-permissions-from-your-tab"></a>タブから権限を確認する

アプリマニフェストに追加`devicePermissions`した後は、メッセージを表示せずに、HTML5 の "PERMISSIONS" API を使用してアクセス許可を確認できます。

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

デバイスのアクセス許可にアクセスするための同意を得るためのプロンプトを表示するには、適切な HTML5 API を利用する必要があります。 たとえば、ユーザーにカメラへのアクセスを要求するために、を呼び出す必要があります。`getUserMedia`

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

呼び出し時に地理位置情報にアクセス許可プロンプトが表示される`getCurrentPosition`

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

を呼び出したときに通知が表示されます。`requestPermission`

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![タブのデバイスアクセス許可のプロンプト](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a>ログインセッション間でのアクセス許可の動作

ネイティブデバイスのアクセス許可は、ログインセッションごとに保存されます。 これは、別の Teams インスタンス (別のコンピューターでは、) にログインすると、以前のセッションからのデバイスのアクセス許可が使用できなくなることを意味します。 代わりに、新しいログイン設定に対するデバイスのアクセス許可への同意を再度受ける必要があります。 これはつまり、Teams からログアウトした場合 (または Teams 内でテナントを切り替える場合)、その前回のログインセッションでデバイスのアクセス許可が削除されることを意味します。 ネイティブデバイスのアクセス許可を開発する場合は、次の点に注意してください。同意するネイティブの機能は、_現在_のログイン設定に対してのみ使用できます。