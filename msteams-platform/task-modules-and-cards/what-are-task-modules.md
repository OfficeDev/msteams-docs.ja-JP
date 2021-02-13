---
title: タスク モジュールとは
author: clearab
description: モーダル ポップアップ エクスペリエンスを追加して、Microsoft Teams アプリからユーザーに情報を収集または表示します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d92da7e6def6d66efd2f94600b7b8f8847553701
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231660"
---
# <a name="what-are-task-modules"></a>タスク モジュールとは

タスク モジュールを使用すると、Teams のアプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。 ポップアップ内では、独自のカスタム HTML/JavaScript コードを実行したり、YouTube や Microsoft Stream ビデオなどの -based ウィジェットを表示したり、アダプティブ カード `<iframe>` [を表示することができます](/adaptive-cards/)。 これらは特に、タスクの開始や完了、ビデオや Power BI ダッシュボードなどのリッチな情報の表示に役立ちます。 一般的にポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスに比べて、より自然にユーザーがタスクを開始したり完了したりすることができるようになっています。

タスク モジュールは、Microsoft Teams のタブの基礎に構築されます。基本的には、ポップアップ ウィンドウ内のタブです。 これらは同じ SDK を使用します。そのため、タブを作成している場合は、タスク モジュールを作成する方法の 90% が既に存在します。

タスク モジュールは次の 3 つの方法で呼び出すことができます。

* **[チャネル] タブまたは [個人用] タブ。** Microsoft Teams Tabs SDK を使用すると、タブのボタン、リンク、またはメニューからタスク モジュールを呼び出す方法について説明します。詳しくは、こちらを [参照してください。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **ボット。** ボットから送信 [されたカード](~/task-modules-and-cards/cards/cards-reference.md) のボタン。 これは、チャネル内のすべてのユーザーがボットで何を行っているのかを確認する必要が生じない場合に特に便利です。 たとえば、チャネル内のユーザーに投票してもらう場合、投票中の記録が見えるのは好ましくありません。 [詳しくは、ここをご覧ください。](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **ディープ リンクからの Teams の外部。** どこからでもタスク モジュールを呼び出す URL を作成できます。 [詳しくは、ここをご覧ください。](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>タスク モジュールの外観

ボットから呼び出された場合のタスク モジュールの外観を次に示します (もちろん、色付き四角形と番号付き円はありません)。

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

それでは、次の方法を見てみいます。

1. アプリの[ `color` アイコン。](~/resources/schema/manifest-schema.md#icons)
2. アプリの[ `short` 名前です](~/resources/schema/manifest-schema.md#name)。
3. TaskInfo オブジェクトのプロパティで指定されたタスク `title` モジュール [のタイトルです](#the-taskinfo-object)。
4. タスク モジュールの [閉じる]/[キャンセル] ボタン。 ユーザーがこれを押すと、アプリはここで説明する `err` イベントを受信 [します](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)。 (**注:** 現在、タスク モジュールがボットから呼び出された場合、このイベントを検出する機能は使用されません)。
5. 青色の四角形は、TaskInfo オブジェクトのプロパティを使用して独自の Web ページを読み込む場合に Web ページが `url` [表示される場所です](#the-taskinfo-object)。 詳細については、後の「 [タスク モジュールのサイズ変更」](#task-module-sizing) セクションを参照してください。
6. TaskInfo オブジェクトのプロパティを介してアダプティブ カードを表示している場合は、パディングが追加されます。それ以外の場合は、これを自分 `card` [で処理する必要があります](#task-module-css-for-htmljavascript-task-modules)。 [](#the-taskinfo-object)
7. アダプティブ カード ボタンがここに表示されます。 独自のページを使用している場合は、独自のボタンを作成する必要があります。

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>タスク モジュールの呼び出しと閉じの概要

タスク モジュールは、タブ、ボット、またはディープ リンクから呼び出すことができます。また、1 つに表示される機能は HTML またはアダプティブ カードのいずれかなので、起動方法とユーザーの対話の結果に対処する方法の点で柔軟性が高い。 次の表は、この動作の概要を示しています。

| **呼び出し方法** | **タスク モジュールは HTML/JavaScript です** | **タスク モジュールがアダプティブ カードである** |
| --- | --- | --- |
| **タブ内の JavaScript** | 1. オプションのコールバック関数で Teams クライアント SDK `tasks.startTask()` 関数を `submitHandler(err, result)` 使用する <br/><br/> 2. タスク モジュールのコードで、ユーザーが終了したら、オブジェクトをパラメーターとして Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。 コールバックが `submitHandler` 指定されている場合 `tasks.startTask()` 、Teams はそれをパラメーターとして `result` 呼び出します。<br/><br/> 3. 呼び出し中にエラーが発生した場合は、代わりに文字列を使用 `tasks.startTask()` `submitHandler` `err` して関数が呼び出されます。 <br/><br/> 4. 呼び出し時に指定することもできます。その場合は、代わりにボット `completionBotId` `teams.startTask()` `result` に送信されます。 | 1. TaskInfo オブジェクトを使用して Teams クライアント SDK 関数を呼び出し、タスク モジュール ポップアップに表示するアダプティブ カードの `tasks.startTask()` JSON[](#the-taskinfo-object) `TaskInfo.card` を含む。 <br/><br/> 2. コールバックが指定されている場合、呼び出し時にエラーが発生した場合、またはユーザーが右上の X を使用してタスク モジュールポップアップを閉じる場合 `submitHandler` `tasks.startTask()` 、Teams は `err` 文字列を使用してコールバックを呼び出します。 `tasks.startTask()` <br/><br/> 3. ユーザーが Action.Submit ボタンを押すと、そのオブジェクトが値 `data` として返されます `result` 。 |
| **ボット カード ボタン** | 1. ボット カードボタンは、ボタンの種類に応じて、ディープ リンク URL またはメッセージの送信という 2 つの方法でタスク モジュールを呼び出 `task/fetch` します。 ディープ リンク URL の動作については、以下を参照してください。 <br/><br/> 2. ボタンのアクションが ( アダプティブ カードのボタンの種類) の場合、イベント (表の下の HTTP POST) がボットに送信され、ボットは `type` `task/fetch` HTTP `Action.Submit` `task/fetch invoke` 200 で POST に応答し [、TaskInfo](#the-taskinfo-object)オブジェクトのラッパーを含む応答本文に応答します。 これは、タスク/フェッチを介 [してタスク モジュールを呼び出す方法で詳細に説明されています](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)。<br/><br/> 3. Teams はタスク モジュールを表示します。ユーザーが終了したら、オブジェクトをパラメーターとして Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。 <br/><br/> 4. ボットは、オブジェクト `task/submit invoke` を含むメッセージを受信 `result` します。 メッセージに応答するには、何もしない (タスクが正常に完了した) 方法、ポップアップ ウィンドウにユーザーにメッセージを表示する方法、または別のタスク モジュール ウィンドウを呼び出す方法 (ウィザードのようなエクスペリエンスの作成) の 3 つの方法があります。 `task/submit` これら 3 つのオプションについては、タスク/提出 [に関する詳細な説明で詳しく説明します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | 1. Bot Framework カードのボタンと同様に、アダプティブ カード上のボタンは、タスク モジュールを呼び出す 2 つの方法 (ボタンを含むディープ リンク URL とボタンの使用) をサポートしています `Action.openUrl` `task/fetch` `Action.Submit` 。 <br/><br/> 2. アダプティブ カードを含むタスク モジュールは、HTML/JavaScript のケースと非常に似た動作をします (左を参照)。 主な違いは、アダプティブ カードを使用している場合は JavaScript がないので、呼び出す方法がない点です `tasks.submitTask()` 。 代わりに、Teams はオブジェクトを取得し、ここで説明するようにイベントの `data` `Action.Submit` `task/submit` ペイロードとして返 [します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 |
| **ディープ リンク URL** <br/>[URL 構文](#task-module-deep-link-syntax) | 1. Teams はタスク モジュールを呼び出します。ディープ リンクのパラメーターで `<iframe>` 指定された内部に表示 `url` される URL。 コールバック `submitHandler` はありません。 <br/><br/> 2. タスク モジュールのページの JavaScript 内で、タブまたはボット カード ボタンから呼び出す場合と同じように、オブジェクトをパラメーターとして呼び出して閉じます。 `tasks.submitTask()` `result` ただし、完了ロジックは若干異なります。 完了ロジックがクライアント上にある場合 (つまり、ボットがない場合) にはコールバックが存在しないので、呼び出しの前のコードに完了ロジックを含む `submitHandler` 必要があります `tasks.submitTask()` 。 呼び出しエラーは、コンソール経由でのみ報告されます。 ボットがある場合は、ディープ リンクにパラメーターを指定して、イベントを介して `completionBotId` `result` オブジェクトを送信 `task/submit` できます。 | 1. Teams はタスク モジュールを呼び出します。アダプティブ カードの JSON カード本文は、ディープ リンクのパラメーターの URL エンコード `card` 値として指定されます。 <br/><br/> 2. ユーザーがタスク モジュールを閉じるには、タスク モジュールの右上にある [X] をクリックするか、カードのボタン `Action.Submit` を押します。 呼び出す必要は何もなから、アダプティブ カード フィールドの値を送信するボット `submitHandler` が必要です。 ディープ リンクの `completionBotId` パラメーターを使用して、イベント経由でデータを送信するボットを指定 `task/submit invoke` します。 |

> [!NOTE]
> JavaScript からのタスク モジュールの呼び出しは、モバイルではサポートされていません。

## <a name="the-taskinfo-object"></a>TaskInfo オブジェクト

オブジェクト `TaskInfo` には、タスク モジュールのメタデータが含まれます。 オブジェクトの定義を以下に示します。 ( **埋** め込み iFrame の場合) または (アダプティブ カード `url` の場合) `card` を定義する必要があります。

| 属性 | 種類 | 説明 |
| --- | --- | --- |
| `title` | string | アプリ名の下とアプリ アイコンの右側に表示されます。 |
| `height` | number または string | タスク モジュールの高さをピクセル単位で表す数値、または 、または `small` `medium` `large` . [高さと幅の処理方法については、以下を参照してください](#task-module-sizing)。 |
| `width` | number または string | タスク モジュールの幅をピクセル単位で表す数値、または 、または `small` `medium` `large` . [高さと幅の処理方法については、以下を参照してください](#task-module-sizing)。 |
| `url` | string | タスク モジュール内に読み込 `<iframe>` まれるページの URL。 URL のドメインは、アプリのマニフェスト内の [アプリの validDomains](~/resources/schema/manifest-schema.md#validdomains) 配列に含む必要があります。 |
| `card` | アダプティブ カードまたはアダプティブ カードボット カードの添付ファイル | タスク モジュールに表示されるアダプティブ カードの JSON。 ボットから呼び出す場合は、Bot Framework オブジェクトでアダプティブ カード JSON を使用する必要 `attachment` があります。 タブからアダプティブ カードを使用します。 [次に例を示します。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。 |
| `completionBotId` | string | タスク モジュールとのユーザーの対話の結果を送信するボット アプリ ID を指定します。 指定した場合、ボットはイベント ペイロードに `task/submit invoke` JSON オブジェクトを含むイベントを受信します。 |

> [!NOTE]
> タスク モジュール機能では、読み込む URL のドメインがアプリのマニフェストの配列 `validDomains` に含まれている必要があります。

## <a name="task-module-sizing"></a>タスク モジュールのサイズ変更

高さと幅を `TaskInfo.width` `TaskInfo.height` ピクセル単位で設定する整数を使用します。 ただし、チームのウィンドウのサイズと画面解像度に応じて、縦横比 (幅/高さ) を維持しながら、比例して縮小されます。

If `TaskInfo.width` and are, or the size of the red rectangle in the picture above is a proportion of the available `TaskInfo.height` `"small"` `"medium"` `"large"` space: 20%, 50%, 60% `width` for and 20%, 50%, 66% for `height` .

タブから呼び出されるタスク モジュールは、動的にサイズ変更できます。 呼び `tasks.startTask()` 出した後、newSize オブジェクトの高さと幅のプロパティが TaskInfo 仕様 `tasks.updateTask(newSize)` (例: `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>HTML/JavaScript タスク モジュール用のタスク モジュール CSS

HTML/JavaScript ベースのタスク モジュールは、ヘッダーの下のタスク モジュールの領域全体にアクセスできます。 これは大きな柔軟性を提供しますが、ヘッダー要素に合わせてエッジの周囲のパディングを使用し、不要なスクロール バーを回避する場合は、適切な CSS を提供する必要があります。 いくつかの使用例の例を次に示します。

### <a name="example-1---youtube-video"></a>例 1 - YouTube ビデオ

YouTube には、Web ページにビデオを埋め込む機能が用意されています。 単純なスタブ Web ページを使用すると、タスク モジュールで簡単に表示できます。

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

CSS を含めずに、このページの HTML を次に示します。

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

PowerApp を埋め込む場合も、同じ方法を使用できます。 個々の PowerApp の高さ/幅はカスタマイズ可能であり、目的のプレゼンテーションを実現するために高さと幅を調整する必要がある場合があります。

![Asset Management PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

CSS は次の要素です。

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>アダプティブ カードまたはアダプティブ カードボット カードの添付ファイル

前に説明したように、呼び出し方法に応じて、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル (添付ファイル オブジェクトにラップされたアダプティブ カード) を使用する必要があります `card` 。

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

ボットから呼び出す場合は、次の例に示すアダプティブ カード ボット カードの添付ファイルを使用する必要があります。

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

アダプティブ カードを含むタスク モジュールをボットから呼び出すのか、タブから呼び出すのかを覚えておく必要があります。

## <a name="task-module-deep-link-syntax"></a>タスク モジュールのディープ リンク構文

タスク モジュールのディープ リンクは、他の 2 つの情報と、オプションで次の 2 つの情報を持つ [TaskInfo](#the-taskinfo-object) オブジェクトのシリアル化 `APP_ID` です `BOT_APP_ID` 。

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

データ [型、および使用可能な値については、TaskInfo](#the-taskinfo-object) オブジェクトを参照してください `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` 。

> [!TIP]
> 特にパラメーター (JavaScript の関数など) を使用する場合は、必ず URL でディープ リンク `card` をエンコード[ `encodeURI()` してください](https://www.w3schools.com/jsref/jsref_encodeURI.asp)。

以下に情報を示 `APP_ID` します `BOT_APP_ID` 。

| 値 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `APP_ID` | string | はい | タスク モジュールを呼び出すアプリの[ID。](~/resources/schema/manifest-schema.md#id) マニフェスト [の validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) には、URL に if のドメイン `APP_ID` `url` `url` が含まれている必要があります。 (アプリ ID は、タスク モジュールがタブまたはボットから呼び出された場合に既に知られています。これは、それが含まれていない理由 `TaskInfo` です)。 |
| `BOT_APP_ID` | 文字列 | いいえ | 値が指定 `completionBotId` されている場合、オブジェクトはメッセージを介して指定 `result` `task/submit invoke` されたボットに送信されます。 `BOT_APP_ID` は、アプリのマニフェストでボットとして指定する必要があります。つまり、ボットに送信する必要があります。 |

これは有効であり、同じであり、多くの場合、アプリがボットを持っている場合は、ボットがある場合はアプリの ID として使用する必要があります。 `APP_ID` `BOT_APP_ID`

## <a name="keyboard-and-accessibility-guidelines"></a>キーボードとアクセシビリティのガイドライン

HTML/JavaScript ベースのタスク モジュールでは、アプリのタスク モジュールをキーボードで使用できる必要があります。 スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。 実際には、これは次の 2 つのことを意味します。

1. HTML タグ [で tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) 属性を使用して、フォーカスできる要素と、シーケンシャル キーボード ナビゲーションに参加する場合/参加する場所を制御します (通常 <kbd>、Tab</kbd> キーと <kbd>Shift キー</kbd> を使用)。
2. タスク モジュール <kbd>の JavaScript</kbd> で Esc キーを処理します。 これを行う方法を示すコード サンプルを次に示します。

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams は、タスク モジュール ヘッダーから HTML へのキーボード ナビゲーションが正しく機能し、その逆も正しく動作します。

## <a name="task-module-samples"></a>タスク モジュールのサンプル

* [Node.js/TypeScript サンプル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [C#/.NET サンプル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)

> [!div class="nextstepaction"]
> [詳細については、デバイスのアクセス許可の要求を参照してください](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [詳細: メディア機能の統合](../concepts/device-capabilities/mobile-camera-image-permissions.md)
