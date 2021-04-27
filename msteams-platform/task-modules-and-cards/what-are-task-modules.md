---
title: タスク モジュールとは
author: clearab
description: モーダル ポップアップ エクスペリエンスを追加して、Microsoft Teams アプリからユーザーに情報を収集または表示する
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 5472f07a8183e6f06ce6cb4fa2a9c048e083dcca
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019518"
---
# <a name="what-are-task-modules"></a>タスク モジュールとは

タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。 ポップアップ内では、独自のカスタム HTML/JavaScript コードを実行したり、YouTube や Microsoft Stream ビデオなどの -based ウィジェットを表示したり、アダプティブ カード `<iframe>` を [表示することができます](/adaptive-cards/)。 これらは特に、タスクの開始や完了、ビデオや Power BI ダッシュボードなどのリッチな情報の表示に役立ちます。 一般的にポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスに比べて、より自然にユーザーがタスクを開始したり完了したりすることができるようになっています。

タスク モジュールは、Microsoft Teams タブの基礎上に構築されます。基本的には、ポップアップ ウィンドウ内のタブです。 同じ SDK を使用します。タブを作成した場合は、タスク モジュールを作成する方法の 90% が既にあります。

タスク モジュールは次の 3 つの方法で呼び出すことができます。

* **チャネルタブまたは個人用タブ。** Microsoft Teams Tabs SDK を使用すると、タブのボタン、リンク、またはメニューからタスク モジュールを呼び出します。詳細については [、こちらを参照してください。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **ボット。** ボットから送信 [されたカード](~/task-modules-and-cards/cards/cards-reference.md) のボタン。 これは、ボットで何をしているのかを確認するためにチャネル内のすべてのユーザーを必要としない場合に特に便利です。 たとえば、チャネル内のユーザーに投票してもらう場合、投票中の記録が見えるのは好ましくありません。 [詳細については、こちらを参照してください。](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **深いリンクからの Teams の外部。** どこからでもタスク モジュールを呼び出す URL を作成できます。 [詳細については、こちらを参照してください。](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>タスク モジュールの外観

ボットから呼び出された場合のタスク モジュールの外観を次に示します (もちろん、色付き四角形と番号付き円はありません)。

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

次に示す方法を示します。

1. アプリのアイコン[ `color` です](~/resources/schema/manifest-schema.md#icons)。
2. アプリ[ `short` の名前です](~/resources/schema/manifest-schema.md#name)。
3. TaskInfo オブジェクトのプロパティで指定 `title` されたタスク モジュール [のタイトル](#the-taskinfo-object)です。
4. タスク モジュールの [閉じる/キャンセル] ボタン。 ユーザーがこれを押すと、アプリはここで説明するように `err` イベントを受信 [します](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)。 (**注:** 現在、タスク モジュールがボットから呼び出されると、このイベントを検出できない場合があります。
5. 青い四角形は、TaskInfo オブジェクトのプロパティを使用して独自の Web ページを読み込む場合に Web ページ `url` が [表示される場所です](#the-taskinfo-object)。 詳細については、以下のタスク [モジュールのサイズ設定](#task-module-sizing) セクションを参照してください。
6. TaskInfo オブジェクトのプロパティを介してアダプティブ カードを表示する場合は、パディングが追加されます。それ以外の場合は、これを自分 `card` [で処理する必要があります](#task-module-css-for-htmljavascript-task-modules)。 [](#the-taskinfo-object)
7. アダプティブ カード ボタンがここに表示されます。 独自のページを使用している場合は、独自のボタンを作成する必要があります。

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>タスク モジュールの呼び出しと終了の概要

タスク モジュールは、タブ、ボット、またはディープ リンクから呼び出すことができます。また、1 つのタブに表示される機能は HTML またはアダプティブ カードのいずれかなので、呼び出し方法とユーザーの対話の結果に対処する方法に関して、柔軟性が大きいです。 次の表に、この動作の概要を示します。

| **via... によって呼び出されます。** | **タスク モジュールは HTML/JavaScript です** | **タスク モジュールはアダプティブ カード** |
| --- | --- | --- |
| **タブ内の JavaScript** | 1. オプションのコールバック関数で Teams クライアント SDK `tasks.startTask()` 関数 `submitHandler(err, result)` を使用する <br/><br/> 2. タスク モジュール コードで、ユーザーが終了したら、オブジェクトをパラメーターとして Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。 コールバックが `submitHandler` で指定されている場合 `tasks.startTask()` 、Teams はそれをパラメーター `result` として呼び出します。<br/><br/> 3. 呼び出し時にエラーが発生した場合は、代わりに文字列 `tasks.startTask()` `submitHandler` で `err` 関数が呼び出されます。 <br/><br/> 4. 呼び出し時に指定することもできます 。その場合は、代わりにボット `completionBotId` `teams.startTask()` `result` に送信されます。 | 1. TaskInfo オブジェクトを使用して Teams クライアント SDK 関数を呼び出し、タスク モジュールポップアップに表示するアダプティブ カードの `tasks.startTask()` JSON[](#the-taskinfo-object) `TaskInfo.card` を含む。 <br/><br/> 2. でコールバックを指定した場合、Teams は、呼び出し時にエラーが発生した場合、またはユーザーが右上の X を使用してタスク モジュールポップアップを閉じる場合、文字列で呼び出します `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` 。 <br/><br/> 3. ユーザーが Action.Submit ボタンを押すと、そのオブジェクトがの値 `data` として返されます `result` 。 |
| **ボット カード ボタン** | 1. ボット カード ボタンは、ボタンの種類に応じて、ディープ リンク URL またはメッセージの送信という 2 つの方法でタスク モジュールを呼び出 `task/fetch` します。 ディープ リンク URL の動作については、以下を参照してください。 <br/><br/> 2. ボタンのアクションが ( アダプティブ カードのボタンの種類) の場合、イベント (表紙の下の HTTP POST) がボットに送信され、ボットは `type` `task/fetch` HTTP `Action.Submit` `task/fetch invoke` 200 で POST に応答し [、TaskInfo](#the-taskinfo-object)オブジェクトのラッパーを含む応答本文に応答します。 これは、タスク/フェッチを介して [タスク モジュールを呼び出す方法で詳しく説明します](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)。<br/><br/> 3. Teams はタスク モジュールを表示します。ユーザーが終了したら、オブジェクトをパラメーターとして Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。 <br/><br/> 4. ボットは、オブジェクト `task/submit invoke` を含むメッセージを受信 `result` します。 メッセージに応答するには、何もしない (タスクが正常に完了した) 方法、ポップアップ ウィンドウでユーザーにメッセージを表示する方法、または別のタスク モジュール ウィンドウを呼び出す方法 (ウィザードのようなエクスペリエンスの作成など) の 3 つの異なる方法があります `task/submit` 。 これら 3 つのオプションについては、task/submit に関する [詳細な説明で詳しく説明します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | 1. Bot Framework カードのボタンと同様に、アダプティブ カード上のボタンは、タスク モジュールを呼び出す 2 つの方法 (ボタンを含むディープ リンク URL とボタンの使用) を `Action.openUrl` `task/fetch` サポートします `Action.Submit` 。 <br/><br/> 2. アダプティブ カードを使用するタスク モジュールは、HTML/JavaScript の場合と非常に似た動作をします (左を参照)。 主な違いは、アダプティブ カードを使用している場合は JavaScript が無いから、呼び出す方法がない点です `tasks.submitTask()` 。 代わりに、Teams はオブジェクトを取得し、ここで説明するようにイベントのペイロード `data` `Action.Submit` `task/submit` として返 [します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 |
| **ディープ リンク URL** <br/>[URL 構文](#task-module-deep-link-syntax) | 1. Teams はタスク モジュールを呼び出します。ディープ リンクのパラメーターで指定 `<iframe>` された内部 `url` に表示される URL を指定します。 コールバック `submitHandler` はありません。 <br/><br/> 2. タスク モジュール内のページの JavaScript 内で、タブまたはボット カード ボタンから呼び出す場合と同じように、オブジェクトをパラメーターとして呼び出して閉じます `tasks.submitTask()` `result` 。 ただし、完了ロジックは若干異なります。 完了ロジックがクライアントに存在する場合 (つまり、ボットがない場合) にはコールバックが存在しないので、完了ロジックは呼び出しの前のコードに存在 `submitHandler` する必要があります `tasks.submitTask()` 。 呼び出しエラーは、コンソール経由でのみ報告されます。 ボットがある場合は、ディープ リンクでパラメーターを指定して、イベントを介して `completionBotId` `result` オブジェクトを送信 `task/submit` できます。 | 1. Teams はタスク モジュールを呼び出します。アダプティブ カードの JSON カード本文は、ディープ リンクのパラメーターの URL エンコード `card` 値として指定されます。 <br/><br/> 2. ユーザーは、タスク モジュールの右上にある X をクリックするか、カードのボタンを押してタスク モジュール `Action.Submit` を閉じます。 呼び出す必要はありませんので、アダプティブ カード フィールドの値を送信するボット `submitHandler` が必要です。 ディープ リンクの `completionBotId` パラメーターを使用して、イベント経由でデータを送信するボットを指定 `task/submit invoke` します。 |

> [!NOTE]
> JavaScript からタスク モジュールを呼び出す操作は、モバイルではサポートされていません。

## <a name="the-taskinfo-object"></a>TaskInfo オブジェクト

オブジェクト `TaskInfo` には、タスク モジュールのメタデータが含まれています。 オブジェクト定義は以下のとおりです。 ( **埋め** 込み iFrame 用) または (アダプティブ カード `url` 用) `card` を定義する必要があります。

| 属性 | 種類 | 説明 |
| --- | --- | --- |
| `title` | string | アプリ名の下とアプリ アイコンの右側に表示されます。 |
| `height` | number または string | これは、タスク モジュールの高さをピクセル単位で表す数値、または `small` 、 `medium` を指定できます `large` 。 [高さと幅の処理方法については、以下を参照してください](#task-module-sizing)。 |
| `width` | number または string | これは、タスク モジュールの幅をピクセル単位で表す数値、または `small` 、 `medium` 、または を指定できます `large` 。 [高さと幅の処理方法については、以下を参照してください](#task-module-sizing)。 |
| `url` | 文字列 | タスク モジュール内に読み込まれた `<iframe>` ページの URL。 URL のドメインは、アプリのマニフェスト内の [アプリの validDomains](~/resources/schema/manifest-schema.md#validdomains) 配列内にある必要があります。 |
| `card` | アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル | タスク モジュールに表示されるアダプティブ カードの JSON。 ボットから呼び出す場合は、Bot Framework オブジェクトでアダプティブ カード JSON を使用する必要 `attachment` があります。 タブからアダプティブ カードを使用します。 [例を次に示します。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | 文字列 | クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。 |
| `completionBotId` | 文字列 | タスク モジュールとのユーザーの対話の結果を送信するボット アプリ ID を指定します。 指定した場合、ボットはイベント ペイロード `task/submit invoke` に JSON オブジェクトを含むイベントを受信します。 |

> [!NOTE]
> タスク モジュール機能では、読み込む URL のドメインがアプリのマニフェストの配列 `validDomains` に含まれている必要があります。

## <a name="task-module-sizing"></a>タスク モジュールのサイズ変更

に整数を使用 `TaskInfo.width` `TaskInfo.height` し、高さと幅をピクセル単位で設定します。 ただし、チームのウィンドウのサイズと画面の解像度に応じて、縦横比 (幅/高さ) を維持しながら、比例して縮小されます。

If and are , or the size of the red rectangle in the picture in the available `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` space: 20%, 50%, 60% for and `width` 20%, 50%, 66% for `height` .

タブから呼び出されるタスク モジュールは、動的にサイズを変更できます。 呼び `tasks.startTask()` 出し後、newSize オブジェクトの高さと幅のプロパティが TaskInfo 仕様 `tasks.updateTask(newSize)` (ex. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>HTML/JavaScript タスク モジュールのタスク モジュール CSS

HTML/JavaScript ベースのタスク モジュールは、ヘッダーの下のタスク モジュールの領域全体にアクセスできます。 多くの柔軟性を提供しますが、ヘッダー要素に合わせてエッジをパディングし、不要なスクロール バーを回避する場合は、適切な CSS を提供する必要があります。 いくつかの使用例の例を次に示します。

### <a name="example-1---youtube-video"></a>例 1 - YouTube ビデオ

YouTube では、Web ページにビデオを埋め込む機能が提供されています。 単純なスタブ Web ページを使用すると、タスク モジュールで簡単に表示できます。

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

CSS を使用せずに、このページの HTML を次に示します。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

CSS は次のように表示されます。

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

### <a name="example-2---powerapp"></a>例 2 - PowerApp

PowerApp を埋め込む場合も、同じ方法を使用できます。 個々の PowerApp の高さ/幅がカスタマイズ可能なので、目的のプレゼンテーションを実現するために高さと幅を調整する必要がある場合があります。

![アセット管理 PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

CSS は次の値です。

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル

上記で説明したように、呼び出し方法によっては、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル (これは、添付ファイル オブジェクトにラップされたアダプティブ カード) を使用する必要があります `card` 。

タブから呼び出す場合は、アダプティブ カードを使用する必要があります。 非常に簡単な例を次に示します。

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat:"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png",
            "size": "Medium"
        }
    ],
    "version": "1.0"
}
```

ボットから呼び出す場合は、次の例のようにアダプティブ カード ボット カードの添付ファイルを使用する必要があります。

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
        "type": "AdaptiveCard",
        "body": [
            {
                "type": "TextBlock",
                "text": "Here is a ninja cat:"
            },
            {
                "type": "Image",
                "url": "http://adaptivecards.io/content/cats/1.png",
                "size": "Medium"
            }
        ],
        "version": "1.0"
    }
}
```

アダプティブ カードを含むタスク モジュールをボットまたはタブから呼び出すかどうかを覚えておく必要があります。

## <a name="task-module-deep-link-syntax"></a>タスク モジュールのディープ リンク構文

タスク モジュールのディープ リンクは、他の 2 つの情報を含む [TaskInfo](#the-taskinfo-object) オブジェクトのシリアル化であり、必要に応じて `APP_ID` 次の情報を使用します `BOT_APP_ID` 。

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

データ型 [および許容値については、TaskInfo](#the-taskinfo-object) オブジェクトを参照してください `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` 。

> [!TIP]
> 特にパラメーター (JavaScript の関数など) を使用する場合は、必ず URL でディープ リンク `card` をエンコード[ `encodeURI()` してください](https://www.w3schools.com/jsref/jsref_encodeURI.asp)。

に関する情報を次に `APP_ID` 示します `BOT_APP_ID` 。

| 値 | 種類 | 必須 | 説明 |
| --- | --- | --- | --- |
| `APP_ID` | string | はい | タスク [モジュール](~/resources/schema/manifest-schema.md#id) を呼び出すアプリの ID。 マニフェスト [の validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) には、URL に if の `APP_ID` `url` ドメイン `url` が含まれている必要があります。 (アプリ ID は、タブまたはボットからタスク モジュールが呼び出されると既に知られているので、そのモジュールは .) に含まれません `TaskInfo` 。 |
| `BOT_APP_ID` | 文字列 | いいえ | for の値 `completionBotId` を指定すると、オブジェクトはメッセージを `result` 介して指定 `task/submit invoke` されたボットに送信されます。 `BOT_APP_ID` アプリのマニフェストでボットとして指定する必要があります。つまり、ボットに送信する必要があります。 |

有効な場合と同じであり、多くの場合、アプリがボットを持っている場合は、ボットがある場合はアプリ `APP_ID` の ID として使用する必要があります。 `BOT_APP_ID`

## <a name="keyboard-and-accessibility-guidelines"></a>キーボードとアクセシビリティのガイドライン

HTML/JavaScript ベースのタスク モジュールでは、アプリのタスク モジュールをキーボードで使用できる必要があります。 スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。 実用的な問題として、これは次の 2 つのことを意味します。

1. HTML タグ [の tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) 属性を使用して、フォーカスできる要素と、シーケンシャル キーボード ナビゲーションに参加する場合と場所を制御します (通常は <kbd>Tab</kbd> キーと <kbd>Shift-Tab</kbd> キーを使用)。
2. タスク モジュール <kbd>の JavaScript</kbd> の Esc キーを処理します。 これを行う方法を示すコード サンプルを次に示します。

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams は、タスク モジュール のヘッダーから HTML へのキーボード ナビゲーションが正しく動作し、その逆も同様に動作します。

## <a name="code-sample"></a>コード サンプル
|**サンプル名** | **説明** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル (Bots-V4) | タスク モジュールを作成するためのサンプル。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|タスク モジュールのサンプル (タブ + Bots-V3) | タスク モジュールを作成するためのサンプル。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|



> [!div class="nextstepaction"]
> [詳細については、デバイスのアクセス許可の要求を参照してください](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [詳細: メディア機能の統合](../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [詳細: Teams に QR またはバーコード スキャナー機能を統合する](../concepts/device-capabilities/qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [詳細: Teams での場所機能の統合](../concepts/device-capabilities/location-capability.md)