---
title: Live Share メディア機能
author: surbhigupta
description: このモジュールでは、Live Share メディア機能、一時停止と待機ポイント、オーディオ ダッキング、ビデオとオーディオの同期の詳細について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 0a1b7a48ffaf0cd71fd0aac2ecf7c1fe2c5970f1
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560590"
---
# <a name="live-share-media-capabilities"></a>Live Share メディア機能

:::image type="content" source="../assets/images/teams-live-share/live-share-media-capabilities-docs-feature-1.png" alt-text="Teams Live Share メディア同期":::

ビデオとオーディオは、現代の世界と職場の重要な部分です。 会議でビデオを一緒に視聴することで、品質、アクセシビリティ、ライセンス保護を向上させるために、より多くのことが可能であるというさまざまなフィードバックが聞こえました。

Live Share SDK を使用すると、わずか数行のコードを使用して、任意の HTML `<video>` と`<audio>`要素に対して堅牢な **メディア同期** が可能になります。 プレイヤーの状態とトランスポート コントロール レイヤーでメディアを同期することにより、アプリで利用できる最高の品質を提供しながら、ビューとライセンスを個別に関連付けることができます。

## <a name="install"></a>インストール

npm を使用して SDK の最新バージョンをアプリケーションに追加するには:

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-media@next --save
```

または

[Yarn](https://yarnpkg.com/) を使用して SDK の最新バージョンをアプリケーションに追加するには:

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-media@next
```

## <a name="media-sync-overview"></a>メディア同期の概要

Live Share SDK には、メディア同期に関連する 2 つの主要なクラスがあります。

| クラス                                                                                        | 説明                                                                                                                                       |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [LiveMediaSession](/javascript/api/@microsoft/live-share-media/livemediasession)     | 独立したメディア ストリームでメディア トランスポート コントロールと再生状態を調整するように設計されたカスタム ライブ オブジェクト。                          |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | インターフェイスを実装`IMediaPlayer`するすべてのオブジェクト (HTML5 `<video>` や -- を使用して `LiveMediaSession`) を`<audio>`同期します。 |

例:

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession } from "@microsoft/live-share-media";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession, IMediaPlayer, MediaPlayerSynchronizer } from "@microsoft/live-share-media";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const mediaSession = container.initialObjects.mediaSession as LiveMediaSession;

// Get the player from your document and create synchronizer
const player: IMediaPlayer = document.getElementById("player") as HTMLVideoElement;
const synchronizer: MediaPlayerSynchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

---

グループの `LiveMediaSession` 再生状態に対する変更を自動的にリッスンします。 `MediaPlayerSynchronizer`によって出力された`LiveMediaSession`状態変更をリッスンし、HTML5 `<video>` や`<audio>`要素などの指定された`IMediaPlayer`オブジェクトに適用します。 バッファー イベントなど、ユーザーが意図的に開始しなかった再生状態の変更を回避するには、プレイヤーから直接ではなく、シンクロナイザーを通じてトランスポート コントロールを呼び出す必要があります。

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

> [!NOTE]
> オブジェクトを使用してメディアを `LiveMediaSession` 手動で同期できますが、通常 `MediaPlayerSynchronizer`は . アプリで使用するプレーヤーによっては、Web プレーヤーのインターフェイスを [IMediaPlayer](/javascript/api/@microsoft/live-share-media/imediaplayer) インターフェイスと一致させるためにデリゲート shim を作成する必要がある場合があります。

## <a name="suspensions-and-wait-points"></a>一時停止と待機ポイント

:::image type="content" source="../assets/images/teams-live-share/live-share-media-out-of-sync.png" alt-text="発表者との一時停止同期を示すスクリーンショット。":::

`LiveMediaSession` オブジェクトの同期を一時的に停止する場合は、一時停止を使用できます。 [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/livemediasessioncoordinatorsuspension) オブジェクトは既定でローカルです。これは、ユーザーが見逃したものに追いついたり、休憩したりする場合に役立ちます。 ユーザーが一時停止を終了すると、同期が自動的に再開されます。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const suspension: MediaSessionCoordinatorSuspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

---

一時停止を開始するときに、オプションの [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint) パラメーターを含めることもできます。これにより、ユーザーは、すべてのユーザーに対して一時停止が発生するタイムスタンプを定義できます。 すべてのユーザーがその待機ポイントの一時停止を終了するまで、同期は再開されません。

待機ポイントが特に便利なシナリオをいくつか次に示します。

- ビデオ内の特定のポイントにクイズやアンケートを追加します。
- 開始前またはバッファリング中に、すべてのユーザーが適切にビデオを読み込むのを待っています。
- 発表者がグループディスカッションのためにビデオ内のポイントを選択できるようにします。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension, CoordinationWaitPoint } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const waitPoint: CoordinationWaitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);

// End the suspension when the user readies up
document.getElementById("ready-up-button")!.onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

---

## <a name="audio-ducking"></a>オーディオ ダッキング

Live Share SDK では、インテリジェントなオーディオ ダッキングがサポートされます。 コードに次を追加することで、アプリケーションでこの機能を使用できます。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer;
meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer: NodeJS.Timeout | undefined;
meeting.registerSpeakingStateChangeHandler((speakingState: meeting.ISpeakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

---

さらに、アプリ マニフェストに次の [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) アクセス許可を追加します。

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

> [!NOTE]
> オーディオ ダッキングに使用される API は `registerSpeakingStateChangeHandler` 、現在、Microsoft Teams デスクトップとスケジュールされた会議の種類でのみ機能します。

## <a name="code-samples"></a>コード サンプル

| サンプルの名前          | 説明                                                                                                                               | JavaScript                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| React ビデオ          | LiveMediaSession オブジェクトが HTML5 ビデオでどのように動作するかを示す基本的な例。                                                        | [表示](https://aka.ms/liveshare-reactvideo)    |
| React メディア テンプレート | 接続されているすべてのクライアントが一緒にビデオを視聴し、共有プレイリストを作成し、誰が管理しているのかを転送し、ビデオに注釈を付けることができるようにします。 | [表示](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Live Share キャンバス](teams-live-share-canvas.md)

## <a name="see-also"></a>関連項目

- [Live Share SDK FAQ](teams-live-share-faq.md)
- [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
- [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
- [会議の Teams アプリ](teams-apps-in-meetings.md)
