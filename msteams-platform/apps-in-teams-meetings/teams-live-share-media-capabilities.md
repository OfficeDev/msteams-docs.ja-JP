---
title: Live Share メディア機能
description: このモジュールでは、Live Share メディア機能、一時停止と待機ポイント、オーディオ ダッキング、ビデオとオーディオの同期の詳細について説明します。
ms.topic: concept
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 662a0204793eaf2ef4702a447a4a61c79964112c
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142480"
---
---

# <a name="live-share-media-capabilities"></a>Live Share メディア機能

ビデオとオーディオは、現代の世界と職場の重要な部分です。 会議で一緒にビデオを視聴することに関して、品質、アクセシビリティ、およびライセンス保護を向上させるためにできることがもっとあるという幅広いフィードバックが寄せられています。

Live Share SDK を使用すると、これまでになく簡単に HTML `<video>` および `<audio>` 要素への **メディア同期** が可能になります。 プレイヤーの状態とトランスポート コントロール レイヤーでメディアを同期することにより、アプリで利用できる最高の品質を提供しながら、ビューとライセンスを個別に関連付けることができます。

## <a name="install"></a>インストール

npm を使用して SDK の最新バージョンをアプリケーションに追加するには:

```bash
npm install @microsoft/live-share --save
npm install @microsoft/live-share-media --save
```

または

[Yarn](https://yarnpkg.com/) を使用して SDK の最新バージョンをアプリケーションに追加するには:

```bash
yarn add @microsoft/live-share
yarn add @microsoft/live-share-media
```

## <a name="media-sync-overview"></a>メディア同期の概要

Live Share SDK には、メディア同期に関連する 2 つの主要なクラスがあります。

| クラス                                                                                                                  | 説明                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| [EphemeralMediaSession](/javascript/api/@microsoft/live-share-media/ephemeralmediasession)     | 独立したメディア ストリームでメディア トランスポート コントロールと再生状態を調整するように設計されたカスタム エフェメラル オブジェクト。 |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | ローカルの HTML メディア要素を `EphemeralMediaSession` のリモート HTML メディア要素のグループと同期します。|

例:

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { EphemeralMediaSession } from "@microsoft/live-share-media";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Setup the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { mediaSession: EphemeralMediaSession },
};
const { container } = await client.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = ["Organizer", "Presenter"];
await mediaSession.start(allowedRoles);
```

`EphemeralMediaSession` は、グループの再生状態の変更を自動的にリッスンし、`MediaPlayerSynchronizer` を通じて変更を適用します。 バッファー イベントなど、ユーザーが意図的に開始しなかった再生状態の変更を回避するには、プレイヤーから直接ではなく、シンクロナイザーを通じてトランスポート コントロールを呼び出す必要があります。

例:

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
  <div class="player-controls">
    <button id="play-button">Play</button>
    <button id="pause-button">Pause</button>
    <button id="restart-button">Restart</button>
    <button id="change-track-button">Change track</button>
  </div>
</body>
```

```javascript
// ...

document.getElementById("play-button").onclick = () => {
  synchronizer.play();
};

document.getElementById("pause-button").onclick = () => {
  synchronizer.pause();
};

document.getElementById("restart-button").onclick = () => {
  synchronizer.seekTo(0);
};

document.getElementById("change-track-button").onclick = () => {
  synchronizer.setTrack({
    trackIdentifier: "SOME_OTHER_VIDEO_SRC",
  });
};
```

 > [!Note]
 > `EphemeralMediaSession` オブジェクトを使用してメディアを直接同期することはできますが、同期ロジックをより細かく制御する必要がない限り、`MediaPlayerSynchronizer` を使用します。 アプリで使用するプレイヤーによっては、委任シムを作成して、Web プレイヤーのインターフェイスを HTML メディア インターフェイスと一致させることができます。

## <a name="suspensions-and-wait-points"></a>一時停止と待機ポイント

`EphemeralMediaSession` オブジェクトの同期を一時的に停止する場合は、一時停止を使用できます。 [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/ephemeralmediasessioncoordinatorsuspension) オブジェクトは既定でローカルです。これは、ユーザーが見逃したものに追いついたり、休憩したりする場合に役立ちます。 ユーザーが一時停止を終了すると、同期が自動的に再開されます。

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

一時停止を開始するときに、オプションの [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint) パラメーターを含めることもできます。これにより、ユーザーは、すべてのユーザーに対して一時停止が発生するタイムスタンプを定義できます。 すべてのユーザーがその待機ポイントの一時停止を終了するまで、同期は再開されません。 これは、ビデオの特定のポイントでクイズや調査を追加する場合などに役立ちます。

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension();
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

## <a name="audio-ducking"></a>オーディオ ダッキング

Live Share SDK では、インテリジェントなオーディオ ダッキングがサポートされます。 アプリケーションで _試験的_ な機能を使用し、次をコードに追加できます。

```javascript
import * as microsoftTeams from "@microsoft/teams-js";

// ...

let volumeTimer;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

オーディオ ダッキングを有効にするには、アプリ マニフェストに次の [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) アクセス許可を追加します。

```json
{
  // ...rest of your manifest here
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Chat",
          "type": "Delegated"
        },
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

> [!Note]
> オーディオ ダッキングに使用される `registerSpeakingStateChangeHandler` API は、現在、話している非ローカル ユーザーに対してのみ機能します。

## <a name="code-samples"></a>コード サンプル

| サンプルの名前   | 説明 | JavaScript |
| -------------------- | ----------------------------| -----------------|
| React ビデオ          | EphemeralMediaSession オブジェクトが HTML5 ビデオでどのように機能するかを示す基本的な例。                                                        | [表示](https://aka.ms/liveshare-reactvideo)    |
| React メディア テンプレート | 接続されているすべてのクライアントが一緒にビデオを視聴し、共有プレイリストを作成し、誰が管理しているのかを転送し、ビデオに注釈を付けることができるようにします。 | [表示](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アジャイル ポーカー チュートリアル](../sbs-teams-live-share.yml)

## <a name="see-also"></a>関連項目

* [Live Share SDK FAQ](teams-live-share-faq.md)
* [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
* [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
* [リファレンス ドキュメント](https://aka.ms/livesharedocs)
* [会議の Teams アプリ](teams-apps-in-meetings.md)
