---
title: Live Share の使用を開始する
author: surbhigupta
description: このモジュールでは、Live Share SDK 機能、RSC アクセス許可、および一時データ構造の詳細について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 35b39f062bcdaf79e0c32d33260dbd0940a4fe2c
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425604"
---
# <a name="live-share-core-capabilities"></a>Live Share コア機能

Live Share SDK は、最小限の労力で会議拡張機能の `sidePanel` と `meetingStage` コンテキストに追加できます。 この記事では、Live Share SDK をアプリに統合する方法と、SDK の主な機能を中心に説明します。

> [!NOTE]
> 現在、スケジュールされた会議のみがサポートされており、すべての参加者が会議予定表に登録している必要があります。 現在、1 対 1 の通話、グループ通話、今すぐ会議などの会議の種類はサポートされていません。

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-dashboard.png" alt-text="Teams Live Share":::

## <a name="install-the-javascript-sdk"></a>JavaScript SDK をインストールする

[Live Share SDK](https://github.com/microsoft/live-share-sdk) は、[npm](https://www.npmjs.com/package/@microsoft/live-share) に発行された JavaScript パッケージであり、npm または Yarn からダウンロードできます。

### <a name="npm"></a>npm

```bash
npm install @microsoft/live-share --save
```

### <a name="yarn"></a>糸

```bash
yarn add @microsoft/live-share
```

## <a name="register-rsc-permissions"></a>RSC アクセス許可を登録する

会議拡張機能で Live Share SDK を有効にするには、まずアプリ マニフェストに次の RSC アクセス許可を追加する必要があります。

```json
{
  // ...rest of your manifest here
  "configurableTabs": [
    {
        "configurationUrl": "https://<<BASE_URI_ORIGIN>>/config",
        "canUpdateConfiguration": false,
        "scopes": [
            "groupchat"
        ],
        "context": [
            "meetingSidePanel",
            "meetingStage"
        ]
    }
  ],
  "validDomains": [
    "<<BASE_URI_ORIGIN>>"
  ],
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "LiveShareSession.ReadWrite.Chat",
          "type": "Delegated"
        },
        {
          "name": "LiveShareSession.ReadWrite.Group",
          "type": "Delegated"
        },
        {
          "name": "MeetingStage.Write.Chat",
          "type": "Delegated"
        },
        {
          "name": "ChannelMeetingStage.Write.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

## <a name="join-a-meeting-session"></a>会議セッションに参加する

ユーザーの会議に関連付けられたセッションに参加するには、次の手順に従います。

1. Teams クライアント SDK を初期化します。
2. [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) を初期化します。
3. 同期する必要のあるデータ構造を定義します。 たとえば、「 `SharedMap` 」のように入力します。
4. コンテナーに参加します。

例:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

---

たったこれだけで、コンテナーをセットアップし、会議のセッションに参加することができます。 ここで、Live Share SDK で使用できる _分散データ構造_ の種類を確認しましょう。

## <a name="fluid-distributed-data-structures"></a>流動分散データ構造

Live Share SDK は、流動フレームワークに含まれる[分散データ構造](https://fluidframework.com/docs/data-structures/overview/)をサポートします。 使用可能なさまざまな種類のオブジェクトの概要を次に示します。

| 共有オブジェクト                                                                       | 説明                                                                                                                             |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [SharedMap](https://fluidframework.com/docs/data-structures/map/)                   | 分散キー値ストア。 任意の JSON シリアル化可能なオブジェクトを指定されたキーに設定し、セッション内のすべてのユーザーにそのオブジェクトを同期させます。 |
| [SharedSegmentSequence](https://fluidframework.com/docs/data-structures/sequences/) | 設定された位置にある一連の項目 (セグメントと呼ばれる) の集合体を格納するリスト状のデータ構造。                                               |
| [SharedString](https://fluidframework.com/docs/data-structures/string/)             | ドキュメント テキスト編集用に最適化された分散文字列シーケンス。                                                                |

`SharedMap` のしくみを見てみましょう。 この例では、`SharedMap` を使用してプレイリスト機能を構築しています。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed, local) => {
  const video = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap, IValueChanged } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Declare interface for object being stored in map
interface IVideo {
  id: string;
  url: string;
}

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed: IValueChanged, local: boolean) => {
  const video: IVideo | undefined = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video: IVideo) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

---

> [!NOTE]
> コア流動フレームワーク DDS オブジェクトでは、会議の役割の検証はサポートされません。 これらのオブジェクト経由で保存されているデータを、会議の参加者全員が変更できます。

## <a name="live-share-ephemeral-data-structures"></a>Live Share 一時データ構造

Live Share SDK には、流動コンテナーに格納されていないステートフル オブジェクトとステートレス オブジェクトを提供する一連の一時的な新しい `SharedObject` クラスが含まれています。 たとえば、人気のある PowerPoint Live 統合など、アプリにレーザー ポインター機能を作成する場合は、Microsoft の `EphemeralEvent` または `EphemeralState` オブジェクトを使用できます。

| 一時オブジェクト                                                             | 説明                                                                                                                             |
| ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralPresence](/javascript/api/@microsoft/live-share/ephemeralpresence) | どのユーザーがオンラインであるかを確認し、各ユーザーにカスタム プロパティを設定し、そのプレゼンスへの変更をブロードキャストします。                               |
| [EphemeralEvent](/javascript/api/@microsoft/live-share/ephemeralevent)       | ペイロード内の任意のカスタム データ属性を持つ個々のイベントをブロードキャストします。                                                             |
| [EphemeralState](/javascript/api/@microsoft/live-share/ephemeralstate)       | SharedMap と同様に、分散キー値ストアを使用すると、発表者など、役割に基づいて状態の変更を制限できます。 |

### <a name="ephemeralpresence-example"></a>EphemeralPresence の例

この `EphemeralPresence` クラスを使用すると、セッションに参加しているユーザーの追跡がこれまで以上に簡単になります。 メソッドを`.initialize()``.updatePresence()`呼び出すときに、名前やプロファイル画像など、そのユーザーのカスタム メタデータを割り当てることができます。 イベントを `presenceChanged` リッスンすることで、各クライアントは最新 `EphemeralPresenceUser` のオブジェクトを受け取り、すべてのプレゼンス更新を一意 `userId`のレコードごとに 1 つのレコードに集約します。

> [!NOTE]
> それぞれに`EphemeralPresenceUser`割り当てられる既定値`userId`はランダム UUID であり、AAD ID に直接関連付けられません。 これをオーバーライドするには、次の例に示すように、主キーとしてカスタム `userId` を設定します。

例:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralPresence,
  PresenceState,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
  },
};
const { container } = await client.joinContainer(schema);
const presence = container.initialObjects.presence;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence, local) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName, profilePicture) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence, PresenceState, EphemeralPresenceUser } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomUserData {
  name: string;
  picture: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence<ICustomUserData>,
  },
};
const { container } = await client.joinContainer(schema);
const presence = container.initialObjects.presence as EphemeralPresence<ICustomUserData>;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence: EphemeralPresenceUser<ICustomUserData>, local: boolean) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName: string, profilePicture: string) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

---

### <a name="ephemeralevent-example"></a>EphemeralEvent の例

`EphemeralEvent` は、会議中に他のクライアントに簡単なイベントを送信するのに最適な方法です。 セッションの通知を送信する場合などのシナリオに便利です。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralEvent } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { notifications: EphemeralEvent },
};
const { container } = await client.joinContainer(schema);
const { notifications } = container.initialObjects;

// Register listener for incoming notifications
notifications.on("received", (event, local) => {
  let notificationToDisplay;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralEvent, IEphemeralEvent } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomEvent extends IEphemeralEvent {
  senderName: string;
  text: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    notifications: EphemeralEvent<ICustomEvent>,
  },
};
const { container } = await client.joinContainer(schema);
const notifications = container.initialObjects.notifications as EphemeralEvent<ICustomEvent>;

// Register listener for incoming notifications
notifications.on("received", (event: ICustomEvent, local: boolean) => {
  let notificationToDisplay: string;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

---

### <a name="ephemeraltimer-example"></a>EphemeralTimer の例

`EphemeralTimer` では、グループのメディテーション タイマーやゲームのラウンド タイマーなど、制限時間があるシナリオを有効にします。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralTimer } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
const { timer } = container.initialObjects;

// Register listener for when the timer starts its countdown
timer.on("started", (config, local) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on("played", (config, local) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on("paused", (config, local) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on("finished", (config) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on("onTick", (milliRemaining) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events for users in session
await timer.initialize();

// Start a 60 second timer
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  TeamsFluidClient,
  EphemeralTimer,
  EphemeralTimerEvents,
  ITimerConfig,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
const timer = container.initialObjects.timer as EphemeralTimer;

// Register listener for when the timer starts its countdown
timer.on(EphemeralTimerEvents.started, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on(EphemeralTimerEvents.played, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on(EphemeralTimerEvents.paused, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on(EphemeralTimerEvents.finished, (config: ITimerConfig) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on(EphemeralTimerEvents.onTick, (milliRemaining: number) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events
await timer.initialize();

// Start a 60 second timer for users in session
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

---

## <a name="role-verification-for-ephemeral-data-structures"></a>一時的なデータ構造に対する役割の検証

Teams 会議は、1 対 1 の通話から全員参加の会議まで、組織を超えたメンバーで行われる場合があります。 一時オブジェクトは、役割の検証をサポートするように設計されており、個々の一時オブジェクトごとにメッセージを送信できる役割を定義できます。 たとえば、ビデオの再生は会議の発表者と開催者のみが制御できるようにしても、ゲストと出席者が次に視聴するビデオを要求できるようにすることもできます。

> [!NOTE]
> このクラスでは `EphemeralPresence` 、ロールの検証はサポートされていません。 `EphemeralPresenceUser`オブジェクトには、特定の`getRoles`ユーザーの会議ロールを返すメソッドがあります。

次を使用する `EphemeralState`例:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralState,
  UserMeetingRole,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { appState: EphemeralState },
};
const { container } = await client.joinContainer(schema);
const { appState } = container.initialObjects;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state, data, local) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralState, UserMeetingRole } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomState {
  documentId: string;
  presentingUserId?: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    appState: EphemeralState<ICustomState>,
  },
};
const { container } = await client.joinContainer(schema);
const appState = container.initialObjects.appState as EphemeralState<ICustomState>;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state: string, data: ICustomState | undefined, local: boolean) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId: string) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId: string) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

---

アプリに役割の検証を実装する前に、特に **[開催者]** の役割のシナリオを理解するために顧客の声を耳を傾けます。 会議の開催者が会議に出席している保証はありません。 一般的な経験則として、組織内で共同作業を行う場合、すべてのユーザーが **[開催者]** または **[発表者]** になります。 ユーザーが **[出席者]** の場合、通常は会議の開催者に代わって意図的に決定されます。

## <a name="code-samples"></a>コード サンプル

| サンプルの名前 | 説明                                                     | JavaScript                                  |
| ----------- | --------------------------------------------------------------- | ------------------------------------------- |
| Dice Roller | 接続されているすべてのクライアントがサイコロをふり、結果を表示できるようにします。 | [表示](https://aka.ms/liveshare-diceroller) |
| アジャイル ポーカー | 接続されているすべてのクライアントが Agile Poker をプレイできるようにします。               | [表示](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Live Share メディア機能](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>関連項目

* [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
* [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
* [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
* [Live Share FAQ](teams-live-share-faq.md)
* [会議の Teams アプリ](teams-apps-in-meetings.md)
