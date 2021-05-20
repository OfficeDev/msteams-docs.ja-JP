---
title: タスク モジュールとは
author: clearab
description: Microsoft Teamsアプリからユーザーに情報を収集または表示するためのモーダル ポップアップ エクスペリエンスを追加する
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23157e30ce25c2dfa1c21e7f5c4ddd4f735b660f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566843"
---
# <a name="task-modules"></a>タスク モジュール

タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。 ポップアップの内部では、独自のカスタム HTML/JavaScript コードを実行 `<iframe>` したり、YouTube や Microsoft Stream のビデオなどのベースのウィジェットを表示したり、 [アダプティブ カード](/adaptive-cards/)を表示したりできます。 これらは特に、タスクの開始や完了、ビデオや Power BI ダッシュボードなどのリッチな情報の表示に役立ちます。 一般的にポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスに比べて、より自然にユーザーがタスクを開始したり完了したりすることができるようになっています。

タスクモジュールは、Microsoft Teamsタブの基礎に基づいて構築されます。これらは、基本的にポップアップウィンドウ内のタブです。 これらは同じ SDK を使用するため、タブを作成した場合は、タスク モジュールを作成する方法の 90% が既に存在します。

タスク モジュールは次の 3 つの方法で呼び出すことができます。

* **チャンネルタブまたは個人用タブ**: Microsoft TeamsタブSDKを使用すると、タブ上のボタン、リンク、メニューからタスクモジュールを呼び出すことができます [。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **ボット**: ボットから送信された [カード](~/task-modules-and-cards/cards/cards-reference.md) のボタン。 これは、ボットで何をしているかを確認するためにチャネル内のすべてのユーザーが必要ない場合に特に便利です。 たとえば、チャネル内のユーザーに投票してもらう場合、投票中の記録が見えるのは好ましくありません。 [これについては、ここで詳しく説明します。](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **ディープリンクからTeamsの外**: どこからでもタスクモジュールを呼び出す URL を作成することもできます。 [これについては、ここで詳しく説明します。](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a>タスクモジュールは次のようになります

ボットから呼び出されたときのタスク モジュールは次のようになります (色付きの四角形と番号付きの円は除く)。

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

それを見てみましょう:

1. アプリの[ `color` アイコン](~/resources/schema/manifest-schema.md#icons)。
1. アプリの[ `short` 名前](~/resources/schema/manifest-schema.md#name)。
1. TaskInfo オブジェクトのプロパティで指定された `title` [タスク](#the-taskinfo-object)モジュールのタイトル。
1. タスク モジュールの閉じる/キャンセル ボタン。 ユーザーがこれを押すと、ここで説明するイベントがアプリに表示されます `err` 。 [](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)
    > [!Note]
    > 現在、タスク モジュールがボットから呼び出されたときに、このイベントを検出することはできません。
1. 青い四角形は、 TaskInfo オブジェクトのプロパティを使用して独自の Web ページを読み込む場合に Web ページが表示される場所 `url` です。 [](#the-taskinfo-object) 詳細については、以下の [タスク モジュールのサイズ設定](#task-module-sizing) に関するセクションを参照してください。
1. TaskInfo オブジェクトのプロパティを使用して Adaptive カードを表示する場合 `card` は、埋め込みが追加されます。 [](#the-taskinfo-object) [](#task-module-css-for-htmljavascript-task-modules)
1. アダプティブ カード ボタンは、ここに表示されます。 独自のページを使用している場合は、独自のボタンを作成する必要があります。

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>タスク モジュールの呼び出しと消去の概要

タスクモジュールはタブ、ボット、ディープリンクから呼び出し、HTMLまたはアダプティブカードのいずれかで表示されるため、どのように呼び出されるか、そしてユーザーの操作の結果にどのように対処するかという点で多くの柔軟性があります。 次の表は、このしくみを要約したものです。

| **を介して呼び出されます。** | **タスクモジュールはHTML/Javaスクリプトです** | **タスクモジュールはアダプティブカードです** |
| --- | --- | --- |
| **タブ内の JavaScript** | 1. オプションのコールバック関数でTeamsクライアント SDK `tasks.startTask()` 関数を使用 `submitHandler(err, result)` します。 <br/><br/> 2. タスク モジュール コードで、ユーザーが終了したら、 `tasks.submitTask()` パラメーターとしてオブジェクトを使用して Teams SDK 関数を呼び出 `result` します。 `submitHandler`コールバックが で指定されている場合 `tasks.startTask()` 、Teamsはパラメーターとして呼び出 `result` します。<br/><br/> 3. 呼び出し時にエラーが発生した場合 `tasks.startTask()` `submitHandler` 、関数は `err` 代わりに文字列で呼び出されます。 <br/><br/> 4. `completionBotId` 呼び出し時にを指定することもできます `teams.startTask()` 。 `result` | 1. TaskInfo オブジェクトを使用してTeamsクライアント SDK 関数を呼び出 `tasks.startTask()` し、タスク[](#the-taskinfo-object) `TaskInfo.card` モジュールポップアップに表示する Adaptive カードの JSON を含めます。 <br/><br/> 2. `submitHandler` コールバックが で指定されている場合 `tasks.startTask()` 、Teams呼 `err` び出し時にエラーがあった `tasks.startTask()` 場合、またはユーザーが右上の X を使用してタスク モジュール ポップアップを閉じた場合に、文字列を使用してコールバックを呼び出します。 <br/><br/> 3. ユーザーが Action.Submit ボタンを押すと、その `data` オブジェクトがの値として返されます `result` 。 |
| **ボット カード ボタン** | 1. ボットカードボタンは、ボタンの種類に応じて、ディープリンクURLまたはメッセージ送信の2つの方法でタスクモジュールを呼び出すことができます `task/fetch` 。 リンク URL の動作の詳細については、以下を参照してください。 <br/><br/> 2. ボタンのアクションが `type` `task/fetch` ( `Action.Submit` アダプティブ カードのボタンの種類) の場合 `task/fetch invoke` 、イベント (カバーの下の HTTP POST) がボットに送信され、ボットは HTTP 200 で POST に応答し、応答本文に [TaskInfo オブジェクト](#the-taskinfo-object)のラッパーを含む。 これは、 [タスク/フェッチを介してタスクモジュールを呼び出す方法](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch)で詳しく説明されています。<br/><br/> 3. Teamsタスクモジュールを表示します。ユーザーが終了したら、Teams SDK 関数を `tasks.submitTask()` パラメーターとしてオブジェクトを使用して呼び出 `result` します。 <br/><br/> 4. ボットは `task/submit invoke` 、オブジェクトを含むメッセージを受信 `result` します。 メッセージに応答するには、 `task/submit` 何もしない (タスクが正常に完了した) 、ポップアップ ウィンドウでユーザーにメッセージを表示する方法、または別のタスク モジュール ウィンドウを呼び出す (つまり、ウィザードのようなエクスペリエンスを作成する) という 3 つの方法があります。 これら 3 つのオプションについては、 [タスク/送信に関する詳細な説明](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)で詳しく説明します。 | 1. Bot Framework カードのボタンと同様に、Adaptive カードのボタンはタスク モジュールを呼び出す 2 つの方法をサポートします: ボタン付きディープ リンク URL `Action.openUrl` と `task/fetch` ボタンを使用して `Action.Submit` 。 <br/><br/> 2. アダプティブカードを使用したタスクモジュールは、HTML/JavaScriptの場合と非常に似ています(左を参照)。 主な違いは、アダプティブカードを使用しているときにJavaScriptが存在しないため、呼び出す方法がなさ `tasks.submitTask()` 代わりに、Teamsは `data` 、ここで説明しているように、オブジェクトをから取得 `Action.Submit` し、イベントのペイロードとして返 `task/submit` [します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 |
| **ディープリンクURL** <br/>[URL 構文](#task-module-deep-link-syntax) | 1. Teamsタスクモジュールを呼び出します。`<iframe>`ディープリンクのパラメータで指定された内部 `url` に表示されるURL。 `submitHandler`コールバックはありません。 <br/><br/> 2. タスクモジュールのページの JavaScript 内で、 `tasks.submitTask()` `result` タブやボットカードボタンから呼び出す場合と同じように、オブジェクトをパラメータとして閉じるように呼び出します。 ただし、完了ロジックは若干異なります。 完了ロジックがクライアント上にある場合 (つまり、ボットがない場合)、コールバックは存在 `submitHandler` しません `tasks.submitTask()` 。 呼び出しエラーはコンソールを介してのみ報告されます。 ボットがある場合は、 `completionBotId` ディープリンクでパラメータを指定して `result` 、イベントを介してオブジェクトを送信できます `task/submit` 。 | 1. Teamsタスクモジュールを呼び出します。アダプティブ カードの JSON カード本体は、ディープ リンクのパラメーターの URL エンコード値として指定 `card` されます。 <br/><br/> 2. タスクモジュールの右上にあるXをクリックするか、カードのボタンを押して、タスクモジュールを閉じます `Action.Submit` 。 `submitHandler`呼び出しが行ないため、Adaptive カード フィールドの値を送信するボットが必要です。 `completionBotId`ディープリンクのパラメータを使用して、イベントを介してデータを送信するボットを指定 `task/submit invoke` します。 |

## <a name="the-taskinfo-object"></a>オブジェクト

`TaskInfo`オブジェクトには、タスク モジュールのメタデータが含まれています。 オブジェクト定義は以下の通りです。  `url` 埋め込み iFrame または `card` アダプティブ カードのどちらかを定義する必要があります。

| 属性 | 種類 | 説明 |
| --- | --- | --- |
| `title` | string | アプリ名の下、アプリアイコンの右側に表示されます。 |
| `height` | number または string | これは、タスク モジュールの高さをピクセル単位で表す数値、または `small` `medium` 、、または を表す数値です `large` 。 [高さと幅の取り扱いについては、以下を参照](#task-module-sizing)してください。 |
| `width` | number または string | これは、タスク モジュールの幅をピクセル単位で表す数値、または `small` `medium` 、、または を表す数値です `large` 。 [高さと幅の取り扱いについては、以下を参照](#task-module-sizing)してください。 |
| `url` | string | タスク モジュール内に読み込まれたページ `<iframe>` の URL。 URL のドメインは、アプリのマニフェストのアプリの [validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) に含まれる必要があります。 |
| `card` | アダプティブ カードまたはアダプティブ カード ボット カードアタッチメント | タスク モジュールに表示されるアダプティブ カードの JSON。 ボットから呼び出す場合は、Bot Framework オブジェクトでアダプティブ カード JSON を使用する必要があります `attachment` 。 タブからは、アダプティブカードだけを使用します。 [例を次に示します。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開かれます。 |
| `completionBotId` | string | ユーザーがタスク モジュールと対話した結果を送信するボット アプリ ID を指定します。 指定した場合、ボットは `task/submit invoke` イベントペイロード内の JSON オブジェクトを含むイベントを受け取ります。 |

> [!NOTE]
> タスク モジュール機能では、読み込む URL のドメインが `validDomains` アプリのマニフェストの配列に含まれている必要があります。

## <a name="task-module-sizing"></a>タスク モジュールのサイズ変更

整数を使用 `TaskInfo.width` し、 `TaskInfo.height` 高さと幅をピクセル単位で設定します。 ただし、チームのウィンドウのサイズと画面の解像度によっては、縦横比 (幅/高さ) を維持しながら、比例して縮小されます。

`TaskInfo.width`と `TaskInfo.height` である場合 `"small"` 、 `"medium"` または `"large"` 上の図の赤い長方形のサイズは、利用可能なスペースの割合です:20%、50%、60% `width` と20%、50%、66%。 `height`

タブから呼び出されたタスク モジュールのサイズを動的に変更できます。 呼び出し後 `tasks.startTask()` に `tasks.updateTask(newSize)` newSize オブジェクトの高さと幅のプロパティが TaskInfo 仕様 (例. `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>HTML/JavaScript タスクモジュールのタスクモジュール CSS

HTML/JavaScript ベースのタスクモジュールは、ヘッダーの下にあるタスクモジュールの領域全体にアクセスできます。 これは非常に柔軟性がありますが、ヘッダー要素に合わせてエッジの周りにパディングを行い、不要なスクロールバーを避ける場合は、適切なCSSを提供する必要があります。 いくつかの使用例を次に示します。

### <a name="example-1---youtube-video"></a>例 1 - YouTube 動画

YouTube では、Web ページに動画を埋め込むことができます。 単純なスタブ Web ページを使用すると、タスク モジュールでこれを簡単に表示できます。

![ユーチューブ動画](~/assets/images/task-module/youtube-example.png)

CSS を使用しないこのページの HTML は次のとおりです。

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

CSS は次のようになります。

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

### <a name="example-2---powerapp"></a>例 2 - パワーアプリ

PowerApp を埋め込むのと同じアプローチを使用することもできます。 個々のPowerAppの高さ/幅はカスタマイズ可能であるため、必要なプレゼンテーションを実現するために高さと幅を調整する必要があります。

![資産管理パワーアプリ](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

そして、CSSは次のとおりです。

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>アダプティブ カードまたはアダプティブ カード ボット カードアタッチメント

上記で説明したように、どのように呼び出すかに応じて `card` 、アダプティブ カードまたはアダプティブ カード ボット カードアタッチメント (添付オブジェクトにラップされたアダプティブ カード) を使用する必要があります。

タブから呼び出す場合は、アダプティブ カードを使用する必要があります。 次に、非常に簡単な例を示します。

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

ボットから呼び出す場合は、次の例のようにアダプティブ カード のボット カードアタッチメントを使用する必要があります。

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

ボットまたはタブから Adaptive カードを含むタスク モジュールを呼び出すかどうかを覚えておく必要があります。

## <a name="task-module-deep-link-syntax"></a>タスク モジュールのディープ リンク構文

タスク モジュールのディープ リンクは、他の 2 つの情報を含む [TaskInfo オブジェクト](#the-taskinfo-object) のシリアル化 `APP_ID` であり、オプションで `BOT_APP_ID` :

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

データ型および 、 、 、および の許容値については、 [TaskInfo オブジェクト](#the-taskinfo-object) `<TaskInfo.url>` を参照 `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` してください。

> [!TIP]
> 特にパラメータを使用する場合は、ディープリンクをURLエンコードしてください `card` (例えば、JavaScriptの[ `encodeURI()` 関数](https://www.w3schools.com/jsref/jsref_encodeURI.asp))。

以下に記載の情報 `APP_ID` を示 `BOT_APP_ID` します。

| 値 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `APP_ID` | string | はい | タスク モジュールを呼び出すアプリの[ID。](~/resources/schema/manifest-schema.md#id) マニフェスト内の [validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) には `APP_ID` `url` 、URL に存在する場合のドメインが含まれている必要があります `url` 。 (このアプリ ID は、タブまたはボットからタスク モジュールが呼び出されたときに既に認識されています `TaskInfo` 。 |
| `BOT_APP_ID` | 文字列 | いいえ | の値 `completionBotId` が指定されている場合、 `result` オブジェクトはメッセージを介して `task/submit invoke` 指定されたボットに送信されます。 `BOT_APP_ID` アプリのマニフェストでボットとして指定する必要があります。 |

それは有効であり `APP_ID` `BOT_APP_ID` 、同じであることに注意してください、そして多くの場合、アプリがボットを持っている場合、それをアプリのIDとして使用することをお勧めします(もしある場合)。

## <a name="keyboard-and-accessibility-guidelines"></a>キーボードとユーザー補助のガイドライン

HTML/JavaScript ベースのタスクモジュールでは、アプリのタスクモジュールをキーボードで使用できるようにする責任があります。 スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。 現実的な問題として、これは2つのことを意味します:

1. HTML タグの [tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) を使用して、フォーカスを設定できる要素と、その要素が連続したキーボード ナビゲーションに参加するかどうか(通常は <kbd>Tab</kbd> キーと Shift キーを押しながら <kbd>Tab キーを</kbd> 押す)を制御します。
2. タスク モジュールの JavaScript で <kbd>Esc</kbd> キーを処理します。 これを行う方法を示すコード サンプルを次に示します。

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams、タスク モジュール ヘッダーから HTML にキーボード ナビゲーションが正しく動作し、その逆が正しく機能することを保証します。

## <a name="code-sample"></a>コード サンプル
|**サンプル名** | **説明** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|タスクモジュールのサンプル(Bots-V4) | タスクモジュールを作成するためのサンプルです。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|タスク モジュールのサンプル (タブ + ボット V3) | タスクモジュールを作成するためのサンプルです。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>関連項目

* [デバイスのアクセス許可を要求する](../concepts/device-capabilities/native-device-permissions.md)
* [メディア機能を統合する](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [TeamsでQRまたはバーコードスキャナ機能を統合](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Teamsでの位置情報機能の統合](../concepts/device-capabilities/location-capability.md)
