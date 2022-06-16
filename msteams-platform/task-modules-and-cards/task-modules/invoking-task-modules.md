---
title: タスク モジュールを呼び出して閉じる
description: コード サンプルを使用したタスク モジュール、タスク情報オブジェクト、タスク モジュール サイジング、タスク モジュール ディープ リンク構文の呼び出しと取り消しについて説明します
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 04e27e780c1d2686be2ee73909c2d28bfc19fd23
ms.sourcegitcommit: b4986bf529c74444db67b7ce522b3b0d2c2a8e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66130411"
---
# <a name="invoke-and-dismiss-task-modules"></a>タスク モジュールを呼び出して閉じる

タスク モジュールは、タブ、ボット、またはディープ リンクから呼び出すことができます。 応答は、HTML、JavaScript、または Adaptive Card のいずれかになります。 タスク モジュールの呼び出し方法と、ユーザーの操作の応答に対処する方法については、さまざまな柔軟性があります。 次の表はこのしくみを纏めています:

| 使用して呼び出される | HTML または JavaScript を使用したタスク モジュール | Adaptive Card を使用したタスク モジュール |
| --- | --- | --- |
| タブ内の JavaScript | 1. オプション `submitHandler(err, result)` のコールバック関数 `tasks.startTask()` を使用して、Teams クライアント SDK 関数を使用します。 <br/><br/> 2. タスク モジュール コードで、ユーザーがアクションを実行したら、`result` オブジェクトをパラメーターとして Teams SDK 関数 `tasks.submitTask()` を呼び出します。 コールバック `submitHandler` が `tasks.startTask()` で指定されている場合、`result` をパラメーターとして Teams を呼び出します。 `tasks.startTask()` の呼び出し時にエラーが発生した場合は、代わりに文字列 `err` を使用して `submitHandler` 関数が呼び出されます。 <br/><br/> 3. `teams.startTask()` を呼び出すときに `completionBotId` を指定することもできます。 その後、代わりに `result` がボットに送信されます。 | 1. [TaskInfo オブジェクト](#the-taskinfo-object) と、タスク モジュール ポップアップに表示する Adaptive Card の JSON を含む `TaskInfo.card` を使用して、Teams クライアント SDK 関数 `tasks.startTask()` を呼び出します。 <br/><br/> 2. `tasks.startTask()` でコールバック `submitHandler` が指定されているとき、`tasks.startTask()` を呼び出すときにエラーが発生した場合、または右上の X を使用してタスク モジュール ポップアップを閉じた場合、Teams は文字列 `err` を使用してコールバックを呼び出します。 <br/><br/> 3. ユーザーが `Action.Submit` ボタンを押すと、そのオブジェクト `data` が `result` の値として返されます。 |
| ボット カード ボタン | 1. ボット カード ボタンは、ボタンの種類に応じて、ディープ リンク URL またはメッセージ `task/fetch` の送信という 2 つの方法で、タスク モジュールを呼び出すことができます。 <br/><br/> 2. ボタンのアクション `type` が `task/fetch` であり、それは Adaptive Card のボタンの種類 `Action.Submit` である場合は、HTTP POST イベント `task/fetch invoke` がボットに送信されます。 ボットは HTTP 200 で POST に応答し、応答本文には [TaskInfo オブジェクト](#the-taskinfo-object)のラッパーが含まれています。 詳細については、「[`task/fetch`を使用したタスク モジュールの呼び出し](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)」を参照してください。 Teams はタスク モジュールを表示します。 <br/><br/> 3. ユーザーがアクションを実行したら、オブジェクト `result` をパラメーターとして指定して、Teams SDK 関数 `tasks.submitTask()` を呼び出します。 ボットは、オブジェクト `result` を含むメッセージ `task/submit invoke` を受け取ります。 <br/><br/> 4. メッセージ `task/submit` に応答する 3 つの方法があります。タスクが正常に完了したことを何も行わないか、ポップアップ ウィンドウでユーザーにメッセージを表示するか、別のタスク モジュール ウィンドウを呼び出すか、です。 詳細については、[次の詳細な説明を参照してください`task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | <ul><li> Bot Framework カードのボタンと同様に、Adaptive Card のボタンでは、タスク モジュールの呼び出しについて、ボタン `Action.openUrl` を含むディープ リンク URL、およびボタン `Action.Submit` を使用する `task/fetch` の 2 つの方法がサポートされています。 </li></ul> <br/><br/> <ul><li> アダプティブ カードを使用するタスク モジュールは、HTML または JavaScript のケースと同様に機能します。 主な違いは、アダプティブ カードを使用しているときに JavaScript がないため、呼び出す `tasks.submitTask()`方法がないことです。 代わりに、Teams は`Action.Submit`からオブジェクト `data` を取得し、イベント `task/submit` のペイロードとして返します。 詳細については、「[`task/submit`の柔軟性](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)」を参照してください。 </li></ul> |
| ディープ リンク URL <br/>[URL 構文](#task-module-deep-link-syntax) | 1. Teams は、ディープ リンクの `url` パラメーター内で指定された `<iframe>` 内に表示される URL で示されるタスク モジュールを呼び出します。 コールバックはありません `submitHandler` 。 <br/><br/> 2. タスク モジュールのページの JavaScript 内で、 `tasks.submitTask()` を呼び出して、タブまたはボット カード ボタンから呼び出すときと同じように、パラメーターとしてオブジェクト `result` 内で閉じます。 ただし、完了ロジックは若干異なります。 完了ロジックがクライアント上に存在する場合は、ボットがない場合はコールバックがないため `submitHandler` 、完了ロジックは呼び出し `tasks.submitTask()`の前のコードに含まれている必要があります。 呼び出しエラーは、コンソール経由でのみ報告されます。 ボットがある場合は、ディープ リンクでパラメーター `completionBotId` を指定して、イベント `task/submit` を介してオブジェクト `result` を送信できます。 | 1. Teams は、ディープ リンクのパラメーター `card` の URL エンコード値として指定された Adaptive Card の JSON カード本体であるタスク モジュールを呼び出します。 <br/><br/> 2. ユーザーは、タスク モジュールの右上にある X を選択するか、カードのボタン `Action.Submit` を押して、タスク モジュールを閉じます。 呼び出す必要がないため `submitHandler` 、アダプティブ カード フィールドの値を送信するボットがユーザーに必要です。 ユーザーはディープ リンクのパラメーター `completionBotId` を使用して、イベント `task/submit invoke` を使用してデータを送信するボットを指定する必要があります。 |

次のセクションでは、タスク モジュールの特定の属性を定義するオブジェクト `TaskInfo` を指定します。

## <a name="the-taskinfo-object"></a>TaskInfo オブジェクト

オブジェクト `TaskInfo` には、タスク モジュールのメタデータが含まれています。 埋め込み iFrame のための `url` またはAdaptive Card のための `card` を定義します。 次の表は、オブジェクト定義を提示します:

| 属性 | 種類 | 説明 |
| --- | --- | --- |
| `title` | string | この属性は、アプリ名の下とアプリ アイコンの右側に表示されます。 |
| `height` | number または string | この属性は、タスク モジュールの高さをピクセル単位で表す数値、または `small`、`medium`、または `large` を指定します。 詳細については、「[タスク モジュールのサイズ策定](#task-module-sizing)」を参照してください。 |
| `width` | number または string | この属性は、タスク モジュールの幅をピクセル単位で表す数値、または `small`、`medium`、または `large` で指定します。 詳細については、「[タスク モジュールのサイズ策定](#task-module-sizing)」を参照してください。 |
| `url` | string | この属性は、タスク モジュール内の `<iframe>` として読み込まれたページの URL です。 URL のドメインは、アプリのマニフェストにアプリの [validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) に含まれている必要があります。 |
| `card` | Adaptive Card または Adaptive Card ボット カードの添付ファイル | この属性は、タスク モジュールに表示される Adaptive Card 向けの JSON です。 ユーザーがボットから呼び出している場合は、Bot Framework オブジェクト `attachment` でAdaptive Card JSON を使用します。 タブから、ユーザーは Adaptive Card を使用する必要があります。 詳細については、「[Adaptive Card またはAdaptive Card ボット カードの添付ファイル](#adaptive-card-or-adaptive-card-bot-card-attachment)」を参照してください。 |
| `fallbackUrl` | string | クライアントがタスク モジュール機能をサポートしていない場合、この属性はブラウザー タブで URL を開きます。 |
| `completionBotId` | string | この属性は、ユーザーがタスク モジュールとやり取りした結果を送信するボット App ID を指定します。 指定した場合、ボットはイベント ペイロードに JSON オブジェクトを含むイベント `task/submit invoke` を受け取ります。 |

> [!NOTE]
> タスク モジュール機能では、読み込む URL のドメインが、アプリのマニフェストの配列 `validDomains` に含まれている必要があります。

次のセクションでは、ユーザーがタスク モジュールの高さと幅を設定できるように、タスク モジュールのサイズを指定します。

## <a name="task-module-sizing"></a>タスク モジュールのサイズ設定

`TaskInfo.width` および `TaskInfo.height` に整数を使用して、タスク モジュールの高さと幅をピクセル単位で設定します。 ただし、チームのウィンドウのサイズと画面の解像度に応じて、幅または高さの縦横比を維持しながら比例的に縮小されます。

`TaskInfo.width` と `TaskInfo.height` が `"small"`、`"medium"`、または `"large"` の場合、次の図の赤い四角形のサイズは、使用可能な領域の割合、`width` の場合は 20%、50%、60% で、`height` の場合は 20%、50%、66% です:

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="タスク モジュールの例":::

タブから呼び出されたタスク モジュールのサイズを動的に変更できます。 `tasks.startTask()` を呼び出した後、newSize オブジェクトの高さプロパティと幅プロパティが TaskInfo 仕様に準拠する `tasks.updateTask(newSize)` を呼び出すことができます。 例えば `{ height: 'medium', width: 'medium' }` です。

次のセクションでは、YouTube ビデオと Power Apps にタスク モジュールを埋め込む例を示します。

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>HTML または JavaScript タスク モジュール用のタスク モジュール CSS

HTML または JavaScript ベースのタスク モジュールは、ヘッダーの下にあるタスク モジュールの領域全体にアクセスできます。 柔軟性は非常に高くなりますが、エッジを埋め込んでヘッダー要素に合わせ、不要なスクロール バーを回避する場合は、ユーザーが適切な CSS を提供する必要があります。 次のセクションでは、2、3 のユース ケースについて幾つかの例を示します。

### <a name="example-1-youtube-video"></a>例 1: YouTube ビデオ

YouTube では、Web ページにビデオを埋め込むことができます。 単純なスタブ Web ページを使用して、タスク モジュール内の Web ページにビデオを簡単に埋め込むことができます。

:::image type="content" source="../../assets/images/task-module/youtube-example.png" alt-text="YouTube の例":::

次のコードは、CSS を含まない Web ページの HTML の例を示しています:

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

次のコードは、CSS の例を示しています:

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

### <a name="example-2-powerapp"></a>例 2: Power Apps

ユーザーは同じ方法を使用して Power Apps を埋め込むことができます。 個々の Power Apps の高さや幅をカスタマイズできるため、ユーザーは高さと幅を調整して目的のプレゼンテーションを実現できます。

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="Power Apps":::

次のコードは、Power Apps 用の HTML の例を示しています:

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

次のコードは、CSS の例を示しています:

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

次のセクションでは、Adaptive Card またはAdaptive Card ボット カードの添付ファイルを使用してカードを呼び出す方法について詳しく説明します。

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>Adaptive Card または Adaptive Card ボット カードの添付ファイル

呼び出し `card`方法に応じて、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイルを使用する必要があります。これは、添付ファイル オブジェクトにラップされたアダプティブ カードです。

タブから呼び出す場合、ユーザーはアダプティブ カードを使用する必要があります。

次のコードは、Adaptive Card の例を示しています:

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

次のセクションでは、`TaskInfo` オブジェクト、`APP_ID`、`BOT_APP_ID` など、タスク モジュールのディープ リンク構文について詳しく説明します。

## <a name="task-module-deep-link-syntax"></a>タスク モジュールのディープ リンク構文

タスク モジュールのディープ リンクは、TaskInfo オブジェクトのシリアル化であり、その他の 2 つの詳細、`APP_ID` と、必要に応じて `BOT_APP_ID` です:

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`<TaskInfo.url>`、`<TaskInfo.card>`、`<TaskInfo.height>`、`<TaskInfo.width>`、および `<TaskInfo.title>` のデータ型と許容値については、「[taskInfo オブジェクト](#the-taskinfo-object)」を参照してください。

> [!TIP]
> パラメーター `card` を使用する場合は、ディープ リンクを URL エンコードします。たとえば、JavaScript [ の `encodeURI()`関数](https://www.w3schools.com/jsref/jsref_encodeURI.asp)。

次の表に、`APP_ID` と `BOT_APP_ID` に関する情報を示します:

| 値 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `APP_ID` | string | はい | タスク モジュールを呼び出すアプリの [ID](~/resources/schema/manifest-schema.md#id)。 `APP_ID`のマニフェストの [validDomains 配列](~/resources/schema/manifest-schema.md#validdomains)には、`url` が URL 内に存在する場合、`url`のドメインが含まれている必要があります。 アプリ ID は、タスク モジュールがタブまたはボットから呼び出されたときに既にわかっています。そのため、アプリ ID は含まれていません `TaskInfo`。 |
| `BOT_APP_ID` | 文字列 | いいえ | `completionBotId` の値を指定した場合、オブジェクト `result` はメッセージ `task/submit invoke` を使用して指定したボットに送信されます。 `BOT_APP_ID` は、アプリのマニフェストでボットとして指定する必要があります。つまり、ボットに送信することはできません。 |

> [!NOTE]
> アプリに、アプリの ID として使用できる 1 つの推奨ボットがある場合、多くの場合 `APP_ID` と `BOT_APP_ID` は同じにすることができます。

次のセクションでは、アプリのタスク モジュールでキーボードを使用する方法について詳しく説明します。

## <a name="keyboard-and-accessibility-guidelines"></a>キーボードとアクセシビリティのガイドライン

HTML または JavaScript ベースのタスク モジュールでは、アプリのタスク モジュールをキーボードで使用できることを確認する必要があります。 スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。 これには、次の 2 つのことを含みます:

* HTML タグで [tabindex 属性](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) を使用して、フォーカスできる要素を制御します。 また、tabindex 属性を使用して、通常の <kbd>Tab キー</kbd> と <kbd>Shift-Tabキー</kbd>を使用してシーケンシャル キーボード ナビゲーションに関係する位置を特定します。
* タスク モジュールのために JavaScript 内で <kbd>Esc</kbd> キーに対応します。 次のコードは、<kbd>Esc</kbd> キーに対応する方法の例を示しています:

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams では、タスク モジュール ヘッダーから HTML へのキーボード ナビゲーションが正しく機能し、その逆も確実に行われます。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル ボット - V4 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|タスク モジュールのサンプル タブとボット - V3 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>関連項目

* [デバイスのアクセス許可を要求する](~/concepts/device-capabilities/native-device-permissions.md)
* [メディア機能を統合する](~/concepts/device-capabilities/media-capabilities.md)
* [Teams で QR コードまたはバーコード スキャナー機能を統合する](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Teams で位置情報機能を統合する](~/concepts/device-capabilities/location-capability.md)
