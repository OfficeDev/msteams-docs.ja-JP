---
title: Live Share キャンバスの概要
author: surbhigupta
description: このモジュールでは、Live Share キャンバスの詳細について説明します。この拡張機能を使用して、会議アプリのインク、レーザー ポインター、カーソルを有効にします。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 10/04/2022
ms.openlocfilehash: 9d1a776432f728c1e56caa357089be6e47c17e4c
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560611"
---
# <a name="live-share-canvas-overview"></a>Live Share キャンバスの概要

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-docs-feature-1.png" alt-text="スクリーンショットは、Teams 会議の他の会議参加者と同期したキャンバスの例を示しています。":::

世界中の会議室や教室では、ホワイトボードはコラボレーションの重要な部分です。 しかし、現代では、ホワイトボードは十分ではありません。 PowerPoint などの多数のデジタル ツールが現代のコラボレーションの中心であり、同じクリエイティブな可能性を実現することが不可欠です。

よりシームレスなコラボレーションを実現するために、Microsoft はPowerPoint Liveを作成しました。これは、Teams でのユーザーの作業に役立つものになりました。 発表者は、ペン、蛍光ペン、レーザー ポインターを使用して、すべてのユーザーが見ることができるスライドに注釈を付けて、重要な概念に注意を引くことができます。 Live Share キャンバスを使用すると、アプリは最小限の労力でPowerPoint Liveインク ツールの機能を利用できます。

## <a name="install"></a>インストール

npm を使用して SDK の最新バージョンをアプリケーションに追加するには:

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-canvas@next --save
```

または

[Yarn](https://yarnpkg.com/) を使用して SDK の最新バージョンをアプリケーションに追加するには:

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-canvas@next
```

## <a name="setting-up-the-package"></a>パッケージを設定する

Live Share キャンバスには、ターンキー コラボレーションを可能にする 2 つのプライマリ クラスがあります。`InkingManager`.`LiveCanvas` `InkingManager` は、完全に機能 `<canvas>` する要素をアプリにアタッチする一方 `LiveCanvas` で、他の会議参加者とのリモート同期を管理する役割を担います。 一緒に使用すると、アプリは数行のコードでホワイトボードに似た完全な機能を持つことができます。

| クラス                                                                     | 説明                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [InkingManager](/javascript/api/@microsoft/live-share-canvas/inkingmanager) | ペンまたは蛍光ペンのストローク、 `<canvas>` レーザー ポインター、線と矢印、消しゴムを自動的に管理するために要素を特定 `<div>` の要素にアタッチするクラス。 API のセット (アクティブなツールを制御する) と基本的な構成設定を公開します。 |
| [LiveCanvas](/javascript/api/@microsoft/live-share-canvas/livecanvas)      | `SharedObject` Live Share セッションのすべてのユーザーのストロークとカーソル位置`InkingManager`を同期するクラス。                                                                                                                   |

例:

```html
<body>
  <div id="canvas-host"></div>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const { liveCanvas } = container.initialObjects;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";
import { ContainerSchema } from "fluid-framework";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const liveCanvas = container.initialObjects.liveCanvas as LiveCanvas;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

---

## <a name="canvas-tools-and-cursors"></a>キャンバス ツールとカーソル

Live Share キャンバスのセットアップと同期が完了したので、ペン ツールを選択するボタンなど、ユーザーが操作できるようにキャンバスを構成できます。 このセクションでは、使用可能なツールとその使用方法について説明します。

### <a name="inking-tools"></a>インクツール

Live Share キャンバスの各インク ツールは、ユーザーが描画する際にストロークをレンダリングします。 タッチ スクリーンまたはスタイラスを使用する場合、ツールは圧力力学もサポートし、ストロークの幅に影響します。 構成設定には、ブラシの色、太さ、図形、およびオプションの終了矢印が含まれます。

#### <a name="pen-tool"></a>ペンツール

:::image type="content" source="../assets/images/teams-live-share/canvas-pen-tool.gif" alt-text="GIF は、ペン ツールを使用してキャンバスにストロークを描画する例を示しています。":::

ペン ツールは、キャンバスに格納されているソリッド ストロークを描画します。 既定のチップ図形は円です。

```html
<div>
  <button id="pen">Enable Pen</button>
  <label for="pen-color">Select a color:</label>
  <input type="color" id="color" name="color" value="#000000" />
  <button id="pen-tip-size">Increase pen size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to pen
document.getElementById("pen").onclick = () => {
  inkingManager.tool = InkingTool.pen;
};
// Change the selected color for pen
document.getElementById("pen-color").onchange = () => {
  const colorPicker = document.getElementById("color");
  inkingManager.penBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for pen
document.getElementById("pen-tip-size").onclick = () => {
  inkingManager.penBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="highlighter-tool"></a>蛍光ペン ツール

:::image type="content" source="../assets/images/teams-live-share/canvas-highlighter-tool.gif" alt-text="GIF は、蛍光ペン ツールを使用してキャンバスに半透明のストロークを描画する例を示しています。":::

蛍光ペン ツールは、キャンバスに格納されている半透明のストロークを描画します。 既定のチップ図形は正方形です。

```html
<div>
  <button id="highlighter">Enable Highlighter</button><br />
  <label for="highlighter-color">Select a color:</label>
  <input type="color" id="highlighter-color" name="highlighter-color" value="#FFFC00" />
  <button id="highlighter-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to highlighter
document.getElementById("highlighter").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for highlighter
document.getElementById("highlighter-color").onchange = () => {
  const colorPicker = document.getElementById("highlighter-color");
  inkingManager.highlighterBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for highlighter
document.getElementById("highlighter-tip-size").onclick = () => {
  inkingManager.highlighterBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="eraser-tool"></a>消しゴム ツール

:::image type="content" source="../assets/images/teams-live-share/canvas-eraser-tool.gif" alt-text="GIF は、消しゴム ツールを使用してキャンバス上のストロークを消去する例を示しています。":::

消しゴム ツールは、パスをまたがるストローク全体を消去します。

```html
<div>
  <button id="eraser">Enable Eraser</button><br />
  <button id="eraser-size">Increase eraser size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("eraser").onclick = () => {
  inkingManager.tool = InkingTool.eraser;
};
// Increase the tip size for eraser
document.getElementById("eraser-size").onclick = () => {
  inkingManager.eraserSize = inkingManager.eraserSize + 1;
};
```

#### <a name="point-eraser-tool"></a>ポイント消しゴム ツール

:::image type="content" source="../assets/images/teams-live-share/canvas-point-eraser-tool.gif" alt-text="GIF は、ポイント消しゴム ツールを使用してキャンバス上のストローク内の個々のポイントを削除する例を示しています。":::

ポイント消しゴム ツールは、既存のストロークを半分に分割することで、そのパスを横断するストローク内の個々のポイントを消去します。 このツールは計算コストが高く、ユーザーのフレーム レートが遅くなる可能性があります。

> [!NOTE]
> ポイント消しゴムは、通常の消しゴム ツールと同じ消しゴムポイント サイズを共有します。

```html
<div>
  <button id="point-eraser">Enable Point Eraser</button><br />
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("point-eraser").onclick = () => {
  inkingManager.tool = InkingTool.pointEraser;
};
```

#### <a name="laser-pointer"></a>レーザー ポインター

:::image type="content" source="../assets/images/teams-live-share/canvas-laser-tool.gif" alt-text="GIF は、レーザー ポインター ツールを使用してキャンバスにストロークを描画する例を示しています。":::

レーザー ポインターは、マウスを動かすとレーザーの先端に後続の効果があるため、一意です。 ストロークを描画すると、後続の効果が短時間レンダリングされ、完全にフェードアウトします。 このツールは、発表者がストロークを消去するためにツールを切り替える必要がないため、会議中に画面上の情報を指摘するのに最適です。

```html
<div>
  <button id="laser">Enable Laser Pointer</button><br />
  <label for="laser-color">Select a color:</label>
  <input type="color" id="laser-color" name="laser-color" value="#000000" />
  <button id="laser-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to laser pointer
document.getElementById("laser").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for laser pointer
document.getElementById("laser-color").onchange = () => {
  const colorPicker = document.getElementById("laser-color");
  inkingManager.laserPointerBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for laser pointer
document.getElementById("laser-tip-size").onclick = () => {
  inkingManager.laserPointerBrush.tipSize = inkingManager.laserPointerBrush.tipSize + 1;
};
```

#### <a name="line-and-arrow-tools"></a>線と矢印のツール

:::image type="content" source="../assets/images/teams-live-share/canvas-line-tool.gif" alt-text="GIF は、線と矢印ツールを使用してキャンバスに直線を描画する例を示しています。":::

線ツールを使用すると、ユーザーは終点に適用できるオプションの矢印を使用して、ある点から別の点に直線を描画できます。

```html
<div>
  <button id="line">Enable Line</button><br />
  <button id="line-arrow">Enable Arrow</button><br />
  <input type="color" id="line-color" name="line-color" value="#000000" />
  <button id="line-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to line
document.getElementById("line").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "none";
};
// Change the selected tool to line
document.getElementById("line-arrow").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "open";
};
// Change the selected color for lineBrush
document.getElementById("line-color").onchange = () => {
  const colorPicker = document.getElementById("line-color");
  inkingManager.lineBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for lineBrush
document.getElementById("line-tip-size").onclick = () => {
  inkingManager.lineBrush.tipSize = inkingManager.lineBrush.tipSize + 1;
};
```

#### <a name="clear-all-strokes"></a>すべてのストロークをクリアする

を呼び出 `inkingManager.clear()`すことで、キャンバス内のすべてのストロークをクリアできます。 これにより、キャンバスからすべてのストロークが削除されます。

### <a name="cursors"></a>カーソル

:::image type="content" source="../assets/images/teams-live-share/canvas-cursors.gif" alt-text="GIF は、キャンバス上でカーソルを共有するユーザーの例を示しています。":::

ユーザーがキャンバス上で互いのカーソル位置を追跡できるように、アプリケーションでライブ カーソルを有効にすることができます。 インクツールとは異なり、カーソルはクラス全体で動作します `LiveCanvas` 。 必要に応じて、各ユーザーを識別する名前と画像を指定できます。 カーソルは、個別に有効にすることも、インクツールを使用して有効にすることもできます。

```javascript
// Optional. Set user display info
liveCanvas.onGetLocalUserInfo = () => {
  return {
    displayName: "YOUR USER NAME",
    pictureUri: "YOUR USER PICTURE URI",
  };
};
// Toggle Live Canvas cursor enabled state
liveCanvas.isCursorShared = !isCursorShared;
```

## <a name="optimizing-across-devices"></a>デバイス間での最適化

Web 上のほとんどのアプリケーションでは、画面サイズやアプリケーションの状態によって、コンテンツのレンダリング方法が異なります。 アプリに対して正しく最適化されていない場合 `InkingManager` は、ストロークとカーソルの表示がユーザーごとに異なる可能性があります。 Live Share キャンバスでは、簡単な API セットがサポートされています。これにより `<canvas>` 、ストロークの位置を調整してコンテンツに正しく揃えることができます。

既定では、Live Share キャンバスはホワイトボード アプリとよく似ています。コンテンツは 1 倍のズーム レベルでビューポートに中央揃えされます。 コンテンツの一部のみが 、 `<canvas>`. 概念的には、鳥の目からビデオを記録するようなものです。 カメラのビューポートは、その下の世界の一部を記録していますが、現実世界はあらゆる方向にほぼ無限に広がります。

この概念を視覚化するのに役立つ簡単な図を次に示します。

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-capabilities-docs-diagram-1.png" alt-text="デスクトップ ユーザーとモバイル ユーザーの全画面表示キャンバス レイアウトを示すスクリーンショット。":::

この動作は、次の方法でカスタマイズできます。

- 開始参照ポイントをキャンバスの左上隅に変更します。
- ビューポートのピクセル オフセット x 位置と y 位置を変更します。
- ビューポートのスケール レベルを変更します。

> [!NOTE]
> 参照ポイント、オフセット、およびスケール レベルはクライアントに対してローカルであり、会議の参加者間で同期されません。

例:

```html
<body>
  <button id="pan-left">Pan left</button>
  <button id="pan-up">Pan up</button>
  <button id="pan-right">Pan right</button>
  <button id="pan-down">Pan down</button>
  <button id="zoom-out">Zoom out</button>
  <button id="zoom-in">Zoom in</button>
  <button id="change-reference">Change reference</button>
</body>
```

```javascript
// ...

// Pan left
document.getElementById("pan-left").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x - 10,
    y: inkingManager.offset.y,
  };
};
// Pan up
document.getElementById("pan-up").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y - 10,
  };
};
// Pan right
document.getElementById("pan-right").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x + 10,
    y: inkingManager.offset.y,
  };
};
// Pan down
document.getElementById("pan-down").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y + 10,
  };
};
// Zoom out
document.getElementById("zoom-out").onclick = () => {
  if (inkingManager.scale > 0.1) {
    inkingManager.scale -= 0.1;
  }
};
// Zoom in
document.getElementById("zoom-in").onclick = () => {
  inkingManager.scale += 0.1;
};
// Change reference
document.getElementById("change-reference").onclick = () => {
  if (inkingManager.referencePoint === "center") {
    inkingManager.referencePoint = "topLeft";
  } else {
    inkingManager.referencePoint = "center";
  }
};
```

## <a name="ideal-scenarios"></a>理想的なシナリオ

すべての図形とサイズで Web ページが表示される場合、Live Share キャンバスをすべてのシナリオをサポートすることはできません。 このパッケージは、すべてのユーザーが同じコンテンツを同時に見ているシナリオに最適です。 すべてのコンテンツが画面に表示される必要はありませんが、デバイス間で線形にスケーリングされるコンテンツである必要があります。

Live Share キャンバスがアプリケーションに適したオプションであるシナリオの例をいくつか次に示します。

- すべてのクライアントで同じ縦横比でレンダリングされる画像とビデオをオーバーレイします。
- 同じ回転角度からマップ、3D モデル、またはホワイトボードを表示します。

どちらのシナリオも適切に機能します。ユーザーが異なるズーム レベルとオフセットを使用してコンテンツを見ている場合でも、すべてのデバイスでコンテンツを同じように表示できるためです。 画面サイズに応じてアプリのレイアウトやコンテンツが変更され、すべての参加者に共通のビューを生成できない場合、Live Share キャンバスはシナリオに適していない可能性があります。

## <a name="code-samples"></a>コード サンプル

| サンプルの名前          | 説明                            | JavaScript                                                                                |
| -------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------- |
| Live Canvas デモ     | シンプルなホワイトボード アプリケーション。         | [表示](https://github.com/microsoft/live-share-sdk/tree/main/samples/03.live-canvas-demo) |
| React メディア テンプレート | 同期されたビデオ プレーヤーの上に描画します。 | [表示](https://aka.ms/liveshare-mediatemplate)                                            |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アジャイル ポーカー チュートリアル](../sbs-teams-live-share.yml)

## <a name="see-also"></a>関連項目

- [Live Share SDK FAQ](teams-live-share-faq.md)
- [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
- [Live Share Canvas SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-canvas/)
- [会議の Teams アプリ](teams-apps-in-meetings.md)
