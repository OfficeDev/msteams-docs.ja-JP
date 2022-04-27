---
title: タスク モジュールを呼び出して閉じる
description: コード サンプルを使用したタスク モジュール、タスク情報オブジェクト、タスク モジュールのサイズ設定、タスク モジュールのディープ リンク構文の呼び出しと無視について説明します
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5685e789dd6f4ad7cc39173e11af15dd9f7360fe
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073696"
---
# <a name="invoke-and-dismiss-task-modules"></a>タスク モジュールを呼び出して閉じる

タスク モジュールは、タブ、ボット、またはディープ リンクから呼び出すことができます。 応答は、HTML、JavaScript、またはアダプティブ カードのいずれかになります。 タスク モジュールの呼び出し方法と、ユーザーの操作の応答に対処する方法に関しては、多くの柔軟性があります。 次の表に、この動作の概要を示します。

| を使用して呼び出される | HTML または JavaScript を使用したタスク モジュール | アダプティブ カードを使用したタスク モジュール |
| --- | --- | --- |
| タブ内の JavaScript | 1. オプション`submitHandler(err, result)`のコールバック関数`tasks.startTask()`を使用して、Teams クライアント SDK 関数を使用します。 <br/><br/> 2. タスク モジュール コードで、ユーザーがアクションを実行したら、オブジェクトをパラメーターとしてTeams SDK 関数`tasks.submitTask()`を`result`呼び出します。 コールバックが`submitHandler`指定`tasks.startTask()`されている場合、Teamsパラメーターとして呼`result`び出します。 呼び出し `tasks.startTask()`時にエラーが発生した場合は、 `submitHandler` 代わりに文字列を `err` 使用して関数が呼び出されます。 <br/><br/> 3. 呼び出すとき`teams.startTask()`に指定`completionBotId`することもできます。 その後、 `result` 代わりにボットに送信されます。 | 1. [TaskInfo オブジェクト](#the-taskinfo-object)を使用してTeamsクライアント SDK 関数`tasks.startTask()`を呼び出し、`TaskInfo.card`アダプティブ カードの JSON を含めてタスク モジュールのポップアップに表示します。 <br/><br/> 2. コールバックが指定`tasks.startTask()`された場合`submitHandler`、呼び出し時にエラーが発生した場合、またはユーザーが右上の X を使用してタスク モジュールポップアップを閉じた場合、Teamsは文字列で呼び出`err``tasks.startTask()`します。 <br/><br/> 3. ユーザーがボタンを `Action.Submit` 押すと、その `data` オブジェクトが値 `result`として返されます。 |
| ボット カード ボタン | 1. ボット カード ボタンは、ボタンの種類に応じて、ディープ リンク URL またはメッセージの送信という 2 つの方法でタスク モジュールを `task/fetch` 呼び出すことができます。 <br/><br/> 2. ボタンのアクション`type`が`task/fetch``Action.Submit`アダプティブ カードのボタンの種類である場合は、`task/fetch invoke`HTTP POST であるイベントがボットに送信されます。 ボットは、HTTP 200 と [TaskInfo オブジェクト](#the-taskinfo-object)のラッパーを含む応答本文を使用して POST に応答します。 詳細については、[を使用した`task/fetch`タスク モジュールの呼び出しを](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)参照してください。 Teamsタスク モジュールが表示されます。 <br/><br/> 3. ユーザーがアクションを実行したら、オブジェクトをパラメーターとしてTeams SDK 関数`tasks.submitTask()`を`result`呼び出します。 ボットは、オブジェクトを `task/submit invoke` 含むメッセージを `result` 受け取ります。 <br/><br/> 4. メッセージに応答するには、タスクが正常に `task/submit` 完了したことを何も行っていないか、ポップアップ ウィンドウでユーザーにメッセージを表示するか、別のタスク モジュール ウィンドウを呼び出すことによって、3 つの異なる方法があります。 詳細については、詳細な [説明を `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)参照してください。 | <ul><li> Bot Framework カードのボタンと同様に、アダプティブ カードのボタンでは、タスク モジュールの呼び出し、ボタンを含む `Action.openUrl` ディープ リンク URL、および `task/fetch` ボタンの使用 `Action.Submit` の 2 つの方法がサポートされています。 </li></ul> <br/><br/> <ul><li> アダプティブ カードを使用するタスク モジュールは、HTML または JavaScript のケースとよく似ています。 主な違いは、アダプティブ カードを使用しているときに JavaScript がないため、呼び出す `tasks.submitTask()`方法がないことです。 代わりに、Teamsはオブジェクトから`Action.Submit`オブジェクトを`data`取得し、それをイベントの`task/submit`ペイロードとして返します。 詳細については[、「`task/submit`.](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit) </li></ul> |
| ディープ リンク URL <br/>[URL 構文](#task-module-deep-link-syntax) | 1. Teamsは、ディープ リンクのパラメーターで`url`指定された内部`<iframe>`に表示される URL であるタスク モジュールを呼び出します。 コールバックはありません `submitHandler` 。 <br/><br/> 2. タスク モジュール内のページの JavaScript 内で、タブまたはボット カード ボタンから呼び出すときと`result`同じように、パラメーターとしてオブジェクトを使用して閉じるように呼び`tasks.submitTask()`出します。 ただし、完了ロジックは若干異なります。 完了ロジックがクライアント上に存在する場合は、ボットがない場合はコールバックがないため `submitHandler` 、完了ロジックは呼び出し `tasks.submitTask()`の前のコードに含まれている必要があります。 呼び出しエラーは、コンソール経由でのみ報告されます。 ボットがある場合は、ディープ リンクにパラメーターを`completionBotId`指定して、イベントを介してオブジェクトを`result``task/submit`送信できます。 | 1. Teamsは、ディープ リンクのパラメーターの URL エンコード値として指定されたアダプティブ カードの `card` JSON カード本体であるタスク モジュールを呼び出します。 <br/><br/> 2. ユーザーは、タスク モジュールの右上にある X を選択するか、カードのボタンを押して、タスク モジュールを `Action.Submit` 閉じます。 呼び出す必要がないため `submitHandler` 、アダプティブ カード フィールドの値を送信するボットがユーザーに必要です。 ユーザーは、ディープ リンクのパラメーターを `completionBotId` 使用して、イベントを使用 `task/submit invoke` してデータを送信するボットを指定する必要があります。 |

次のセクションでは、タスク モジュールの `TaskInfo` 特定の属性を定義するオブジェクトを指定します。

## <a name="the-taskinfo-object"></a>TaskInfo オブジェクト

オブジェクトには `TaskInfo` 、タスク モジュールのメタデータが含まれています。 `url`埋め込み iFrame または`card`アダプティブ カードを定義します。 次の表に、オブジェクト定義を示します。

| 属性 | 種類 | 説明 |
| --- | --- | --- |
| `title` | string | この属性は、アプリ名の下とアプリ アイコンの右側に表示されます。 |
| `height` | number または string | この属性は、タスク モジュールの高さを表す数値 (ピクセル単位)、または `small`、 ( `medium`または `large`) を指定できます。 詳細については、「 [タスク モジュールのサイズ設定](#task-module-sizing)」を参照してください。 |
| `width` | number または string | この属性には、タスク モジュールの幅を表す数値 (ピクセル単位)、または `small`、 ( `medium`または `large`) を指定できます。 詳細については、「 [タスク モジュールのサイズ設定](#task-module-sizing)」を参照してください。 |
| `url` | string | この属性は、タスク モジュール内に `<iframe>` 読み込まれたページの URL です。 URL のドメインは、アプリのマニフェスト内のアプリの [validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) に含まれている必要があります。 |
| `card` | アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル | この属性は、アダプティブ カードがタスク モジュールに表示される JSON です。 ユーザーがボットから呼び出している場合は、Bot Framework `attachment` オブジェクトでアダプティブ カード JSON を使用します。 タブから、ユーザーはアダプティブ カードを使用する必要があります。 詳細については、「[アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル](#adaptive-card-or-adaptive-card-bot-card-attachment)」を参照してください。 |
| `fallbackUrl` | string | クライアントがタスク モジュール機能をサポートしていない場合、この属性はブラウザー タブで URL を開きます。 |
| `completionBotId` | string | この属性は、ユーザーがタスク モジュールと対話した結果を送信するボット アプリ ID を指定します。 指定した場合、ボットはイベント ペイロードに JSON オブジェクトを含むイベントを受信 `task/submit invoke` します。 |

> [!NOTE]
> タスク モジュール機能では、読み込む URL のドメインがアプリのマニフェストの配列に含まれている `validDomains` 必要があります。

次のセクションでは、ユーザーがタスク モジュールの高さと幅を設定できるようにするタスク モジュールのサイズを指定します。

## <a name="task-module-sizing"></a>タスク モジュールのサイズ設定

の整数を `TaskInfo.width` 使用して `TaskInfo.height`、タスク モジュールの高さと幅をピクセル単位で設定します。 ただし、チームのウィンドウのサイズと画面の解像度に応じて、縦横比 (幅または高さ) を維持しながら比例的に縮小されます。

`TaskInfo.height`次の図の赤い四角形のサイズが`"medium"``"small"``"large"`、使用可能な領域の割合(20%、50%、60%)、20%`width`、50%、66% `height`の場合。次の図の場合`TaskInfo.width`は 、次のようになります。

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="タスク モジュールの例":::

タブから呼び出されたタスク モジュールは、動的にサイズ変更できます。 呼び出した `tasks.startTask()` 後、newSize オブジェクトの高さと幅のプロパティが TaskInfo 仕様に準拠している場所を呼び出 `tasks.updateTask(newSize)` すことができます。たとえば `{ height: 'medium', width: 'medium' }`、

次のセクションでは、YouTube ビデオと PowerApp にタスク モジュールを埋め込む例を示します。

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>HTML または JavaScript タスク モジュール用のタスク モジュール CSS

HTML または JavaScript ベースのタスク モジュールは、ヘッダーの下にあるタスク モジュールの領域全体にアクセスできます。 非常に柔軟ですが、エッジの周囲にパディングを配置してヘッダー要素と一致させ、不要なスクロール バーを回避する場合は、ユーザーが適切な CSS を提供する必要があります。 次のセクションでは、いくつかのユース ケースの例をいくつか示します。

### <a name="example-1-youtube-video"></a>例 1: YouTube ビデオ

YouTube では、Web ページにビデオを埋め込むことができます。 単純なスタブ Web ページを使用して、タスク モジュール内の Web ページにビデオを簡単に埋め込むことができます。

:::image type="content" source="../../assets/images/task-module/youtube-example.png" alt-text="Youtube の例":::

次のコードは、CSS を含まない Web ページの HTML の例を示しています。

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

次のコードは、CSS の例を示しています。

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

### <a name="example-2-powerapp"></a>例 2: PowerApp

ユーザーは同じ方法で PowerApp を埋め込むことができます。 個々の PowerApp の高さまたは幅はカスタマイズ可能であるため、ユーザーは目的のプレゼンテーションを実現するために高さと幅を調整できます。

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="powerapp":::

次のコードは、PowerApp 用の HTML の例を示しています。

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

次のコードは、CSS の例を示しています。

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

次のセクションでは、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイルを使用してカードを呼び出す方法について詳しく説明します。

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル

呼び出し `card`方法に応じて、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイルを使用する必要があります。これは、添付ファイル オブジェクトにラップされたアダプティブ カードです。

タブから呼び出す場合、ユーザーはアダプティブ カードを使用する必要があります。

次のコードは、アダプティブ カードの例を示しています。

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

次のコードは、ボットから呼び出すときのアダプティブ カード ボット カードの添付ファイルの例を示しています。

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

次のセクションでは、オブジェクト `TaskInfo` や `APP_ID` `BOT_APP_ID`.

## <a name="task-module-deep-link-syntax"></a>タスク モジュールのディープ リンク構文

タスク モジュールディープ リンクは、次の 2 つの詳細を含む TaskInfo オブジェクトのシリアル化であり、必要に応じて次 `APP_ID` の情報を含 `BOT_APP_ID`みます。

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

、および [、TaskInfo オブジェクト](#the-taskinfo-object)の`<TaskInfo.url>``<TaskInfo.height>``<TaskInfo.card>``<TaskInfo.width>`データ型と`<TaskInfo.title>`許容される値については、「TaskInfo オブジェクト」を参照してください。

> [!TIP]
> URL は、パラメーター (JavaScript の関数など) を`card`使用するときにディープ リンクを[`encodeURI()`](https://www.w3schools.com/jsref/jsref_encodeURI.asp)エンコードします。

次の表に、次の情報を示します。`APP_ID` `BOT_APP_ID`

| 値 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `APP_ID` | string | はい | タスク モジュールを呼び出すアプリの [ID](~/resources/schema/manifest-schema.md#id) 。 マニフェスト内[の validDomains 配列](~/resources/schema/manifest-schema.md#validdomains)には、`APP_ID`url 内にある場合`url`の`url`ドメインが含まれている必要があります。 アプリ ID は、タスク モジュールがタブまたはボットから呼び出されたときに既にわかっています。そのため、タスク モジュールは  に含 `TaskInfo`まれていません。 |
| `BOT_APP_ID` | 文字列 | いいえ | 値 `completionBotId` が指定されている場合、オブジェクトは指定された `result` ボットにメッセージを `task/submit invoke` 使用して送信されます。 `BOT_APP_ID` はアプリのマニフェストでボットとして指定する必要があります。つまり、ボットに送信することはできません。 |

> [!NOTE]
> `APP_ID` アプリ `BOT_APP_ID` にアプリの ID として使用する推奨ボットがある場合は、多くの場合同じにすることができます。

次のセクションでは、アプリのタスク モジュールでキーボードを使用する方法について詳しく説明します。

## <a name="keyboard-and-accessibility-guidelines"></a>キーボードとアクセシビリティのガイドライン

HTML または JavaScript ベースのタスク モジュールでは、アプリのタスク モジュールをキーボードで使用できることを確認する必要があります。 スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。 これには、次の 2 つのことが含まれます。

* HTML タグで [tabindex 属性](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) を使用して、フォーカスできる要素を制御します。 また、Tabindex 属性を使用して、通常は <kbd>Tab</kbd> キーと <kbd>Shift キーを押しながら Tab キー</kbd> を押しながら、キーボードのシーケンシャル ナビゲーションに参加する場所を特定します。
* タスク モジュールの JavaScript で <kbd>Esc</kbd> キーを処理する。 次のコードは、 <kbd>Esc</kbd> キーを処理する方法の例を示しています。

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teamsにより、タスク モジュール ヘッダーから HTML へのキーボード ナビゲーションが正しく機能し、その逆も確実に機能します。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル ボット-V4 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|タスク モジュールのサンプル タブとボット-V3 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>関連項目

* [デバイスのアクセス許可を要求する](~/concepts/device-capabilities/native-device-permissions.md)
* [メディア機能を統合する](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Teams で QR コードまたはバーコード スキャナー機能を統合する](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Teams で位置情報機能を統合する](~/concepts/device-capabilities/location-capability.md)
