---
title: Live Share コード チュートリアル
author: surbhigupta
description: このモジュールでは、Live Share SDK の使用を開始する方法と、Live Share SDK を使用して Dice Roller サンプルをビルドする方法について説明します
ms.topic: conceptual
ms.localizationpriority: high
ms.author: stevenic
ms.date: 04/07/2022
ms.openlocfilehash: 66ff0cfed7fcd34d741a35ff4aa30e507adf8717
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560541"
---
# <a name="dice-roller-code-tutorial"></a>Dice Roller コードのチュートリアル

Dice Roller サンプル アプリでは、ユーザーにロールボタンが付いたサイコロが表示されます。 サイコロがロールされると、Live Share SDK は Fluid Framework を使用してクライアント間でデータを同期するため、すべてのユーザーに同じ結果が表示されます。 データを同期するには、 [app.js](https://github.com/microsoft/live-share-sdk/blob/main/samples/01.dice-roller/src/app.js) ファイルで次の手順を実行します。

1. [アプリケーションを設定する](#set-up-the-application)
2. [Fluid コンテナーを結合する](#join-a-fluid-container)
3. [ステージ ビューを記述する](#write-the-stage-view)
4. [ステージ ビューを Fluid データに接続する](#connect-stage-view-to-fluid-data)
5. [サイド パネル ビューを記述する](#write-the-side-panel-view)
6. [設定ビューを記述する](#write-the-settings-view)

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="DiceRoller サンプル":::

## <a name="set-up-the-application"></a>アプリケーションを設定します。

まず、必要なモジュールをインポートします。 このサンプルでは、Fluid Framework の [SharedMap DDS](https://fluidframework.com/docs/data-structures/map/) と Live Share SDK [の TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) を使用します。 このサンプルでは Teams 会議機能拡張がサポートされているため、 [Teams クライアント SDK](https://github.com/OfficeDev/microsoft-teams-library-js) を含める必要があります。 最後に、サンプルはローカルと Teams の両方の会議で実行するように設計されているため、 [サンプルをローカルでテスト](https://fluidframework.com/docs/testing/testing/#azure-fluid-relay-as-an-abstraction-for-tinylicious)するために、より多くの Fluid Framework の部分を含める必要があります。

アプリケーションは、コンテナーで使用できる一連の _初期オブジェクト_ を定義するスキーマを使用して、Fluid コンテナーを作成します。 このサンプルでは、SharedMap を使用して、ロールされた現在のサイコロ値を格納します。 詳細については、「[データ プライバシー](https://fluidframework.com/docs/build/data-modeling/)」を参照してください。

Teams 会議アプリには、コンテンツ、構成、ステージなどの複数のビューが必要です。 ビューを `start()` 識別するのに役立つ関数を作成できます。 これは、必要な初期化をレンダリングして実行するのに役立ちます。 アプリでは、Web ブラウザーと Teams 会議内の両方でローカルで実行できます。 この関数は `start()` 、クエリ パラメーターを `inTeams=true` 検索して、Teams で実行されているかどうかを判断します。

> [!NOTE]
> Teams で実行する場合は、他の teams-js メソッドを呼び出す `app.initialize()` 前にアプリケーションを呼び出す必要があります。

クエリ パラメーターに `inTeams=true` 加えて、クエリ パラメーターを `view=content|config|stage` 使用して、レンダリングする必要があるビューを決定できます。

```js
import { SharedMap } from "fluid-framework";
import { app, pages } from "@microsoft/teams-js";
import { LiveShareClient, testLiveShare } from "@microsoft/live-share";
import { InsecureTokenProvider } from "@fluidframework/test-client-utils";

const searchParams = new URL(window.location).searchParams;
const root = document.getElementById("content");

// Define container schema

const diceValueKey = "dice-value-key";

const containerSchema = {
  initialObjects: { diceMap: SharedMap },
};

function onContainerFirstCreated(container) {
  // Set initial state of the rolled dice to 1.
  container.initialObjects.diceMap.set(diceValueKey, 1);
}

// STARTUP LOGIC

async function start() {
  // Check for page to display
  let view = searchParams.get("view") || "stage";

  // Check if we are running on stage.
  if (!!searchParams.get("inTeams")) {
    // Initialize teams app
    await app.initialize();

    // Get our frameContext from context of our app in Teams
    const context = await app.getContext();
    if (context.page.frameContext == "meetingStage") {
      view = "stage";
    }
  }

  // Load the requested view
  switch (view) {
    case "content":
      renderSidePanel(root);
      break;
    case "config":
      renderSettings(root);
      break;
    case "stage":
    default:
      const { container } = await joinContainer();
      renderStage(container.initialObjects.diceMap, root);
      break;
  }
}

start().catch((error) => console.error(error));
```

## <a name="join-a-fluid-container"></a>Fluid コンテナーを結合する

アプリのすべてのビューが共同作業である必要はありません。 `stage`ビューには _常に_ コラボレーション機能が必要です。ビューには`content`コラボレーション機能 _が必要な場合があります_。また、`config` ビューにはコラボレーション機能は必要 _ありません_。 共同作業機能が必要なビューの場合は、現在の会議に関連付けられている Fluid コンテナーに参加する必要があります。

会議のコンテナーに参加するのは、 [LiveShareClient](/javascript/api/@microsoft/live-share/liveshareclient) を初期化し、 [joinContainer()](/javascript/api/@microsoft/live-share/liveshareclient#@microsoft-live-share-liveshareclient-joincontainer) メソッドを呼び出すのと同じくらい簡単です。

ローカルで実行している場合は、 [testLiveShare](/javascript/api/@microsoft/live-share/testliveshare) をインポートし、その [initialize()](/javascript/api/@microsoft/live-share.testliveshare#@microsoft-live-share-testliveshare-initialize) メソッドを呼び出すことができます。 次に、 [joinContainer()](/javascript/api/@microsoft/live-share.testliveshare#@microsoft-live-share-testliveshare-joincontainer) メソッドを使用してセッションに接続します。

```js
async function joinContainer() {
  // Are we running in teams?
  if (!!searchParams.get("inTeams")) {
    // Create client
    const liveShare = new LiveShareClient();
    // Join container
    return await liveShare.joinContainer(containerSchema, onContainerFirstCreated);
  }
  // Create client and configure for testing
  testLiveShare.initialize();
  return await testLiveShare.joinContainer(containerSchema, onContainerFirstCreated);
}
```

ローカルでテストする場合は、 `testLiveShare` 作成されたテスト コンテナーの ID を含むブラウザー URL を更新します。 そのリンクを他のブラウザー タブにコピーすると、 `testLiveShare` 作成されたテスト コンテナーに参加します。 アプリケーション URL の変更がアプリケーションの操作に干渉する場合、テスト コンテナー ID の格納に使用される戦略は、[setLocalTestContainerId オプションと getLocalTestContainerId](/javascript/api/@microsoft/live-share.iliveshareclientoptions#@microsoft-live-share-iliveshareclientoptions-setlocaltestcontainerid) オプションを[](/javascript/api/@microsoft/live-share.iliveshareclientoptions#@microsoft-live-share-iliveshareclientoptions-getlocaltestcontainerid)`LiveShareClient`使用してカスタマイズできます。

## <a name="write-the-stage-view"></a>ステージ ビューを記述する

多くの Teams 会議機能拡張アプリケーションは、ビュー フレームワークに React を使用するように設計されていますが、これは必要ありません。 たとえば、このサンプルでは、標準の HTML/DOM メソッドを使用してビューをレンダリングします。

### <a name="start-with-a-static-view"></a>静的ビューから開始する

Fluid 機能を使用せずにローカル データを使用してビューを簡単に作成し、アプリの重要な部分を変更して Fluid を追加できます。

この関数は `renderStage` 、 `stageTemplate` 渡された HTML 要素に追加され、 **ロール** ボタンが選択されるたびにランダムなサイコロ値を持つ作業用サイコロ ローラーを作成します。 `diceMap` は、次のいくつかの手順で使用されます。

```js
const stageTemplate = document.createElement("template");

stageTemplate["innerHTML"] = `
  <div class="wrapper">
    <div class="dice"></div>
    <button class="roll"> Roll </button>
  </div>
`;
function renderStage(diceMap, elem) {
  elem.appendChild(stageTemplate.content.cloneNode(true));
  const rollButton = elem.querySelector(".roll");
  const dice = elem.querySelector(".dice");

  rollButton.onclick = () => updateDice(Math.floor(Math.random() * 6) + 1);

  const updateDice = (value) => {
    // Unicode 0x2680-0x2685 are the sides of a die (⚀⚁⚂⚃⚄⚅).
    dice.textContent = String.fromCodePoint(0x267f + value);
  };
  updateDice(1);
}
```

## <a name="connect-stage-view-to-fluid-data"></a>ステージ ビューを Fluid データに接続する

### <a name="modify-fluid-data"></a>Fluid データを変更する

アプリケーションで Fluid の使用を開始するために最初に変更することは、ユーザーが `rollButton` を選択したときに何が起こるかです。 ローカル状態を直接更新する代わりに、ボタンは、渡された `diceMap` の `value` キーに格納されている番号を更新します。 `diceMap` はFluid `SharedMap` であるため、変更はすべてのクライアントに分散されます。 イベントに変更を `diceMap` 加えた場合、 `valueChanged` イベントが生成され、イベント ハンドラーによってビューの更新がトリガーされる可能性があります。

このパターンは、ビューがローカル変更とリモート変更の両方で同じ動作を可能にするため、Fluid では一般的です。

```js
rollButton.onclick = () =>
  diceMap.set("dice-value-key", Math.floor(Math.random() * 6) + 1);
```

### <a name="rely-on-fluid-data"></a>Fluid データに依存する

次に行う必要がある変更は、任意の値を `updateDice` 受け入れなくなったため、関数を変更することです。 つまり、アプリはローカルのサイコロ値を直接変更できなくなりました。 代わりに、値は呼び出される`SharedMap`たびに`updateDice`取得されます。

```js
const updateDice = () => {
  const diceValue = diceMap.get("dice-value-key");
  dice.textContent = String.fromCodePoint(0x267f + diceValue);
};
updateDice();
```

### <a name="handle-remote-changes"></a>リモート変更を処理する

`diceMap` から返される値は、特定の時点のスナップショットに過ぎません。 データの変更時にデータを最新の状態に保つには、`valueChanged` イベントが送信されるたびに `updateDice` を呼び出すように `diceMap` にイベント ハンドラーを設定する必要があります。 発生したイベントの一覧とそれらのイベントに渡される値を取得するには、 [SharedMap](https://fluidframework.com/docs/data-structures/map/) に関するサイトを参照してください。

```js
diceMap.on("valueChanged", updateDice);
```

## <a name="write-the-side-panel-view"></a>サイド パネル ビューを記述する

タブ `contentUrl` から `sidePanel` フレーム コンテキストで読み込まれたサイド パネルビューは、ユーザーが会議内でアプリを開いたときにサイド パネルに表示されます。 サイド パネル ビューの目的は、アプリを会議ステージに共有する前に、ユーザーがアプリのコンテンツを選択できるようにすることです。 Live Share SDK アプリの場合は、サイド パネル ビューをアプリのコンパニオン エクスペリエンスとして使用することもできます。 サイド パネル ビューから [joinContainer()](/javascript/api/@microsoft/live-share/liveshareclient#@microsoft-live-share-liveshareclient-joincontainer) を呼び出すと、ステージ ビューが接続されているのと同じ Fluid コンテナーに接続されます。 このコンテナーは、ステージ ビューとの通信に使用できます。 全員のステージ ビュー _および_ サイドパネル ビューと通信していることを確認してください。

サンプルのサイド パネル ビューでは、ユーザーに [ステージへの共有] ボタンの選択を求めるメッセージが表示されます。

```js
const sidePanelTemplate = document.createElement("template");

sidePanelTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Lets get started</p>
    <p class="text">Press the share to stage button to share Dice Roller to the meeting stage.</p>
  </div>
`;

function renderSidePanel(elem) {
  elem.appendChild(sidePanelTemplate.content.cloneNode(true));
}
```

## <a name="write-the-settings-view"></a>設定ビューを記述する

アプリ マニフェストに読み込まれた `configurationUrl` 設定ビューは、最初に Teams 会議にアプリを追加したときにユーザーに表示されます。 このビューにより、開発者は、ユーザー入力に基づいて会議に固定されるタブの `contentUrl` を構成できます。 `contentUrl` を設定するためにユーザー入力が必要ない場合でも、このページは現在必要です。

> [!NOTE]
> Live Share の [joinContainer()](/javascript/api/@microsoft/live-share/liveshareclient#@microsoft-live-share-liveshareclient-joincontainer) は、タブ `settings` コンテキストではサポートされていません。

サンプルの設定ビューでは、保存ボタンを選択するようにユーザーに求められます。

```js
const settingsTemplate = document.createElement("template");

settingsTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Welcome to Dice Roller!</p>
    <p class="text">Press the save button to continue.</p>
  </div>
`;

function renderSettings(elem) {
  elem.appendChild(settingsTemplate.content.cloneNode(true));

  // Save the configurable tab
  pages.config.registerOnSaveHandler((saveEvent) => {
    pages.config.setConfig({
      websiteUrl: window.location.origin,
      contentUrl: window.location.origin + "?inTeams=1&view=content",
      entityId: "DiceRollerFluidLiveShare",
      suggestedDisplayName: "DiceRollerFluidLiveShare",
    });
    saveEvent.notifySuccess();
  });

  // Enable the Save button in config dialog
  pages.config.setValidityState(true);
}
```

## <a name="test-locally"></a>ローカルでテストする

`npm run start` を使用して、アプリをローカルでテストできます。 詳細については、「[クイック スタート ガイド](./teams-live-share-quick-start.md)」を参照してください。

## <a name="test-in-teams"></a>Teamsでのテスト

`npm run start` を使用してローカルでアプリの実行を開始したら、Teams でアプリをテストできます。 デプロイせずにアプリをテストする場合は、[`ngrok`](https://ngrok.com/) トンネリング サービスを ダウンロードして使用します。

### <a name="create-a-ngrok-tunnel-to-allow-teams-to-reach-your-app"></a>Teams がアプリに到達できるように、ngrok トンネルを作成する

1. [ngrok をダウンロードします](https://ngrok.com/download)。

1. ngrok を使用して、ポート 8080 を使用してトンネルを作成します。 次のコマンドを実行します。

   ```bash
    ngrok http 8080 --host-header=localhost
   ```

   新しい ngrok ターミナルが新しいURL (たとえば `https:...ngrok.io`)で開きます。 新しい URL は、アプリを指すトンネルであり、アプリで `manifest.json` 更新する必要があります。

### <a name="create-the-app-package-to-sideload-into-teams"></a>Teams にサイドロードするアプリ パッケージを作成する

1. コンピューターの Dice Roller サンプル フォルダー `\live-share-sdk\samples\01.dice-roller` に移動します。 GitHub のダイスローラー サンプルから [`.\manifest\manifest.json`](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller/manifest) を確認することもできます。

1. manifest.json を開き、構成 URL を更新します。

   `https://<<BASE_URI_DOMAIN>>` を ngrok の http エンドポイントに置き換えます 。

1. 次のシナリオでは、これらのプロパティを更新できます。

   - `developer.name` を自分の名前に設定します。
   - `developer.websiteUrl` を Web サイトで更新します。
   - `developer.privacyUrl` をプライバシー ポリシーを使用して更新します。
   - `developer.termsOfUseUrl` の使用条件を更新します。

1. `manifest.zip` を作成するマニフェスト フォルダーの内容を zip 化します。 `manifest.zip` に `manifest.json` ソース ファイル、`color` アイコン、および `outline` アイコンのみが含まれていることを確認します。

   1. Windowsで、`.\manifest` ディレクトリ内のすべてのファイルを選択し、圧縮します。

   > [!NOTE]
   >
   > - 含まれているフォルダーを zip にしないでください。
   > - zip ファイルにわかりやすい名前を付けます。 たとえば、「 `DiceRollerLiveShare` 」のように入力します。

   マニフェストの詳細については、「[Teams マニフェストのドキュメント](../resources/schema/manifest-schema.md)」を参照してください

### <a name="sideload-your-app-into-a-meeting"></a>アプリを会議にサイドロードする

1. Teams を開きます。

1. Teams の予定表から会議をスケジュールします。 会議に少なくとも 1 人の出席者を招待していることを確認します。

1. 会議に参加します。

1. 上部の会議ウィンドウで、[**+ アプリ** > **アプリの管理**] を選択します。

1. [**アプリの管理**] ウィンドウで、**カスタム アプリアップロード** を選択します。

   1. **カスタム アプリをアップロード** するオプションが表示されない場合は、[手順](/microsoftteams/teams-custom-app-policies-and-settings)に従ってテナントでカスタム アプリを有効にします。

1. ボタンを選択し、コンピューターから `manifest.zip` ファイルを選択します。

1. [**追加**] を選択して、サンプル アプリを会議に追加します。

1. **[+ アプリ]** を選択し、**[アプリの検索]**  検索ボックスに「Dice Roller」と入力します。

1. 会議でアクティブ化するアプリを選択します。

1. **[保存]** を選択します。

   Dice Roller アプリは、Teams 会議パネルに追加されます。

1. サイド パネルで、ステージへの共有アイコンを選択します。 Teams 会議の会議ステージでユーザーとのライブ同期を開始します。

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-to-stage.png" alt-text="ステージ アイコンに共有する":::

   これで、会議ステージにダイス ローラーが表示されます。

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-meeting-stage.png" alt-text="会議ステージの画像":::

会議に招待されたユーザーは、会議に参加するときに、ステージ上でアプリを表示できます。

## <a name="deployment"></a>展開

コードをデプロイする準備ができたら、[Teams Toolkit](../toolkit/provision.md#provision-using-teams-toolkit-in-visual-studio-code) または [[Teams 開発者ポータル]](https://dev.teams.microsoft.com/apps) を使用して、アプリの zip ファイルをプロビジョニングしてアップロードできます。

> [!NOTE]
> アプリをアップロードまたは配布する前に、プロビジョニングされた appId を `manifest.json` に追加する必要があります。

## <a name="code-samples"></a>コード サンプル

| サンプルの名前 | 説明                                                     | JavaScript                                                                           |
| :---------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Dice Roller | 接続されているすべてのクライアントがサイコロをふり、結果を表示できるようにします。 | [表示](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [コア機能](teams-live-share-capabilities.md)

## <a name="see-also"></a>関連項目

- [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
- [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
- [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
- [Live Share FAQ](teams-live-share-faq.md)
- [会議の Teams アプリ](teams-apps-in-meetings.md)
