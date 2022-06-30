---
title: Live Share コード チュートリアル
description: このモジュールでは、Live Share SDK の使用を開始する方法と、Live Share SDK を使用して Dice Roller サンプルをビルドする方法について説明します
ms.topic: concept
ms.localizationpriority: high
ms.author: stevenic
ms.openlocfilehash: 8af4a452820a01c0a535106e9273d953cb5f0713
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484629"
---
---

# <a name="dice-roller-code-tutorial"></a>Dice Roller コードのチュートリアル

Dice Roller サンプル アプリでは、ユーザーにロールボタンが付いたサイコロが表示されます。 サイコロがロールされると、Live Share SDK は流動フレームワークを使用してクライアント間でデータを同期するため、すべてのユーザーに同じ結果が表示されます。 データを同期するには、 [app.js](https://github.com/microsoft/live-share-sdk/blob/main/samples/01.dice-roller/src/app.js) ファイルで次の手順を実行します。

1. [アプリケーションを設定する](#set-up-the-application)
2. [Fluid コンテナーを結合する](#join-a-fluid-container)
3. [ステージ ビューを記述する](#write-the-stage-view)
4. [ステージ ビューを Fluid データに接続する](#connect-stage-view-to-fluid-data)
5. [サイド パネル ビューを記述する](#write-the-side-panel-view)
6. [設定ビューを記述する](#write-the-settings-view)

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="DiceRoller サンプル":::

## <a name="set-up-the-application"></a>アプリケーションを設定します。

まず、必要なモジュールをインポートします。 このサンプルでは、流動フレームワークの [SharedMap DDS](https://fluidframework.com/docs/data-structures/map/) と、Live Share SDK の [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) を使用します。 このサンプルでは、Teams会議の機能拡張がサポートされているため、[[Teams クライアント SDK]](https://github.com/OfficeDev/microsoft-teams-library-js) を含める必要があります。 最後に、サンプルはローカルとTeams会議の両方で実行するように設計されているため、[サンプルをローカルでテスト](https://fluidframework.com/docs/testing/testing/#azure-fluid-relay-as-an-abstraction-for-tinylicious)するために必要な追加の流動フレームワーク部分を含める必要があります。
  
アプリケーションは、コンテナーで使用できる一連の *初期オブジェクト* を定義するスキーマを使用して、Fluid コンテナーを作成します。 このサンプルでは、SharedMap を使用して、ロールされた最新のダイ値を格納します。 詳細については、「[データ プライバシー](https://fluidframework.com/docs/build/data-modeling/)」を参照してください。

Teams 会議アプリ、複数のビュー (コンテンツ、構成、ステージ) が必要です。 レンダリングするビューを識別し、必要な初期化を実行するのに役立つ `start()` 関数を作成します。 アプリで Web ブラウザーと Teams 会議内の両方の実行をサポートし、`start()` 関数が `inTeams=true` クエリ パラメーターを検索して、Teamsで実行されているかどうかを判断できるようにします。 Teams で実行する場合は、他の teams-js メソッドを呼び出す`app.initialize()`前にアプリケーションを呼び出す必要があります。

クエリ パラメーターに `inTeams=true` 加えて、クエリ パラメーターを `view=content|config|stage` 使用して、レンダリングする必要があるビューを決定できます。

```js
import { SharedMap } from "fluid-framework";
import { TeamsFluidClient } from "@microsoft/live-share";
import { app, pages } from "@microsoft/teams-js";
import { LOCAL_MODE_TENANT_ID } from "@fluidframework/azure-client";
import { InsecureTokenProvider } from "@fluidframework/test-client-utils";

const searchParams = new URL(window.location).searchParams;
const root = document.getElementById("content");

// Define container schema

const diceValueKey = "dice-value-key";

const containerSchema = {
  initialObjects: { diceMap: SharedMap }
};

function onContainerFirstCreated(container) {
  // Set initial state of the rolled dice to 1.
  container.initialObjects.diceMap.set(diceValueKey, 1);
}


// STARTUP LOGIC

async function start() {

  // Check for page to display
  let view = searchParams.get('view') || 'stage';

  // Check if we are running on stage.
  if (!!searchParams.get('inTeams')) {

    // Initialize teams app
    await app.initialize();

    // Get our frameContext from context of our app in Teams
    const context = await app.getContext();
    if (context.page.frameContext == 'meetingStage') {
      view = 'stage';
    }
  }

  // Load the requested view
  switch (view) {
    case 'content':
      renderSidePanel(root);
      break;
    case 'config':
      renderSettings(root);
      break;
    case 'stage':
    default:
      const { container } = await joinContainer();
      renderStage(container.initialObjects.diceMap, root);
      break;
  }
}

start().catch((error) => console.error(error));
```

## <a name="join-a-fluid-container"></a>Fluid コンテナーを結合する

すべてのアプリ ビューが共同作業である必要があるわけではありません。 `stage`ビューには *常に* コラボレーション機能が必要です。ビューには`content`コラボレーション機能 *が必要な場合があります*。また、`config` ビューにはコラボレーション機能は必要 *ありません*。 共同作業機能が必要なビューの場合は、現在の会議に関連付けられている Fluid コンテナーに参加する必要があります。

会議のコンテナーに参加するのは、新しい [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) を作成し、それを [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) メソッドと呼ぶのと同じくらい簡単です。  ローカルで実行する場合は、特別な `LOCAL_MODE_TENANT_ID` カスタム接続構成を渡す必要がありますが、それ以外の場合は、ローカル コンテナーの結合は、Teams でコンテナーを参加させるのと同じです。

```js
async function joinContainer() {
  // Are we running in teams?
  let client;
  if (!!searchParams.get('inTeams')) {
      // Create client
      client = new TeamsFluidClient();
  } else {
      // Create client and configure for testing
      client = new TeamsFluidClient({
        connection: {
          tenantId: LOCAL_MODE_TENANT_ID,
          tokenProvider: new InsecureTokenProvider("", { id: "123", name: "Test User" }),
          orderer: "http://localhost:7070",
          storage: "http://localhost:7070",
        }
      });
  }

  // Join container
  return await client.joinContainer(containerSchema, onContainerFirstCreated);
}
```

> [!NOTE]
> ローカルでテストすると、TeamsFluidClient によってブラウザー URL が更新され、作成されたテスト コンテナーの ID が含まれます。 そのリンクを他のブラウザー タブにコピーすると、TeamsFluidClient が作成されたテスト コンテナーに参加します。 アプリケーション URL の変更がアプリケーションの操作を妨げる場合、テスト コンテナー ID の格納に使用される戦略は、TeamsFluidClient に渡される [setLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-setlocaltestcontainerid) オプションと [getLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-getlocaltestcontainerid) オプションを使用してカスタマイズできます。

## <a name="write-the-stage-view"></a>ステージ ビューを記述する

多くの Teams 会議機能拡張アプリケーションは、ビュー フレームワークに React を使用するように設計されていますが、これは必要ありません。 たとえば、このサンプルでは、標準の HTML/DOM メソッドを使用してビューをレンダリングします。

### <a name="start-with-a-static-view"></a>静的ビューから開始する

Fluid 機能を使用せずにローカル データを使用してビューを簡単に作成し、アプリの重要な部分を変更して Fluid を追加できます。

この `renderStage` 関数は、渡された HTML 要素に `stageTemplate` を追加し、 **ロール** ボタンが選択されるたびにランダムなサイコロ値を持つ作業用サイコロ ローラーを作成します。 `diceMap` は、次のいくつかの手順で使用されます。

```js
const stageTemplate = document.createElement("template");

stageTemplate["innerHTML"] = `
  <div class="wrapper">
    <div class="dice"></div>
    <button class="roll"> Roll </button>
  </div>
`
function renderStage(diceMap, elem) {
    elem.appendChild(stageTemplate.content.cloneNode(true));
    const rollButton = elem.querySelector(".roll");
    const dice = elem.querySelector(".dice");

    rollButton.onclick = () => updateDice(Math.floor(Math.random() * 6)+1);

    const updateDice = (value) => {
        // Unicode 0x2680-0x2685 are the sides of a die (⚀⚁⚂⚃⚄⚅).
        dice.textContent = String.fromCodePoint(0x267f + value);
    };
    updateDice(1);
}
```

## <a name="connect-stage-view-to-fluid-data"></a>ステージ ビューを Fluid データに接続する

### <a name="modify-fluid-data"></a>Fluid データを変更する

アプリケーションで Fluid の使用を開始するために最初に変更することは、ユーザーが `rollButton` を選択したときに何が起こるかです。 ローカル状態を直接更新する代わりに、ボタンは、渡された `diceMap` の `value` キーに格納されている番号を更新します。 `diceMap` はFluid `SharedMap` であるため、変更はすべてのクライアントに分散されます。 `diceMap` を変更すると、`valueChanged` イベントが発行され、イベント ハンドラーがビューの更新をトリガーできます。

このパターンは、ビューがローカル変更とリモート変更の両方で同じ動作を可能にするため、Fluid では一般的です。

```js
    rollButton.onclick = () => diceMap.set("dice-value-key", Math.floor(Math.random() * 6)+1);
```

### <a name="rely-on-fluid-data"></a>Fluid データに依存する

次に行う必要のある変更は、`updateDice` 関数を変更して、任意の値を受け入れないようにすることです。 つまり、アプリはローカルのサイコロ値を直接変更できなくなりました。 代わりに、値は呼び出される`SharedMap`たびに`updateDice`取得されます。

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

タブ `contentUrl` から `sidePanel` フレーム コンテキストで読み込まれたサイド パネルビューは、ユーザーが会議内でアプリを開いたときにサイド パネルに表示されます。 このビューの目的は、会議ステージにアプリを共有する前に、ユーザーがアプリのコンテンツを選択できるようにすることです。 Live Share SDK アプリの場合は、サイド パネル ビューをアプリのコンパニオン エクスペリエンスとして使用することもできます。 サイド パネル ビューから [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) を呼び出すと、ステージ ビューが接続されているのと同じ Fluid コンテナーに接続されます。 このコンテナーは、ステージ ビューとの通信に使用できます。 全員のステージ ビュー *および* サイドパネル ビューと通信していることを確認してください。

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

アプリマニフェストの `configurationUrl` を介して読み込まれた設定ビューは、ユーザーが最初に Teams 会議にアプリを追加したときに表示されます。 このビューにより、開発者は、ユーザー入力に基づいて会議に固定されるタブの `contentUrl` を構成できます。 `contentUrl` を設定するためにユーザー入力が必要ない場合でも、このページは現在必要です。

> [!Important]
> Live Share SDK の [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) は、タブ `settings` コンテキストではサポートされていません。

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
    pages.config.registerOnSaveHandler(saveEvent => {
      pages.config.setConfig({
        websiteUrl: window.location.origin,
        contentUrl: window.location.origin + '?inTeams=1&view=content',
        entityId: 'DiceRollerFluidLiveShare',
        suggestedDisplayName: 'DiceRollerFluidLiveShare'
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

    ```
     `ngrok http 8080 --host-header=localhost`
    ```

    新しい ngrok ターミナルが新しいURL (たとえば `https:...ngrok.io`)で開きます。 新しい URL は、アプリを指すトンネルであり、アプリで `manifest.json` 更新する必要があります。

### <a name="create-the-app-package-to-sideload-into-teams"></a>Teams にサイドロードするアプリ パッケージを作成する

1. コンピューターの Dice Roller サンプル フォルダー `\live-share-sdk\samples\01.dice-roller` に移動します。 GitHub のダイスローラー サンプルから [`.\manifest\manifest.json`](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller/manifest) を確認することもできます。

1. manifest.json を開き、構成 URL を更新します。

   `https://<<BASE_URI_DOMAIN>>` を ngrok の http エンドポイントに置き換えます 。

1. 次のシナリオでは、これらのプロパティを更新できます。
   * `developer.name` を自分の名前に設定します。
   * `developer.websiteUrl` を Web サイトで更新します。
   * `developer.privacyUrl` をプライバシー ポリシーを使用して更新します。
   * `developer.termsOfUseUrl` の使用条件を更新します。

1. `manifest.zip` を作成するマニフェスト フォルダーの内容を zip 化します。 `manifest.zip` に `manifest.json` ソース ファイル、`color` アイコン、および `outline` アイコンのみが含まれていることを確認します。

   1. Windowsで、`.\manifest` ディレクトリ内のすべてのファイルを選択し、圧縮します。
  
   > [!NOTE]
   >
   > * 含まれているフォルダーを zip にしないでください。
   > * zip ファイルにわかりやすい名前を付けます。 たとえば、「 `DiceRollerLiveShare` 」のように入力します。
  
   マニフェストの詳細については、「[Teams マニフェストのドキュメント](../resources/schema/manifest-schema.md)」を参照してください

### <a name="sideload-your-app-into-a-meeting"></a>アプリを会議にサイドロードする

1. Teams を開きます。

1. Teams の予定表から会議をスケジュールします。 少なくとも 1 人の出席者を会議に招待していることを確認します。

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

コードをデプロイする準備ができたら、[Teams Toolkit](../toolkit/provision.md#provision-using-teams-toolkit) または [[Teams 開発者ポータル]](https://dev.teams.microsoft.com/apps) を使用して、アプリの zip ファイルをプロビジョニングしてアップロードできます。

> [!NOTE]
> アプリをアップロードまたは配布する前に、プロビジョニングされた appId を `manifest.json` に追加する必要があります。

## <a name="code-samples"></a>コード サンプル

| サンプルの名前 | 説明                                                      | JavaScript                                                                           |
| :---------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Dice Roller | 接続されているすべてのクライアントがサイコロをふり、結果を表示できるようにします。 | [表示](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [コア機能](teams-live-share-capabilities.md)

## <a name="see-also"></a>関連項目

* [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
* [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
* [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
* [Live Share FAQ](teams-live-share-faq.md)
* [会議の Teams アプリ](teams-apps-in-meetings.md)
